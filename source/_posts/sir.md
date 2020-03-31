---
title: 傳染病 SIR 模型與機率模型介紹與簡易模擬
date: 2020-03-31 11:07:00
tags: [傳染病, 程式, python, SIR, 模擬, 機率]
---

## 1. 簡介

最近武漢肺炎人心惶惶，有台大教授發表化學動力論來模擬傳染變化，而其實我高中時也做過類似的事，就是我的「[傳染病之數學模型與個體導向模擬](/post/2015/07/infectious-disease/)」科展。啟發於科學人雜誌《虛擬城市：天花來了》，文中藉由科學模擬來進行流行病預測與防治，我覺得十分有趣，那陣子對伊波拉病毒想深入研究加上也覺得寫程式好玩，因此就做了那個科展，本篇大致將我高中時的科展報告重新整理。

本文介紹 SIR 模型來做大尺度傳染病預測，同時也用機率函數來做個體導向的微觀尺度模擬，用兩種方式來模擬傳染病的擴散狀況。

公共衛生對傳染病研究有很多理論模型，其中隔間模型（Compartmental Model）藉由假設整個人口被區分成幾個群體，並且在同一群體中所有個體皆有一樣的特性，藉由這幾個假設可以簡化傳染病的社學模型。

在隔間模型中，易感受-感染者-康復者模型（SIR Model）是指由人口由易感受族群（Susceptible, $S$）、已感染族群（Infectious, $I$）、已康復族群（Recovered, $R$）三個部分組成的傳染病模型。模型假設傳染病可以藉由直接接觸傳染，並且每個人會隨機接觸其他人。模型中有兩個重要參數，分別是感染族群傳染給健康族群的傳染力（transmission rate）$β$，以及感染族群恢復的康復力（rate of recovered） $γ$。

機率模型則是本文藉由分布函數去模擬個體互動是否造成感染的簡易模型。
<!-- more --> 

## 2. 數學定義

接著對封閉族群下之易感受-感染者-康復者模型（closed SIR model)來作探討，因為短時間傳染的影響大於人口流動的影響，因此封閉模型指排除人口變化的因素，根據這條件下，我們定義：

### 2.1 SIR 模型定義

易感染者 $S$ 隨時間 $t$ 變化： 
$$\frac{dS}{dt} = - \frac{βIS}{N}$$

已感染者 $I$ 隨時間 $t$ 變化：
$$\frac{dI}{dt} = \frac{βIS}{N} - 𝛾I$$

康復者 $R$ 隨時間 $t$ 變化：
$$\frac{dR}{dt} = 𝛾I$$

其中參數 $β$ 為傳染力，$γ$ 為康復力。


在總人口數為 $N$ 又滿足：
$$\frac{dS}{dt} + \frac{dI}{dt} + \frac{dR}{dt} = 0$$
$$ S(t) + T(t) + R(t) = N$$

### 2.2 基本傳染數 $R_0$

在 SIR 模型中有提到傳染力 $β$ 和康復力 $γ$，這時我們要來定義這兩個參數。同時需要介紹基本傳染數。

基本傳染數（basic reproduction number, $R_0$）是在傳染病學上，指在沒有外力介入，同時所有人都沒有免疫力的情況下，一個感染到某種傳染病的人，會把疾病傳染給其他多少個人的平均數。基本傳染數通常被寫成為 $R_0$。$R_0$ 的數字愈大，該傳染病在傳播初期的爆發潛力越強。

