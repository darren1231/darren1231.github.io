---
layout: post
title: "在windows系統上用octopress打造自己的部落格"
date: 2020-01-19 22:02:26 +0800
comments: true
categories:
---


## 一.前言
小編之前一直都是使用匹克幫這種簡單的網站，不用費太多心力，直接剪剪貼貼就可以將圖片以及想要的資訊分享給大家，但使用一段時間後覺得匹克邦的網頁簡潔度、美觀都不如我長期使用的Markdown好用，常常Markdown寫完一篇文章後還要再花費心力整理到匹克幫然後做排版的動作，實在很費功夫，因此決定換個方式架設我的網站，搜尋了一下後發現竟然有可以使用github當成架設網站伺服器的方法，經過幾番摸索後終於架設成功了，底下就紀錄架設順序方便以後複習。

## 二.安裝步驟
底下介紹安裝的方法，首先要安裝ruby 環境以及gem

### a.安裝Ruby環境

* 官網:[https://rubyinstaller.org/downloads](https://rubyinstaller.org/downloads)

到上面的官網連結下載

#### 1.rubyinstaller-2.3.3-x64.exe

#### 2.DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe\

然後點擊安裝rubyinstaller，記得要勾選自動配置環境。

[](https://i.imgur.com/gnfUvGP.png)
![](https://i.imgur.com/3wDNMZH.png)

然後點擊安裝Devkit，選擇完解壓縮的位置後開啟命令提示元移動到安裝的資料夾下輸入以下指令


```
ruby dk.rb init 
ruby dk.rb install
```

![](https://i.imgur.com/8WsFsxQ.png)

### b.更新gem
安裝完成功後就要輸入以下指令更新gem，可以打gem測試看看有無成功
```
gem update --system
```
![](https://i.imgur.com/UntOmd4.png)

[](https://i.imgur.com/VavS8zg.png)

### c.用git拿到octopress資料
執行這步驟前先要確定電腦已經安裝了git，安裝完後打開git bash　輸入以下指令：
```
git clone git://github.com/imathis/octopress.git octopress
cd octopress
gem install bundler
bundle install
rake install

# gem uninstall rake(if you want to delete rake)
```
[](https://i.imgur.com/MULJVjR.png)
![](https://i.imgur.com/pydyfcD.png)
![](https://i.imgur.com/xokNqkp.png)

### d.設定github的路徑
這裡會將部落格原始碼連結到您的github帳號底下，沒有github帳好的請去申請一個，之後創造一個名稱為username.github.io的repository(注意：這裡要把username換成您的github帳號名稱)
![](https://i.imgur.com/15Xhsl2.png)

[](https://i.imgur.com/we7LvjE.png)

之後在git bash視窗下輸入下列程式碼，它會直接跳到下一行等待您輸入github的網域位置
```
rake setup_github_pages
git@github.com:darren1231/darren1231.github.io.git
```
[](https://i.imgur.com/zQux6dp.png)
![](https://i.imgur.com/sZOQZpX.png)

### e.接下來就可以運用rake指令管理您的部落格了
* 建立新文章
```
rake new_post["this is the title"]
```
* 發佈
```
rake generate
rake deploy
```
* 預覽
輸入下列程式碼就可以在本地端觀看網頁(在網址列輸入http://127.0.0.1:4000/)
```
rake preview
```

### f.push 到github上

```
git add .
git commit -m "first commit"
git push origin source
```

## 三.增加額外功能

### a.加入disqus 討論區
修改 _config.yml 內的 # Disqus Comments ，填上在 Disqus 申請的 short name ，並改成 true。

![](https://i.imgur.com/fprLGrc.png)

### b.加入數學公式
* 1.安裝kramdown
```
gem install kramdown
```
* 2.修改_config.yml
取代所有rdiscount 關鍵字成kramdown

* 3.修改Gemfile
把gem 'ridiscount'改成gem 'kramdown in Gemfile

* 4.添加Mathjax配置

在source/_includes/custom/head.html 添加以下代碼
```
<!-- mathjax config similar to math.stackexchange -->
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  jax: ["input/TeX", "output/HTML-CSS"],
  tex2jax: {
    inlineMath: [ ['$', '$'] ],
    displayMath: [ ['$$', '$$']],
    processEscapes: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
  },
  messageStyle: "none",
  "HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX","TeX"] }
});
</script>
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML" type="text/javascript"></script>
```

* 5.修復Mathjax右擊頁面空白bug

修改 sass/base/_theme.scss，並將div 改成 div#main
```
  > div#main {
     background: $sidebar-bg $noise-bg;
     border-bottom: 1px solid $page-border-bottom;
     > div {
```
* 6.測試公式

整段LeTex
```
$$
\begin{align}
\mbox{Union: } & A\cup B = \{x\mid x\in A \mbox{ or } x\in B\} \\
\mbox{Concatenation: } & A\circ B  = \{xy\mid x\in A \mbox{ and } y\in B\} \\
\mbox{Star: } & A^\star  = \{x_1x_2\ldots x_k \mid  k\geq 0 \mbox{ and each } x_i\in A\} \\
\end{align}
$$
```
$$
\begin{align}
\mbox{Union: } & A\cup B = \{x\mid x\in A \mbox{ or } x\in B\} \\
\mbox{Concatenation: } & A\circ B  = \{xy\mid x\in A \mbox{ and } y\in B\} \\
\mbox{Star: } & A^\star  = \{x_1x_2\ldots x_k \mid  k\geq 0 \mbox{ and each } x_i\in A\} \\
\end{align}
$$

內嵌 LaTex
```
If $a^2=b$ and $b=2$, then the solution must be
either $a=+\sqrt{2}$ or $a=-\sqrt{2}$.
```
If $a^2=b$ and $b=2$, then the solution must be
either $a=+\sqrt{2}$ or $a=-\sqrt{2}$.

## 四.參考資料
* [1.http://itspg.logdown.com/posts/1701-octopress-on-windows-tutorial](http://itspg.logdown.com/posts/1701-octopress-on-windows-tutorial)
* [2.http://www.yebangyu.org/blog/2015/10/17/howtoinstalloctopress/](http://www.yebangyu.org/blog/2015/10/17/howtoinstalloctopress/)
* [3.https://amos-vwr.blogspot.tw/2013/01/octopress-github.html](https://amos-vwr.blogspot.tw/2013/01/octopress-github.html)
* [4.http://dreamrunner.org/blog/2014/03/09/octopresszhong-shi-yong-latexxie-shu-xue-gong-shi/](http://dreamrunner.org/blog/2014/03/09/octopresszhong-shi-yong-latexxie-shu-xue-gong-shi/)