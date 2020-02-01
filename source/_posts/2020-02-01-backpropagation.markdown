---
layout: post
title: "類神經網路筆記"
date: 2020-02-01 15:51:57 +0800
comments: true
categories: 
---

## 一.前言

小編看了很多的書籍介紹類神經的，發現這本講的最淺顯易懂而且還附有程式碼，我認為電腦科學與其他物理學、電磁學...等最不同的點在於他是可以看出效果的，是感覺的到的，就算不太懂他的數學原理，反覆地去看程式碼再回來對照公式很快就可以更深入的了解，但是類似電磁學那種理論，即使你經由公式算出了電場是多少，電荷是多少，我依然沒有什麼感覺因為他看不到也摸不到，但電腦科學就不同了，你可以經由寫程式透過軟體去驗證你的理論正不正確，下面就帶各位一步一步地進入類神經的科學理論以及用個實際的例子說明這理論要如何使用。

![](https://i.imgur.com/gfzFe2N.png)

類神經網路與模糊控制理論入門與應用(附範例程式光碟片)


## 二.類神經生物模型

當今最神秘的器官不外乎就是我們人類的大腦，就算在21世紀的今日我們還是對大腦還是有許多不解的地方，因此許多科學家就想解開大腦的奧秘，當中一些電腦科學家就想把腦神經的運作原理透過數學的方式推導出一套可行的演算法出來，因此第一代類神經就這樣產生了。

* 下圖為一個典型的類神經圖解，人的腦神經系統分為下面幾個構造:

![](https://i.imgur.com/hDbP2li.png)




圖 １‑1

圖1中繪有兩個神經細胞，每個神經細胞主要由：（1）神經細胞核（Soma）、（2）神經軸（Axon）、（3）神經樹（Dendrites）、（4）神經節（Synapses）等四部分構成。底下，我們依序介紹此四部份。

* 神經細胞核（Soma）

它是神經細胞的中心體，它的作用，目前並沒有完全徹底的了解，大概是將神經樹收集到的信號，在此作加總後再作一次非線性轉換，再由神經軸將信號傳送到其它的神經細胞中。

* 神經軸（Axon）

連接在神經細胞核上，用來傳送由神經細胞核產生的信號至其它的神經細胞中。

* 神經樹（Dendrites）

神經樹分為兩種：輸入神經樹及輸出神經樹。在圖1中左邊接到神經核的神經樹是用來接收其他神經細胞傳來的信號，稱為輸入神經樹。而在圖1右側接到神經軸的神經樹是用來傳送信號至其它神經細胞，稱為輸出神經樹。所以我們可以說：神經樹是神經細胞呈樹枝狀的輸出入機構。

* 神經節（Synapse）

輸入神經樹和輸出神經樹相連接的點稱為神經節，如圖1中以小圓圈框起來的接點即是。每個神經細胞大約有1000個神經節。神經節是神經網路上的記憶體，它表示兩個神經細胞間的聯結強度，我們將此聯結強度以一個數值來表示，並稱之為加權值（weight）。



一般言之，當神經網路在進行學習時，外界刺激神經細胞所產生的電流會去改變神經節上的加權值，在學習過程中，外界刺激所產生的電流反覆在神經網路上流動，神經節上的加權值也反覆地改變，最後會慢慢的趨向穩定，此時即表示學習已告完成。若神經網路是處於認知或辨識的過程中，由外界刺激所產生的電流，在進入神經網路後，會與貯存在神經節上的加權值作簡單的運算處理，若處理後的信號為可辨識的信號，則外界事物便是神經網路可認知或辨識的的事物了。



## 三.類神經人工神經元模型


了解了生物神經細胞模型後，我們將介紹如何以人工神經元來模仿生物神經細胞。

讓我們再把相關的知識作個簡單的陳述，請參考圖1，當神經細胞透過輸入神經樹由其它神經細胞輸入脈波訊號後，經過神經細胞核的處理，其處理大約是將收集到的訊號作加總，再作一次非線性轉換後，產生一個新的脈波信號，如果這個訊號夠強，則新的脈波信號會由神經軸傳送到輸出神經樹，再透過神經節將此訊號傳給其它神經細胞。值得注意的是：當訊號經過神經節後，由於神經節加權值的影響，其訊號大小值會改變。經由上述的說明，我們提出人工神經元的模型如圖2所示。

![](https://i.imgur.com/jfV2Ke8.png)

圖 ２‑1

在圖2中，每一個人工神經元皆有多個輸入χ1, χ2, …, χn及一個輸出y，輸入值與輸出值的關係式，一般可用輸入值的加權乘積和的函數來表示，即

$$y\left( t \right) = f\lbrack\sum_{i = 1}^{n}{W_{i}*X_{i}\left( t \right) - \theta\rbrack}$$

其中

ｗi  = 模仿生物神經細胞的神經節加權值。

θ  = 模仿生物神經細胞的細胞核偏權值（bias），即輸入訊號的加權乘積和必須要大

於偏權值後，才能被傳輸至其它人工神經元中。

f（θ） = 模仿生物神經細胞的細胞核非線性轉換函數。

t = 時間。

n = 人工神經元輸入數目。



常用的非線性轉換函數


Sigmoid

![](https://i.imgur.com/Yi30lLE.png)

圖 ３‑1

Tanh

![](https://i.imgur.com/bw6sDzG.png)

圖 ３‑2

ReLU

![](https://i.imgur.com/KgP0SuQ.png)

圖 ３‑3

Leaky ReLU

![](https://i.imgur.com/NxdTgLs.png)

圖 ３‑4



## 四.單層感知機(perceptron)


此種類神經網路是經由F.Rosenblatt在1957年所提出，為最簡單形式的前饋神經網路，是一種二元線性分類器，當初他之所以會提出此種網路，是希望以此網路來模仿動物的大腦及視覺系統。雖然最初被認為有著良好的發展潛能，但感知機最終被證明不能處理諸多的模式識別問題。1969年，人工智慧支父Marvin Minsky和Seymour Papert在《Perceptrons》書中，仔細分析了以感知機為代表的單層神經網絡系統的功能及局限，證明感知機不能解決簡單的XOR等線性不可分問題。


![](https://i.imgur.com/y0BeBye.png)

圖 ４‑1

單層感知機的數學模型如圖4-1所示，其中ai表示網路的輸入信號，Wi表示網路的加權值，θ 為網路的偏權值，而其輸出方程式為:


$$Y = \left\{ \begin{matrix} 1,\text{if}\sum_{i}^{}{a_{i}W_{i} \geq \theta} \\ 0,\text{if}\sum_{i}^{}{a_{i}W_{i} < \theta} \\ \end{matrix} \right.\ $$

因此轉換函數為Step function


![](https://i.imgur.com/lHq937v.png)

圖 ４‑2

單層感知機早期應用在印刷字體的識別，如果輸入樣本是線性可分的，那麼單層感知機便可以成功地做分類，如以下例子。底下我們實現一個AND邏輯閘的單層感知機，我們將網路加權值設為 W1=1，W2=1，θ=1.5。


![](https://i.imgur.com/2fYNyD2.png)

圖 ４‑3

我們簡單的套用真質表來檢視這組參數，首先測試第一組X1=0,X2=0，代入公式後呈現


X1W1 + X2W2 − θ = −1.5 < 0

Fstep(−1.5)=0

繼續測試第二組 X1=1,X2=1，代入公式後呈現


X1W1 + X2W2 − θ = 0.5 > 0

Fstep(0.5)=1

各位可以繼續的測試其他兩樣，做出來也都是同樣符合真質表的描述，如果以X軸當資料X1，Y軸當作資料X2畫圖出來的話，可以發現我們所設的參數所描述的就是一條直線方程式，所以只要是畫在平面圖上且資料呈現線性可分特性，用感知機就能學出來。


![](https://i.imgur.com/tH3zh83.png)

圖 ４‑4

讓我們再來看一個例子，我們來找可以使得感知機可以解決Xor邏輯閘的參數。

根據第一組資料，我們可以推導出式子如下，因此θ > 0

X1 = 0, X2 = 0 → X1W1 + X2W2 = 0 < θ ( ３-4‑1)

再根據第二組資料，推出W2 > θ

X1 = 0, X2 = 1 → X1W1 + X2W2 = W2 > θ ( ４‑2)

繼續第三組資料，推出W1 > θ

X1 = 1, X2 = 0 → X1W1 + X2W2 = W1 > θ ( ４‑3)

最後一組推出 W1 + W2 < θ

X1 = 1, X2 = 1 → X1W1 + X2W2 = W1 + W2 < θ ( ４‑4)

由( ３-4‑2) ( ４‑2) ( ４‑3) 我們得知 W1 + W2 > θ ，但是( ４‑4)卻推出W1 + W2 < θ ，因此我們無法找到一組解使得單層感知機解決 Xor 問題，所以從此第一代類神經走入第一個寒冬中，因為它連Xor這麼簡單的問題都解決不了。

 
![](https://i.imgur.com/BPtTtku.png)

圖 ４‑5 圖 ４‑6



## 五.加入隱藏層的感知機


雖然單層感知機無法解決Xor問題，但是有科學家後續發現加入一個隱藏單元就可以順利排除這困難，原因是加入一個隱藏單元及等於是增加了一維變數，它會形成類似如圖4-5的橢圓曲線來做分類。一個可行的網路架構如圖5-1所示，它的輸出方程式為


$$y^{'} = \left\{ \begin{matrix} 1,\ \ \ \ if\ X_{1} + X_{2} > 1.5 \\ 0,\ \ \ if\ X_{1} + X_{2} < 1.5 \\ \end{matrix} \right.\ $$


$$y = \left\{ \begin{matrix} 1,\ \ \ if\ X_{1} + X_{2} - 2y' > 0.5\ \\ 0,\ \ \ if\ X_{1} + X_{2} - 2y^{'} \leq 0.5 \\ \end{matrix} \right.\ $$

我們仿造剛剛的運算，繼續將第一組數據帶入驗證測試，第一科神經元為


X1 = 0, X2 = 0 → X1W11 + X2W21 − θ1 = −1.5 < 0 → y′ = 0


X1W12 + X2W22 − 2y′ − θ2 = −0.5 < 0 → y = 0

第二組數據為X1 = 0, X2 = 1，第一二科神經元為


X1 = 0, X2 = 1 → X1W11 + X2W21 − θ1 = −0.5 < 0 → y′ = 0


X1W12 + X2W22 − 2y′ − θ2 = 0.5 > 0 → y = 1

第三組


X1 = 1, X2 = 0 → X1W11 + X2W21 − θ1 = −0.5 < 0 → y′ = 0


X1W12 + X2W22 − 2y′ − θ2 = 0.5 > 0 → y = 1

第四組


X1 = 1, X2 = 1 → X1W11 + X2W21 − θ1 = 0.5 > 0 → y′ = 1


X1W1 + X22W22 − 2y′ − θ2 = −0.5 < 0 → y = 0


![](https://i.imgur.com/h1eauzN.png)

圖 ５‑1

我們可以將上列方程式簡單的用 Matlab 跑圖驗證一下，可以發現產生如圖5-2 的效果，紅色代表輸出為1，藍色代表輸出為0，多加了一顆隱藏神經元就會產生另一條直線來畫分。




![](https://i.imgur.com/fDk8I4g.jpg)

圖 ５‑2

後續的研究人員重複著類似的實驗，並把神經元做多項的變化，比較加一層以及加兩層神經元的效果圖，可以統計出一張圖表如下(摘自書中)，他們發現神經元加越多層或是神經元加越多顆，所能區分的圖形就更複雜、圖形就更佳多樣化。


![](https://i.imgur.com/PLVor5S.png)

圖 ５‑3

## 六.倒傳遞神經網路


倒傳遞神經網路(Back-propagation Neural Network) 是一種具有學習能力的多層前授型網路。此網路是由 Rumelhart、Mcclelland在1985年所提出的，當初他們之所以會提出此種網路，是希望提出一種平行分布訊息的處理方法來探索人類認知的微結構。


![](https://i.imgur.com/wfUhq4z.png)

圖 ６‑1



* 簡單手算版


我找尋許多資料發現大多數講解倒傳遞類神經模型時都是用一堆數學公式，的確，類神經是經由精巧的微積分並運用微積分的連鎖律，一層一層地從後面傳遞誤差回去，因此我們就可以求出神經元權重的改變量，但直接看公式的話會很容易陷入迷思，因此我在網路上找到一份手算倒傳遞網路的資料 [6]，我把它翻譯成中文，相信經過這個例子的說明後再去看公式會容易許多。


![](https://i.imgur.com/KFUygYU.png)

圖 ６‑2

我們先從簡單的模型開始講起，倒傳遞網路的連接方式與perceptron不同，它是採取全部神經元互相連接的方式，但是只有層與層的神經元互相連結，層之間的神經元不做溝通，旁邊的數字代表參數的初始值為了等一下方便計算，這裡的b就是相當於剛剛所講的θ，事實上，大部分類神經書籍文獻都用b表示，只是書中為了與人腦神經元模型相呼應因此改成θ，在這裡我們將b命名為 bias，並將以前的公式改為如下


$$y\left( t \right) = f\lbrack\sum_{i = 1}^{n}{W_{i}*X_{i}\left( t \right) + b\rbrack}$$

假如我們這裡選的函數f是sigmoid函數，因此，這裡h1的輸出值就為


$${y_{h1} = f\left( w1*i1 + w2*i2 + b1 \right) = f\left( 0.15*0.05 + 0.2*0.1 + 0.35 \right) = f\left( 0.3825 \right)}$$

$${= \frac{1}{1 + e^{- 0.3825}} = 0.6}$$



用同樣的算法我們可以得出yh2 = 0.596884378

接下來以同樣的方法計算出o1, o2


outo1 = f(h1*w5+h2*w6+b2) = 0.75

outo2 = f(h1*w7+h2*w8+b2) = 0.773

這裡要注意的是作者似乎把bias項目簡化了，事實上每科神經元都各自有一個bias，但這裡作者為了計算方便將兩顆神經元的bias都設為一樣。

接下來我們要定義總體誤差為


$$E_{\text{total}} = \Sigma\frac{1}{2}\left( target - output \right)^{2}\ $$

其中target就是我們所想得到的值，整個演算法運作的目的就是想讓我的輸出越接近target越好，平方是為了消除正負號所帶來的影響，0.5是為了後面微分方便，加總是指，假如輸出神經元有N個，那就是代表要將N科神經元的誤差都加總起來，所以類神經訓練到最後Etotal會越來越小，代表神經元的輸出已經和我的樣本資料幾乎一模一樣了。

這裡輸出神經元有兩個，因此


$${E_{\text{total}} = E_{o1} + E_{o2} = \frac{1}{2}\left( \text{targe}t_{o1} - out_{o1} \right)^{2} + \frac{1}{2}\left( \text{targe}t_{o2} - out_{o2} \right)^{2}}$$

$${= \frac{1}{2}\left( 0.01 - 0.75 \right)^{2} + \frac{1}{2}\left( 0.99 - 0.773 \right)^{2} = 0.3}$$

再來我們要用微積分的連鎖律求出Etotal和w5的關係式，我們想要知道w5該如何調整能使我的Etotal變得更小，因此我們可以求出$\frac{\partial Etotal}{\partial w5}$ ，找出微分關係式後就可以套用底下公式找出調整w5的方向，其中α稱作學習率。

$$w5_{\text{new}} = w5_{\text{old}} - \alpha\frac{\partial Etotal}{\partial w5}$$


根據微積分連鎖率我們可以得知


$$\frac{\partial Etotal}{\partial w5} = \frac{\partial Etotal}{\partial out_{o1}}*\frac{\partial out_{o1}}{\partial\text{ne}t_{o1}}*\frac{\partial net_{o1}}{\partial w5}$$

其中neto1指的是f函式中裡面的加總式子，也就是說


neto1 = h1 * w5 + h2 * w6 + b2

接下來就是分別算出各項偏微分，然後再將它們組合起來就可以得到$\frac{\partial Etotal}{\partial w5}$

首先算出第一項$\frac{\partial Etotal}{\partial out_{o1}}$，回想起剛剛定義的Etotal為


$$E_{\text{total}} = \frac{1}{2}\left( \text{targe}t_{o1} - out_{o1} \right)^{2} + \frac{1}{2}\left( \text{targe}t_{o2} - out_{o2} \right)^{2}$$

因此


$$\frac{\partial Etotal}{\partial out_{o1}} = \frac{1}{2}*2*\left( \text{targe}t_{o1} - out_{o1} \right)* - 1 + 0 = - \left( 0.01 - 0.75 \right) = 0.74$$

再來計算第二項$\frac{\partial out_{o1}}{\partial net_{o1}}$，回想起剛剛解釋的neto1，因此


$$\text{ou}t_{o1} = \ f\left( \text{ne}t_{o1} \right) = \frac{1}{1 + e^{- net_{o1}}}$$

所以


$$\frac{\partial out_{o1}}{\partial net_{o1}} = \ \text{ou}t_{o1}*\left( 1 - \text{ou}t_{o1} \right) = 0.75*\left( 1 - 0.75 \right) = 0.186$$

最後一項$\frac{\partial net_{o1}}{\partial w5}$，因為neto1 = h1 * w5 + h2 * w6 + b2，所以


$$\frac{\partial net_{o1}}{\partial w5} = h1 = 0.6$$

全部組裝再一起可以得到


$$\frac{\partial Etotal}{\partial w5} = 0.74*0.186*0.6 = 0.082$$

假設學習率為0.5，因此我們就可以得知


$$w5_{\text{new}} = w5_{\text{old}} - \alpha*\frac{\partial Etotal}{\partial w5} = 0.4 - 0.5*0.082 = 0.359$$

圖6-3為作者所畫的流程圖，這就是為什麼網路稱為倒傳遞神經網路的原因，從最後一層的Error項傳遞誤差到outo1，然後再到neto1，一直層層傳遞到w5。


![](https://i.imgur.com/dMIhwux.png)

圖 ６‑3

我們可以用同樣的方法算出其他科神經元


w6new = 0.4

w7new = 0.51

w8new = 0.56


![](https://i.imgur.com/bxwDZLd.png)

圖 ６‑4

再來我們要將Error繼續傳遞到 w1，因此我們要算出$\frac{\partial Etotal}{\partial w1}$

我們一樣套用連鎖率概念可以得知


$$\frac{\partial Etotal}{\partial w1} = \frac{\partial Etotal}{\partial\text{ou}t_{h1}}*\frac{\partial out_{h1}}{\partial net_{h1}}*\frac{\partial net_{h1}}{\partial w1}$$

其中$\frac{\partial Etotal}{\partial out_{h1}}$     為如下，因為改變outh1對後面每一項的誤差皆有影響，因此必須把它們加總起來


$$\frac{\partial Etotal}{\partial out_{h1}} = \frac{\partial E_{o1}}{\partial out_{h1}} + \frac{\partial E_{o2}}{\partial out_{h1}}$$

我們開始像剛剛一樣逐個計算偏微分項目，從$\frac{\partial E_{o1}}{\partial out_{h1}}$開始，我們可以套用剛剛已經求得的項目


$$\frac{\partial E_{o1}}{\partial out_{h1}} = \frac{\partial E_{o1}}{\partial net_{o1}}*\frac{\partial net_{o1}}{\partial out_{h1}} = \frac{\partial E_{o1}}{\partial out_{o1}}*\frac{\partial out_{o1}}{\partial net_{o1}}*\frac{\partial net_{o1}}{\partial out_{h1}} = 0.74*0.18*\frac{\partial\text{ne}t_{o1}}{\partial out_{h1}}$$

因為 neto1 = w5 * outh1 + w6 * outh2 + b2 * 1，所以


$$\frac{\partial net_{o1}}{\partial out_{h1}} = w5 = 0.4$$

組合起來就得到


$$\frac{\partial E_{o1}}{\partial out_{h1}} = 0.74*0.18*0.4 = 0.0554$$

同樣的程序我們可以得到


$$\frac{\partial E_{o2}}{\partial out_{h1}} = - 0.02$$

因此


$$\frac{\partial Etotal}{\partial\text{ou}t_{h1}} = 0.0554 - 0.02 = 0.0354$$

再來繼續算第二項$\frac{\partial out_{h1}}{\partial net_{h1}}$

∵$out_{h1} = \frac{1}{1 + e^{- net_{h1}}}$          

∴$\frac{\partial out_{h1}}{\partial net_{h1}}=out_{h1}*(1-out_{h1})=0.6\times(1-0.6)=0.24$


最後一項$\frac{\partial\text{ne}t_{h1}}{\partial w1}$

∵neth1 = w1 * i1 + w2 * i2 + b1 * 1 

∴$\frac{\partial net_{h1}}{\partial w1} = i1 = 0.05$(也就是前一層的輸出)

全部組裝再一起可以得到

$$\frac{\partial Etotal}{\partial w1} = \frac{\partial Etotal}{\partial out_{h1}}*\frac{\partial out_{h1}}{\partial net_{h1}}*\frac{\partial net_{h1}}{\partial w1} = 0.0354*0.24*0.05 = 0.0004248$$

因此

$w1_{\text{new}}$

$=w1_{old} - \alpha\frac{\partial Etotal}{\partial w1}$

$= 0.15 - 0.5*0.0004248 = 0.1497876$

同樣的也可以找出隱藏層的其他weight出來


w2new = 0.19956143

w3new = 0.24975114

w4new = 0.29950229

有了前面的例子作簡介後，接下來我們要代入公式版的backpropagation推導，如果在公式版的有哪個地方看不懂，請反覆去回顧剛剛講的簡介，如此來回推敲多次相信很快就能理解的。

* 複雜公式版

![](https://i.imgur.com/WcFveG3.png)

圖 ６‑5

$a_{j}^{l} = f(\sum_{k}^{}{w_{\text{jk}}^{l}a_{k}^{l - 1} + b_{j}^{l})} = f(z_{j}^{l})$ ( ６-2‑1)

首先我們先定義各項參數，$a_{j}^{l}$代表在第l層中，第j科神經元的輸出，$w_{\text{jk}}^{l}$代表在模型中第l層和l-1層中的權重值，$b_{j}^{l}$代表在模型中第l層和l-1層中的偏權值，k代表l-1層的神經元索引值。

$E = \frac{1}{2}\sum_{n}^{}\left\lbrack y_{j} - a_{j}^{L} \right\rbrack^{2}$ ( ６-2‑2)

其中，L代表最後一層，$a_{j}^{L}$代表在輸出層中第j科神經元的輸出，$y_j$是代表第j個輸出的樣本，n代表最後一層神經元個數，我們將輸出層所有神經元誤差都加總起來，並加上平方項目以消除正負號所帶來的影響，最後除以2來當作整個神經網路的總體誤差。

我們首先求得總體誤差對輸出層權重質的微分，根據微積分的交換率我們可以改寫如以下公式( ６-2‑3)，我們分別對各個篇微分項做運算得到( ６-2‑4) ( ６-2‑5) ( ６-2‑6)

$\frac{\partial E}{\partial w_{\text{jk}}^{L}} = \frac{\partial E}{\partial a_{j}^{L}}*\frac{\partial a_{j}^{L}}{\partial z_{j}^{L}}\times\frac{\partial z_{j}^{L}}{w_{\text{jk}}^{L}}$ ( ６-2‑3)

$\frac{\partial E}{\partial a_{j}^{L}} = - (y_{j} - a_{j}^{L})$ ( ６-2‑4)

$\frac{\partial a_{j}^{L}}{\partial z_{j}^{L}} = \frac{\partial f\left( z_{j}^{L} \right)}{\partial z_{j}^{L}} = f'(z_{j}^{L})$ ( ６-2‑5)

$\frac{\partial z_{j}^{L}}{\partial w_{jk}^{L}}=\frac{\partial\sum_{k}^{}{w_{\text{jk}}^{L}a_{k}^{L - 1} + b_{j}^{L}}}{\partial w_{jk}^{L}} = a_{k}^{L - 1}$( ６-2‑6)


將( ６-2‑4) ( ６-2‑5) ( ６-2‑6)組裝再一起我們可以得到( ６-2‑8)，其中$δ_j^L$稱作在L層第j顆神經元的敏感度，式子如( ６-2‑9)所示。


$\frac{\partial E}{\partial w_{\text{jk}}^{L}} = a_{k}^{L - 1}\left( a_{j}^{L} - y_{j} \right)f^{'}\left( z_{j}^{L} \right) = a_{k}^{L - 1}\delta_{j}^{L}$ ( ６-2‑8)

$δ_j^L = (a_j^L−y_j)f′(z_j^L)$ ( ６-2‑9)

再來我們求得總體誤差對隱藏層權重值的偏導數，我們一樣可以按照連鎖律將式子拆成如( ６-2‑10)所示，依照剛剛的方法分別運算可以求得式子( ６-2‑11) ( ６-2‑12) ( ６-2‑13)

$\frac{\partial E}{\partial w_{\text{ki}}^{L - 1}} = \frac{\partial E}{\partial a_{k}^{L - 1}}\times\frac{\partial a_{k}^{L - 1}}{\partial z_{k}^{L - 1}}\times\frac{\partial z_{k}^{L - 1}}{w_{\text{ki}}^{L - 1}}$ ( ６-2‑10)

$\frac{\partial E}{\partial a_{k}^{L - 1}} = \sum_{j}^{}{\frac{\partial E}{\partial a_{j}^{L}}\times\frac{\partial a_{j}^{L}}{\partial z_{j}^{L}}}\times\frac{\partial z_{j}^{L}}{\partial a_{k}^{L - 1}}$ ( ６-2‑11)

$\frac{\partial a_{k}^{L - 1}}{\partial z_{k}^{L - 1}} = f'(z_{k}^{L - 1})$ ( ６-2‑12)



$\frac{\partial z_{k}^{L - 1}}{w_{\text{ki}}^{L - 1}} = a_{i}^{L - 2}$ ( ６-2‑13)

其中( ６-2‑11-1) 為式子( ６-2‑11)中的子項目，( ６-2‑11-1-1)為( ６-2‑11-1)的子項目，( ６-2‑12) ( ６-2‑13)與( ６-2‑5) ( ６-2‑6)算法一樣只是代號變了。

$\frac{\partial E}{\partial a_{k}^{L - 1}} = \sum_{j}^{}{\frac{\partial E}{\partial a_{j}^{L}}}\frac{\partial a_{j}^{L}}{\partial z_{j}^{L}}\frac{\partial z_{j}^{L}}{\partial a_{k}^{L - 1}}\ = \sum_{j}^{}(a_{j}^{L} - y_{j})f'(z_{j}^{L})w_{\text{jk}}^{L}$ ( ６-2‑11-1)

$\frac{\partial z_{j}^{L}}{\partial a_{k}^{L - 1}} = \frac{\partial\sum_{k}^{}{w_{\text{jk}}^{L}a_{k}^{L - 1} + b_{j}^{L}}}{\partial a_{k}^{L - 1}} = w_{\text{jk}}^{L}$ ( ６-2‑11-1-1)

因此我們可以將其組裝再一起寫做( ６-2‑14)，我們可以將後面的項目取代成式子( ６-2‑15)，其中$δ_k^{L − 1}$稱做在L-1層中第K個神經元的敏感度。

$\frac{\partial E}{\partial w_{\text{ki}}^{L - 1}}=a_{i}^{L - 2}f'(z_{k}^{L - 1})\sum_{j}^{}{\frac{\partial E}{\partial a_{j}^{L}}\frac{\partial a_{j}^{L}}{\partial z_{j}^{L}}}\frac{\partial z_{j}^{L}}{\partial a_{k}^{L - 1}}$( ６-2‑14)

$\frac{\partial E}{\partial w_{\text{ki}}^{L - 1}} = a_{i}^{L - 2}\delta_{k}^{L - 1}$ ( ６-2‑15)

因此$δ_k^{L − 1}$如公式( ６-2‑16)所示，我們可以將( ６-2‑9)代入公式( ６-2‑16)得到( ６-2‑17)，這是類神經中很重要的公式，代表前一層的敏感度是後面一層敏感度與權重的加總，然後再對前一層的神經元做輸出函數的微分，不論類神經模型還是深度學習模型都是靠這行重要的公式反覆的把誤差由後面往前傳做運算以求出總體誤差對權重值的偏導量，以得知權重值的改變方向而使得模型中樣本輸出與最後一層神經元輸出值的差距越來越小，進而使的模型具有擬合任意非線性方程式的意義。



$\delta_{k}^{L - 1} = f'(z_{k}^{L - 1})\sum_{j}^{}{(a_{j}^{L} - y_{j})f'(z_{j}^{L})}w_{jk}^{L}$ ( ６-2‑16)

$= f'\left( z_{k}^{L - 1} \right)\sum_{j}^{}{\delta_{j}^{L}w_{\text{jk}}^{L}}$ ( ６-2‑17)


我們接著繼續求總體誤差對偏權值的偏導項( ６-2‑18)，其中前面兩項式子( ６-2‑4) ( ６-2‑5)就已經求過，而最後一項對偏權值的微分項為1，因此可以寫成式子( ６-2‑19)，表示總體誤差對偏權值的微分剛好等於該層神經元的敏感度。

$\frac{\partial E}{\partial b_{j}^{L}} = \frac{\partial E}{\partial a_{j}^{L}}\frac{\partial a_{j}^{L}}{\partial z_{j}^{L}}\frac{\partial z_{j}^{L}}{\partial b_{j}^{L}}$ ( ６-2‑18)

$\frac{\partial E}{\partial b_{j}^{L}} = \left( a_{j}^{L} - y_{j} \right)f'\left( z_{j}^{L} \right) = \delta_{j}^{L}$ ( ６-2‑19)


自此，四大公式已全數求出，分別為如下，我將表示最後一層L的代號用任意層l取代，藉以表達出類神經模型中的通用函式:



$\delta_{j}^{l} = \frac{\partial E}{\partial a_{j}^{L}}\ f'\left( z_{j}^{l} \right)$ (Equation 1)



$\delta_{k}^{l - 1} = f'\left( z_{k}^{l - 1} \right)\sum_{j}^{}{\delta_{j}^{l}w_{\text{jk}}^{l}}$ (Equation 2)



$\frac{\partial E}{\partial w_{\text{jk}}^{l}} = a_{k}^{l - 1}\delta_{j}^{l}$ (Equation 3)



$\frac{\partial E}{\partial b_{j}^{l}} = \delta_{j}^{l}$ (Equation 4)

常見的表示式如下

![](https://i.imgur.com/qna0kTc.png)

## 七.參考資料


類神經網路與模糊控制理論 入門與應用 王進德 編著

http://neuron.csie.ntust.edu.tw/homework/93/NN/homework2/M9304302/welcome.htm

http://iamtrask.github.io/2015/07/12/basic-python-network/

https://en.wikipedia.org/wiki/Hadamard_product_(matrices)

http://neuralnetworksanddeeplearning.com/chap2.html

https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/

http://cs231n.github.io/optimization-2/