---
title: 用網頁相似性來優化瀏覽器
date: 2017-12-31 23:38:34
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
前兩天（[1](https://ithelp.ithome.com.tw/articles/10194936?sc=hot)＆[2](https://ithelp.ithome.com.tw/articles/10194725?sc=hot)）都找了比較有趣的論文來寫，沒意外都登上熱門了。不過是時候回來講一些比較硬的東西了！

## 論文
今天研究的論文是「 [Similarity-based Web Browser Optimization](http://wwwconference.org/proceedings/www2014/proceedings/p575.pdf) 」，顧名思義是使用網頁本身得相似性，讓瀏覽器渲染的效能可以更優化。這邊只截取重點和加入我一些心得，大家有興趣可以點連結去看原始論文。

在看本文之前，推薦大家先看一篇文章「[Browser Rendering Optimization(中文)](https://blog.techbridge.cc/2016/04/02/Browser-Rendering-Optimization/)」，這是以前端開發者角度探討如何讓網頁渲染更優化。先了解如何在前端中做優化，再來看如何以瀏覽器架構本身達到優化，相信會更有收穫！


---
## 簡介
首先我們從過去研究中知道幾件事
- CSS 和 layout 的處理佔處理頁面的 50% 左右
- 優化 javascript 的運算最多就快 7％ 左右

所以如果我們想做優化瀏覽器渲染的速度，看起來著重在 CSS 似乎影響最大！
這篇論文沿用 Zhang et.al 提倡的 Smart Caching 想法，也就是將 style 算好的結果暫存，減少之後碰到一樣的 style 還要重複計算。

可以看到像維基百科不同項目頁面，相似度就很高
![](https://user-images.githubusercontent.com/18013815/34462183-fcc89040-ee78-11e7-8e6b-77ca8e27f05c.png)

再來看看各家網站的子網頁相似度如何，包含 HTML 和 CSS
![](https://user-images.githubusercontent.com/18013815/34462196-3b305b60-ee79-11e7-9ff8-d7fb26e8353f.png)
不管是 HTML 還是 CSS 的有一定的相似度，其中 CSS 的相似度高達八成，也意味著如果能減少計算這些部分，瀏覽器速度就可以更快！

---
## 概念
所以這邊作者提倡一種「再利用」style 的方法，看概念圖不難理解
![](https://user-images.githubusercontent.com/18013815/34462233-22b9f0e0-ee7a-11e7-87a1-5bbfb6a3c423.png)

---
接下來看這張圖，是重點了！
![](https://user-images.githubusercontent.com/18013815/34462292-55f201b8-ee7b-11e7-909d-e8ed65e58501.png)
根據研究，70% 使用者進入首頁後不會再回來，因此對首頁做 cache 沒意義。但是統計顯示 60% 的瀏覽行為會開啟相似的子網頁，意思是同樣路徑下的網頁們（比方說都在 `\products\` 這個路徑下，可能就有好幾樣商品的個別網頁），有非常大的機率重複，所以我們就針對這些網頁建立一個 cache tree。還記得我們之前提到的 DOM tree、Style tree 嗎？這邊也類似，使用 `<TagName, ID, Class>` 建立樹，並直接對照 Style tree，如果發現有一樣的就可以直接提取 cache。

---
## 演算法
接著是演算法的部分了，概念是如果同目錄下有其他網頁，就可以直接採用他們的 cache，若是沒有則搜尋鄰近路徑其他網頁有沒有機會。

首先是搜尋，將所有網頁以 graph 的方式處理，就有了「網頁距離」的概念。由於最相鄰的網頁（也就是路徑接近）越容易有相似的 style，所以距離最短的也就越有可能，於是我們採用 [Breadth-first Search(BFS)](http://www.csie.ntnu.edu.tw/~u91029/Graph.html#4)來做這件事。如果當前網頁還沒建立好 style tree，就採用 BFS 找最鄰近的網頁的 style tree 來用。

再來是 style 的比對
![](https://user-images.githubusercontent.com/18013815/34462376-88c2690a-ee7d-11e7-9143-6b8401e62449.png)
我們知道 child 會繼承 parent，所以如果 parent 本身就不一樣了，也就代表 child 通通沒機會用 cache，也就是要重算。那如果 parent 一樣，則對 child 一個一個檢查。

當然也有可能會碰到不同頁面，雖然都是同個 DOM 卻個別客製化，所以每當想要重新利用 style 的時候，要先檢查 style 的內容。

---
## 成效
接著就是看有沒有效了:
這張柱狀圖顯示有沒有採用這個方法前後所需要的時間，有明顯地縮短時間！
![](https://user-images.githubusercontent.com/18013815/34462515-98e6e7a4-ee80-11e7-9458-2d2006193fc8.png)
這張表格顯示這個方法減少的「重複運算」的比例，也就是先前提到一樣的 style 不需要再算一次，可以發現減少不少比例，特別是重複「繁雜」CSS 的時候效果最顯著！
![](https://user-images.githubusercontent.com/18013815/34462517-99ae67b6-ee80-11e7-9f86-a93bdf3cee59.png)

---
## 心得
這篇論文看下來似乎覺得很厲害，的確他在某些網站上達到很好的效果。但做研究時我們要知道沒有絕對的好，也沒有絕對的壞。以這篇論文來說，可以肯定他在「靜態」以及有相似「模板」的網站上處理效果很不錯，但如果是「動態」的網站呢？恐怕 cache 的效益就很小了，因為大多數東西都是 JS 算出來的。此外如果是非常客製化的網站（每個 DOM 都獨一無二），效果一樣也不顯著。

這時候我們就要取捨，如果有效那事先執行優化就很有幫助，但如果碰到此方法沒效的網站，那只是徒勞無功浪費計算而已。這篇論文是 2014 年的，其實我滿好奇最新的瀏覽器有沒有採用類似這篇論文的方法做優化？我想，如果調查顯示大多數網站都是靜態、模板的話，那就很有理由把這個優化方法採納進來！

後記：
同樣概念下的延伸想法
- 利用網頁相似性來事先檢查快取有沒有過期（大量減少 RTT）
- 利用網頁相似性事先進行預快取（我記得 Chrome 似乎有這樣做）

---
希望對大家有幫助，我們明天見！
                                                        