根據 [Wikipedia: Basic Reproduction Number](https://en.wikipedia.org/wiki/Basic_reproduction_number) 數據，SARS 的 $R_0$ 約為 2~5，最近大爆發的武漢肺炎 COVID-19 大約在 1.4~3.9。

$R_0$ 的定義如下：

$$R_0 = 𝜏 × 𝑐̅ × d = \frac{β}{𝛾}$$

其中 $𝜏$ 為每單位十間的接觸量，$𝑐̅$ 為每次接觸傳染的機率，$d$ 為感染的時間。

又定義

$$β = 𝜏 × 𝑐̅$$
$$γ = d^{-1}$$


根據 SIR 模型，當 $\frac{dI}{dt} > 0$ 時，傳染病會蔓延，意味著：

$$\frac{βIS}{N} -  𝛾I > 0$$
$$\frac{βIS}{N} > 𝛾I$$

因為 $S ≅ N$、$I=1$ 且 $β = 𝜏 × 𝑐̅$ 、 $𝛾 = 𝑑^{-1}$ 代回 $𝜏 × 𝑐̅ × d$，因此：

$$\frac{β}{𝛾} = R_0 > 1$$

### 2.3 指數分布（Exponential Distribution）

數學上指數分布是一種連續機率分布。指數分布可以用來表示獨立隨機事件發生的時間間隔，遊客進入旅館的時間間隔、收到信件的時間間隔，抑或是一個人得到傳染病的時間間隔。

指數分布的機率密度函數定義如下。

當 $ x>= 0 $ 時：
$$ f(x; \lambda) = 1 - e ^ {- \lambda x}$$
當 $ x= 0 $ 時：
$$ f(x; \lambda) = 0$$

其中 $λ> 0$ 是分布的一個參數，常被稱為率參數（rate parameter）即每單位時間發生該事件的次數。指數分布的區間 $[0,∞)$。此分佈意在於抽取一個平均發生速率為 $λ$ 的事件之發生時間。

## 3 程式模擬

### 3.1 巨觀模擬

直接使用 `2.1` 節介紹的 SIR 數學模型來做巨觀的模擬計算。

模擬是根據時間變換 $dt$ 來進行，$dt$ 可以想成就是一回合，在這回合 $dS$、$dR$、$dI$ 都會有變化，再把變化加進 $S$、$I$、$R$。

```
def SIR(S, I, R):

    # 計算變化
    dS = - Beta * S *  I/ N
    dR = Gamma * I
    dI = - dS - dR
    
    # 把變化加回去
    s = S + dS
    i = I + dI
    r = R + dR
    
    # 邊界檢查
    if (s < 0):
        s = 0
    if (i > N): 
        i = N
    if (r > N):
        r = N

    return s, i, r
```

完整包含畫圖的 Python 程式碼可以在[這邊下載](https://gist.github.com/tigercosmos/9f0251283bda230aafe8582305cc71f1)，可以親自跑跑看。

下圖為模擬天數 20 天，$\beta$ 為 1，$\gamma$ 為 0.5，總數 2000 人一開始有 10 人感染。

![sir plot](https://user-images.githubusercontent.com/18013815/78059251-1ca76600-73bc-11ea-8f2e-ee08af9d526a.png)

### 3.2 微觀模擬

我們也可以用個體模擬的方式，就是設定很多物件，讓他們彼此接觸，然後再統計每次互動的結果。在本例中，就是很多人去跟其他人互動，看會不會被傳染。

首先我們定義人：

```python
class Person:
    def __init__(self, id, state):
        self.id = id
        self.state = state

    def step(self, people, dt=1):
        if self.state == State.SUS:
            new_beta = 0

            # 假設和所有人都碰過, people 是所有人的 List
            for person in people:
                if person.state == State.INF:
                    new_beta += Beta

            if InfectiousEvent(new_beta, dt):
                self.state = State.INF

        elif self.state == State.INF:
            if RecoveredEvent(Gamma, dt):
                self.state = State.RECV
```

我們剛剛說到 $\beta$ 是感染力，所以當某個人碰到越多已經感染的人，感染力也就會越強，這邊是直接以相加的方式做處理。

`step()` 就是每一回合和所有人接觸會怎樣，如果這個人是健康的（`State.SUS`）的話，就讓他和其他人互動，並算出最後的感染力，並算出會感染的機率。如果這個人已經被感染（`State.INF`），那就算她康復的機率。如果這人已經康復（`State.RECV`），在此模型中康復者不會復發，因此不處理。

注意到這邊有很特別的 `InfectiousEvent()` 和 `RecoveredEvent()` 函數，這兩個是機率函數，也就是 `2.3` 介紹的分布函數。

還記得分布函數定義是 $ f(x; \lambda) = 1 - e ^ {- \lambda x}$ 嗎？其 inverse 為分位數函數，會得到 $x$ 的分布位置。我們算出 $x$ 位置後，可以和一個閾值做比較，除果小於閾值就當做事件會觸發。

```py
# 感染的事件
def InfectiousEvent(rate, dt):
    try:
        return -log(random()) / rate*k < dt
    except ZeroDivisionError:
        return 0

# 恢復的事件
def RecoveredEvent(rate, dt):
    try:
        return -log(random()) / rate*h < dt
    except ZeroDivisionError:
        return 0
```

根據此函數定義，傳入的 `rate` 越大時，事件越容易發生，藉由亂數來決定此事是否在分布函數中達到「發生」，也就是要不要被感染或者康復，其中的 `h` 和 `k` 是用來調整倍率的參數。

完整包含畫圖的 Python 程式碼可以在[這邊下載](https://gist.github.com/tigercosmos/050bc988ba1be3279a1733d94540b686)，可以親自跑跑看。

下圖為模擬天數 20 天，$\beta$ 為 1，$\gamma$ 為 0.5，總數 2000 人一開始有 10 人感染。同樣參數下，想讓微觀模擬的圖和巨觀的圖一樣的話，就需要去調整 `h` 和 `k`。

![agent based SIR model](https://user-images.githubusercontent.com/18013815/78068560-2e443a00-73cb-11ea-9d94-795d43b947dc.png)

### 3.3 微觀和巨觀的比較

巨觀模擬可以很快算出答案，但是彈性很低，必須假設所有人都是一樣。相反的，透過微觀模擬，我們可以很細緻調整每個個體的參數，比方說在團體裡面加入年輕人和老人，年輕人比較容易康復，老人比較容易感染。或是模擬在一間學校，人群就有接觸的分群，像是同間教室比較會接觸，同個社團比較會接觸。微觀模擬可以做到非常客製化的各種情境假設。

## 4 結論

SIR 模型或機率模型都只是一種簡化假設模型，他們可能可以解釋某個傳染病的擴散，也可能無法解釋。每個模型都有適合的時空背景，例如人口是否封閉，是否可以透過家禽傳染，是否有實施居家隔離政策等等。我們可以藉由建立符合當下背景的模型，透過模擬結果一窺傳染病的影響，例如是否會造成大流行，藉此做到公共衛生預防和因應。


