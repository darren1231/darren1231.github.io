---
layout: post
title: "batchnorm2conv"
date: 2020-04-19 23:21:10 +0800
comments: true
categories: 
---


# 融合batchnorm 至conv中

最近在將模型轉換成嵌入式裝置可以使用的模型時，發現很多人都會將batchnorm層溶入到卷積層中做運算，剛開始看程式都看不太懂，後來查詢了一些資料再自己推導一次，發現是很簡單的數學運算，覺得很有趣，特地記錄下來學習學習~~

## 公式運算:

原本的卷積核公式為

![](https://i.imgur.com/TqGySUA.png)

原本的batch_norm的公式為:

![](https://i.imgur.com/BS3sqH3.png)

如今要把batchnorm與卷積核融合成為同一個卷積核，也就是說要計算出一個新的權重w'與b'，如下列公式所示

![](https://i.imgur.com/bcjP84O.png)

再來就是公式推導了，首先將Z取代為wx+b然後代入

![](https://i.imgur.com/XSOTM2s.png)

之後移項推一推就可以得出下列式子

![](https://i.imgur.com/ZB1HY0y.png)

對照一下可以發現出新的w'與新的b'對照如下:

![](https://i.imgur.com/1heO534.png)

## 程式碼實現(caffe)

```
## load weights
mean = bn[0].data
var = bn[1].data
scalef = bn[2].data

# process scale
scales = scale[0].data
shift = scale[1].data

if scalef != 0:
    scalef = 1. / scalef
mean = mean * scalef
var = var * scalef

## process variance
rstd = 1. / np.sqrt(var + 1e-5)
                
## caculate conv   
rstd1 = rstd.reshape((channels,1,1,1))
scales1 = scales.reshape((channels,1,1,1))
wt = wt * rstd1 * scales1

## caculate bias
bias = (bias - mean) * rstd * scales + shift


## set nobn weights and bias
nobn.params[key][0].data[...] = wt
nobn.params[key][1].data[...] = bias
```

## 參考資料:
https://github.com/chuanqi305/MobileNet-SSD/blob/master/merge_bn.py
https://www.itread01.com/content/1556626925.html
https://stackoverflow.com/questions/49536856/tensorflow-how-to-merge-batchnorm-into-convolution-for-faster-inference
https://ithelp.ithome.com.tw/articles/10225171

###### tags: `learning report`