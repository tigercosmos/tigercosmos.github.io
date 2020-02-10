---
title: <論文> Servo 案例分析：平行化瀏覽器效能-能源的預測模型
date: 2018-01-19 17:49:09
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
今日論文：[Parallel Performance-Energy Predictive Modeling of Browsers: Case Study of Servo](http://ieeexplore.ieee.org/document/7839666/)
發表： High Performance Computing (HiPC), 2016 IEEE 23rd International Conference
作者： Rohit Zambre(CA)、Lars Bergstrom(Mozilla)、Laleh Aghababaie Beni(CA)

> 本文圖片來自原始論文

---
[本系列](https://ithelp.ithome.com.tw/users/20103745/ironman/1270)有介紹過 Servo，是一個平行化的瀏覽器引擎。而這篇論文第二作者是之前 Servo 團隊的主管。

平行化處理不一定每次都比較快。有時候，與其分散給四個執行緒跑，不如讓單一執行緒時脈衝高，可能處理得更快，也就是說，不是每次都採用平行化就是最好的。而今天我們既然想要做一個更快的引擎，當然就不能反而被「平行化」而扯後腿，所以這篇在研究如何建立一個模型，讓我們在處理網站的時候，能決定要用幾個執行緒，來達到最佳效能。

---
例如我們看這張圖，顯示不同模型下的結果：
![](https://user-images.githubusercontent.com/18013815/35107469-f7c35d46-fcab-11e7-8751-0560ae75c7fb.png)
其中 `Servo` 標籤是 Servo 預設執行情況，通常會是四執行緒。而 `Best` 是試試看 1, 2, 4執行緒，得到最好效能的那次。而 `Our` model 則是這篇論文用機器學習方式推得出來該用幾個執行緒得到的結果。

可以發現，假設這個網站其實用 1 執行緒比較好，但 Servo 預設是全開，那反而就慢了。而這篇論文預測的準度也還算不錯，看圖大致上 `Our` 都有吻合 `Best`。

---
既然談到機器學習，就要選一些特徵值，這邊作者採用 DOM tree 的一些數據來當特徵。
這張圖視覺化一棵 DOM tree 的樣子，順帶一提用的工具是 [treeify](https://chikeichan.wordpress.com/2014/12/23/treeify-visualizing-dom-tree/)，大家可以玩玩看
![](https://user-images.githubusercontent.com/18013815/35138533-f388b216-fd29-11e7-9ee9-69a019544581.png)
最後作者挑出以下九點當特徵值，不過後來有兩個發現沒啥用：
1. DOM tree 的 node 總數（DOM 尺寸）
2. HTML tag 用 attributes 的數量
3. 網頁的 bytes 大小
4. DOM tree 有幾層（深度）
5. DOM tree 的葉子數量
6. 每層有多少 node 的平均值 (avg-tree-width)
7. 每層有多少 node 的最大值 (max-tree-width)
8. max-tree-width 和 average-tree-width 的比值(max-avg-width-ratio)
9. DOM-size 和 tree-depth 的比值(avg-work-per-level)


這邊可以看下一些網站 tree 深度和廣度的關係：
![](https://user-images.githubusercontent.com/18013815/35139483-4e5cc3ae-fd2e-11e7-81ff-1e52fb24c945.png)

而事實上我們可以猜測說，avg-tree-width 和 avg-work-per-level 越大，平行化效果越好，其實滿好想的，就是事情越多越多人做越容易，但事情很少分給很多人就是雞肋。所以從上圖（圖3）我們可以發現 Facebook 普遍寬度很小，avg-tree-width 和 avg-work-per-level 也就當然都比較小，實驗也證明在 Facebook 上用平行化效果不佳。

---
接著來談三種 cost model：
- 效能：平行化帶來的進步
- 能源：平行化帶來的能源消耗
- 效能與能源：兩者皆考慮

這張圖顯示，處理 Styling 和 Layout 花的比例：
![](https://user-images.githubusercontent.com/18013815/35141500-0e5dbe9a-fd36-11e7-8146-b4c797491d82.png)
可以發現 Layout 真的很少，也因為工作量少，實驗後這部分拿去平行化效果也不佳

接著就來做實驗了。首先是效能模型，實驗方法很簡單，將所有要測試的網頁，都分別用 1, 2, 4 執行緒都跑跑看，看採用幾個執行緒處理速度比較快，就標上最佳的那個數字，當做他在效能模型上的標籤。換句話說，就是看那個網頁該用幾個執行緒最好。實驗後發現標籤 1, 2 和 4 分別為 299 (55.88%), 49 (9.15%) 和 187 (34.95%)。

能源模型應該也很有趣，剛剛是考慮處理速度變快，改成消耗能源就好。不過作者沒有針對這部份做測試，只有提出來而已。但是能源對手機瀏覽器應該就很重要了，以後可以做做看。

接著是效能能源模型，兩著接考慮的情況下，我們以能源不超過某個上限的情況下，決定效能最佳的那個。當全部不符合的時候，就認定執行緒1為最佳。最後結論是標籤 1, 2 和 4 分別為 317 (59.25%), 50 (9.34%) 和 168 (31.40%)。

---
接著來看特徵值和效能(p)、能源(e)的關聯（p2 是效能模型 2 執行緒的意思，以此類推）：
![](https://user-images.githubusercontent.com/18013815/35143636-22395076-fd3d-11e7-990f-a8a2c09f6bc8.png)
然後發現  tree-depth 和 max-avg-width-ratio 幾乎沒影響，相關係數不足 0.1，所以就被排除掉。

接著用 90-10% 資料-測試的比例，將測資分成十組，每組約55個樣本，然後用三種機器學習的模型來測：
- MNR： 在 90-10% 訓練測試的交叉驗證下，平均和最大的正確率為 72.22% 和 87.27%。
- emsmeble：AdaBoostM2＋決策樹搭配 surrogate splits，平均和最大的正確率為 69.44% 和 85.45%。
- 神經網路：80-10-10％ 訓練-驗證-測試下，測資正確率為 77.8%。

正確率看起來有點低啦，不過這篇論文本來就不是一篇「機器學習」的論文，所以情有可原。

---
不過即使機器學習的效果沒有到非常好，但是拿 MNR 的結果來和原本的 Servo 比起來，最多可以省到 94% 的效能，例如 "indeed.com" 原本 Servo 預設用 4 執行緒要跑 45ms，但其實用 1 執行緒只要 2.48 ms，甚至消耗的能量也少了一半。

總之這篇論文最有趣的地方就是，用機器學習來判斷說，現在瀏覽的這個網站該採用幾個執行緒來處理比較好。看完這篇有給我一點啟發，如果將類似的概念套入快取的處理上呢？


> 延伸閱讀：[Fine-grained timing and energy profiling in Servo](https://blog.servo.org/2015/09/11/timing-energy/)

