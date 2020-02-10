---
title: 站在巨人的肩膀上，一覽瀏覽器引擎研究
date: 2017-12-20 22:08:08
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


## 瀏覽器相關研究

今天來談談瀏覽器的學術研究，提供大家一些論文參考。

```
「
    如果說我能看的更遠一些，那是因為我站在巨人的肩膀上。
                                                    」 -- 牛頓
```

科技的日新月異，是由無數人共同努力的心血，我們現在享受方便的資訊服務，都是由前人一點一滴研究出來，再由更多人將研究再研究，才達到至今我們所看到的頂尖技術。

瀏覽器如何不是如此，從 IE、Chrome、Firefox 等等瀏覽器中我們可以看到不斷進步的腳印，至今 Firefox 推出「Firefox Quantum」挑戰群雄再戰最高點，背後就是由一堆研究人員不斷尋找新的方法、理論、技術來突破現狀。Chrome 的開發人員絕對不會坐以待斃，不久一定會推出能擠下 Firefox 的新版本，而我們則是在這良性競爭下的最大受益者。瀏覽網站飆高速，就像是開賽車一樣爽！

有關於瀏覽器的相關研究真的很少，一般發 paper 都是大學、研究單位，但這些地方幾乎沒人做這方面研究。像我想在台大找教授研究瀏覽器，看了一下資工系的教授背景，頂多「軟體架構設計」這個研究領域比較接近一點了。瀏覽器研究完全不是顯學，機器學習、視覺辨識這方面反而一堆。多數的技術都是由瀏覽器的開發人員自己設計出來，卻也不會去發 paper。我自己認為比較可惜，雖然現在都開源了，但如果沒有文章特別去解釋技術，恐怕別人也很難去學習。



## 瀏覽器的並行/平行化

*   [Engineering the Servo Web Browser Engine using Rust](https://raw.githubusercontent.com/larsbergstrom/papers/master/icse16-servo-preprint.pdf)
*   [Experience Report: Developing the Servo Web Browser Engine using Rust](http://arxiv.org/abs/1505.07383)
*   [ZOOMM: A Parallel Web Browser Engine for Multicore Mobile Devices](http://www.tinmith.net/papers/cascaval-ppopp-2013.pdf)
*   [A Case for Parallelizing Web Pages](https://www.usenix.org/system/files/conference/hotpar12/hotpar12-final58.pdf)
*   [The Multi-Principal OS Construction of the Gazelle Web Browser](http://research.microsoft.com/pubs/79655/gazelle.pdf)

## 瀏覽器工作的平行化

*   [Parallel JavaScript Execution in Web Navigation Sequences](http://ieeexplore.ieee.org/xpl/articleDetails.jsp?arnumber=7396817)
*   [HPar: A practical parallel parser for HTML--taming HTML complexities for parallel parsing](http://dl.acm.org/citation.cfm?id=2555301)
*   [Fast and Parallel Webpage Layout](https://lmeyerov.github.io/projects/pbrowser/pubfiles/paper.pdf)
*   [Towards Parallelizing the Layout Engine of Firefox](https://www.usenix.org/legacy/event/hotpar10/tech/full_papers/Badea.pdf)


## 瀏覽器工作的分析與建模

*   [An In-depth Study of Mobile Browser Performance](http://dl.acm.org/citation.cfm?id=2883014)
*   [Energy consumption and privacy in mobile Web browsing: Individual issues and connected solutions](http://www.sciencedirect.com/science/article/pii/S2210537916000081)
*   [Concurrency in Mobile Browser Engines](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=7140678)
*   [Exploiting Webpage Characteristics for Energy-Efficient Mobile Web Browsing](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=6327179)
*   [WebCore: Architectural Support for Mobile Web Browsing](http://www.yuhaozhu.com/pubs/isca14.pdf)
*   [Demystifying Page Load Performance with WProf](https://www3.cs.stonybrook.edu/%7Earunab/papers/wprof.pdf)
*   [High-Performance and Energy-Efficient Mobile Web Browsing on Big/Little Systems](http://3nity.io/%7Evj/downloads/publications/zhu10hpca.pdf)
*   [A study of performance variations in the Mozilla Firefox web browser](http://delivery.acm.org/10.1145/2530000/2525402/p3-larres.pdf?ip=169.234.217.188&id=2525402&acc=PUBLIC&key=CA367851C7E3CE77%2EE385B6E260950907%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&CFID=804568850&CFTOKEN=79805568&__acm__=1466664534_ac8d7658ff673120270c10e7287b5e46)
*   [Who killed my battery?: Analyzing Mobile Browser Energy Consumption](https://crypto.stanford.edu/~dabo/pubs/papers/browserpower.pdf)
*   [Why are Web Browers Slow on Smartphones?](http://dl.acm.org/citation.cfm?id=2184508)
*   [A Limit Study of JavaScript Parallelism](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=5649419)

## 改善瀏覽器的效率

*   [Polaris: Faster Page Loads Using Fine-grained Dependency Tracking](http://web.mit.edu/ravinet/www/polaris_nsdi16.pdf)
*   [Energy-Aware Web Browsing on Smartphones](http://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6776557)
*   [Similarity-based web browser optimization](http://delivery.acm.org/10.1145/2570000/2567971/p575-wang.pdf?ip=169.234.217.188&id=2567971&acc=ACTIVE%20SERVICE&key=CA367851C7E3CE77%2EE385B6E260950907%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&CFID=804568850&CFTOKEN=79805568&__acm__=1466664056_0298e63e62dbf74a962413739f521a82)
*   [Mobile Web Browser Optimizations in the Cloud Era: A Survey](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=6525571&tag=1)
*   [GPU acceleration for the web browser based evolutionary computing system](http://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6689051)
*   [Smart Caching for Web Browsers](http://delivery.acm.org/10.1145/1780000/1772741/p491-zhang.pdf?ip=169.234.16.99&id=1772741&acc=ACTIVE%20SERVICE&key=CA367851C7E3CE77%2EE385B6E260950907%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&CFID=773108184&CFTOKEN=96473062&__acm__=1461092571_faf3749e491f2a63796ae5bf811efc79)


## 一些文件

*   [Towards parallelizing the layout engine of firefox](https://www.usenix.org/legacy/event/hotpar10/tech/slides/badea.pdf)
*   [Parallelizing the web browser](http://lmeyerov.github.io/projects/pbrowser/hotpar09/paper.pdf)
*   [Rethinking Browser Performance](http://lmeyerov.github.io/projects/pbrowser/pubfiles/login.pdf)
*   [Parallel Webpage Layout](http://parlab.eecs.berkeley.edu/sites/all/parlab/files/playout.pdf)

---
以上的資料很多，全部都看要花不少時間，但也代表網路的世界很寬闊。
如果你看完有心得歡迎與我分享！
更歡迎你一起投入瀏覽器的研究！

希望對大家有幫助，我們明天見！
                                                        
