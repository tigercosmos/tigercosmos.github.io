---
title: <論文> 網頁瀏覽器在異質運算多核心處理器平台上電量管理的工作量描述
date: 2018-04-10 22:56:34
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
最近又看了一篇論文，覺得寫得很精彩所以決定來分享一下

- 原文標題：Web browser workload characterization for power management on HMP platforms
- 作者： Nadja Peters(1), Sangyoung Park(1), Samarjit Chakraborty(1), Benedikt Meurer(2), Hannes Payer(2), Daniel Clifford(2). (1)Technical University of Munich, (2)Google Inc
- 發表： Hardware/Software Codesign and System Synthesis (CODES+ISSS), 2016 International Conference on

---

## 簡介
這篇論文在研究 Google 的 Chrome 瀏覽器在異質運算多核心處理器（heterogeneous multi-processing, HMP），或是所謂 [big.LITTLE](https://zh.wikipedia.org/wiki/Big.LITTLE) 架構的情況下，處理器使用方式對於瀏覽器的效能以及耗電有怎樣的影響。

big.LITTLE 是 ARM 提出的處理器架構，也就是由幾個「高效能」處理器搭配幾個「低功耗」處理器，所組成的處理器叢集。至於所謂異質運算多核心處理器，節錄自 Wiki：
> 異質多處理（heterogeneous multi-processing，HMP）是big.LITTLE組態中最靈活也是效能最強勁的使用模式，在這種組態中，同一時間點上所有的物理CPU核心都是可用的並且可以同時全部開啟使用，也可以將高效能CPU核心全數關閉而只使用低功耗CPU核心。高優先級或者對運算速度吃重的執行緒可以被分派至高效能CPU核心上，而低優先級或對運算速度要求不高的執行緒（如背景任務），則是由低功耗CPU核心負責完成。

而作者發現處理器預設的 schedulers 對於 CPU 的控制過於簡單，所以提出三種構想並加以實驗。
- 控制處理器執行數量（Constraints for Core Allocation）
- 電源門控功耗設計（Power Gating）
- 動態調整電壓和頻率（dynamic voltage and frequency scaling, DVFS）

以上幾個專有名詞後面還會用到。

簡單來說如果想要最高效能的話，把 CPU 從級的所有核心都全開效能一定最好，但如果想要達到效能與功耗的最佳平衡，這三種方法都值得考慮，因為都能做到降低效能，卻省下功耗。那接著就是看，我們要怎麼樣取捨，也許是看「節省功耗的比例」與「變差效能的比例」的比值，哪一個方法讓比值最高，意味著省比較多電，卻犧牲比較少效能。但如何抉擇沒有絕對，重點是我們注意到在考慮效能與功耗平衡的情況下，處理器本身的控制還有進步空間。

## 瀏覽器架構
在本系列討論瀏覽器架構已經是老生常談了
![瀏覽器架構](https://user-images.githubusercontent.com/18013815/38518906-d3f81bf4-3c70-11e8-8824-15da5b480f5b.png)
作者在這邊提到說，開啟網站的過程中，70％消耗的功來自於網頁渲染，其中又有60％來自於 JS 運算的消耗。

## 實驗器材
Samsung Galaxy S5 手機的 Odroid-XU3 board，特色是有 Exynos5422 系統單晶片（SoC）。其中的異質處理器晶片 (heterogeneous multiprocessor system-on-chip) 也是照著 ARM 的 big.LITTLE 架構設計。所以叢集共有 4 個功耗優化 Cortex-A7 處理器和 4 個效能優化的 Cortex-A15 處理器。

瀏覽器則是用 Chrome 的精簡版，Content Shell。

## HMP 平台電源控制
![A7-A15架構](https://user-images.githubusercontent.com/18013815/38518804-8f3d27c0-3c70-11e8-9b34-b76855d4cd5e.png)
Android 本身是基於 Linux 核心，其中控制 CPU 的部分有三個，(1) the scheduler (2) the frequency governor (3) the wakelock mechanism。scheduler 是用來分配工作給核心，governor 負責控制頻率，通常 linux 都是採用 ondemand 和 interactive，其中 interactive governor 是特地設計給行動裝置的。而 wakelock 是 Android 特有的，負責讓執行中的程式一直處於「醒著」狀態。

![ebay 結果，採用原設定](https://user-images.githubusercontent.com/18013815/38519534-b4aeee56-3c72-11e8-94ac-6d0e23fb6b4e.png)
圖四是採用 Android 原生設定，去瀏覽 ebay 的結果。我們看到幾個問題：
1. 前兩秒 A15 都沒被使用，頻率卻衝到最高
2. 後來 CPU 使用率低於 100%，代表單一核心就夠了，但 CPU 仍維持高頻率
3. 就算 A15 沒被使用，依舊維持 50% 的頻率

從以上幾點，我們可以改進很多地方，例如第一點可以透過動態電壓時脈（DVFS）改善，第二點可以透過限制核心來辦到，第三點可以用電源門控功耗設計來改善。

## 檢測機制
![Exynos5422-based measurement setup](https://user-images.githubusercontent.com/18013815/38532455-82643430-3ca7-11e8-808c-2ccf1ab3e3a6.png)
在 CPU 前面有 Shunt 是電阻 和 INA231 電壓電流感測器。
![Software setup for data acquirement](https://user-images.githubusercontent.com/18013815/38532452-81ecbcfc-3ca7-11e8-9a70-e078ade49c11.png)
藉由功耗紀錄、工作排程紀錄、瀏覽器堆疊紀錄，可以分析瀏覽網站的功耗

## 瀏覽器執行緒
![Relative CPU time of web browser threads for representative websites per A15 and A7 cluster](https://user-images.githubusercontent.com/18013815/38533062-271ba22c-3caa-11e8-8bfc-205eb804df4d.png)
從圖 7 和 8 可以發現，瀏覽器在渲染的時候，CrRendererMain（渲染主程式） 和 CompositorTileW（處理合成）佔了大部分的消耗，而又這兩個程序只要又是以 A15 來處理，幾乎是 80-90% 的工作量。

![Figure 9: Relative energy distribution of the web page com- ponents HTML, CSS and JavaScript.](https://user-images.githubusercontent.com/18013815/38535603-d8dec65e-3cb6-11e8-8ef0-4a435c5e878d.png)
![Figure 10: Relative time distribution of V8-related function calls by category.](https://user-images.githubusercontent.com/18013815/38535720-7aa49d7e-3cb7-11e8-8717-d2692c7bca58.png)
從圖 9 和 10 ，V8 花了 40%在解析，50% 在執行。又發現 V8 在主渲染執行緒花了 83-96%，但只有 1-13% 的執行緒時間是用在 ScriptStreamerThread（解析JS）。意味著也許我們可以把解析的部份交給 A7 處理，也就是不怎花資源的部份交給功耗優化的處理器負責，這樣會更省功耗！

## 實驗囉！

### 限制效能分析（Power-Performance Trade-off Analysis）
直接限制 A15 可以用的最高時脈
![figure 11 12](https://user-images.githubusercontent.com/18013815/38539109-4ad61548-3cc9-11e8-82a7-9f81e7ae3426.png)
eBay 的例子中，將最高時脈限制在 1.2GHz，消耗的功減少 34.6% ，但處理時間只增加 16.7% (0.6 s)
其他網站也都差不多，簡單來說就是效能換取時間。這個方法與是否為異質處理器無關，就算是單核心也會是一樣的結果，滿直觀的結果。

### 限制使用核心（Constraints for Core Allocation）
在剛剛討論瀏覽器執行緒的時候，我們知道把工作分一些給效能導向的處理器是比較有效率的。
測試三種模式，限制可以用的處理器核心數：
1. 4 個 A7 + 4 個 A15
2. 4 個 A7 + 1 個 A15
3. 4 個 A7
![figure13](https://user-images.githubusercontent.com/18013815/38562563-75b2ee28-3d0d-11e8-872f-3a6ed9f2bc53.png)
在 eBay 的例子中，第一種（全開）跟第二種（半開）相比，半開能量省了 13%，執行時間只多了 5%。這樣的交換其實滿值得的！
![figure14](https://user-images.githubusercontent.com/18013815/38562751-dc7dcccc-3d0d-11e8-9d2d-c71a9c7d7d30.png)
但在 Wikipedia 的情況下，第一種和第二種效能和功耗則幾乎沒改變。但這也說明了，多數時候我們其實可以選擇半開就好，最壞結果就是沒變，比較好結果就是犧牲一點點時間換取更多的能量。

至於第三種，只使用 A7 情況下，執行時間幾乎是兩倍，但省電量卻很可觀，因為本身就是功耗優化導向。
詳細比較可以看這張表：
![比較](https://user-images.githubusercontent.com/18013815/38563072-9a17a5dc-3d0e-11e8-8685-1356404ee9e2.png)

### 採用動態時脈電壓（Power Savings by DVFS without Perfor- mance Compromise）
oracle predictor 是以上帝視角來看，假設我們都知道怎樣做最好了。他建立一個模型讓我們在動態調整時脈和電壓的過程中，可以讓效能幾乎沒有改變，也就是最優化所需的時脈電壓。

透過以下模型預測所需的功率，參數解釋也在圖中：
![方程式](https://user-images.githubusercontent.com/18013815/38563769-3a17b486-3d10-11e8-930e-a7188a5d33a1.png)

從下圖中可以看到，黑線為理論預測，灰線為實際實驗，採用模型時，明顯可以減少功耗消耗。
這邊也代表理論上能達到的最佳值，不管怎樣優化，即便是上帝也只能做到這樣好而已。
![理論比較](https://user-images.githubusercontent.com/18013815/38563848-75874a2c-3d10-11e8-89d7-7e6217e671d3.png)

### 前階段電門控制（Post-Loading Phase Power Gating）
在一開始我們討論到，一開始最初的時候 A15 並沒有做事，卻維持高頻率。
所以作者讓電門關閉 A15 直到 A7 使用率達到 110% 再開啟。（選擇 110% 是因為前階段處理幾乎都是 A7 單核心執行）
比較後發現，約莫可以省下 10% 的能源。

## 結論
瀏覽器處理過程中，有很多階段，藉由巧妙控制異質處理器的使用，可以在比火力全開下只稍微慢一點，卻省下更多電量。而這樣的做法同樣也可以用在遊戲之類的應用軟體上，也是由許多不同階段處理程序組成。

最後除了作者實驗用的三星手機之外，Apple 的 iPhone 現在也都是採用 big.LITTLE 了，而目前手機都是採用預設的最簡單控制模型，一個穩定優秀的新模型，可以讓手機採用更節能又有效率的使用體驗。使用者甚至可以自由決定是否要用「火力全開」模式，或是用「最佳平衡」模式。

