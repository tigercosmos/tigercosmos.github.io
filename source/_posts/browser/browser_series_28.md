---
title: 掩卷沈思瀏覽器
date: 2018-01-08 18:44:38
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
今天我們不談技術，來談談對瀏覽器的想法。

目前看起來瀏覽器已經是很成熟的產品了，在經歷過幾個大事件，例如 IE 幹掉 Netscape Navigator，再來就是 Chrome 一舉成為市場老大。後來就幾乎沒有什麼大事了，大家能做的就是一些優化、使用者友善、介面等等，說穿了就是沒有任何的「創舉」。例如最近 Firefox 有量子專案釋出，的確變快了，但是其實就是快得跟 Chrome 一樣，裡面用到的技術當然還是滿厲害的，例如使用平行化的技術就讓人眼睛為之一亮，但要說重大突破卻還不至於。

這邊指的突破是什麼呢。就像是 Windows 改變人類使用電腦的方式，或是 iphone 引領智慧型手機的流行。
什麼是突破？當你可以改變世界的運作方式，人們因這個產品、技術而改變生活模式，甚至潛移默化圍繞著你的東西而擺脫不了，這就是一大突破了。想想看電腦、手機，哪天沒有 3C 產品的話，現代人還活得下去嗎？

我們渴望的是在瀏覽器這個題目上能做出「創舉」，單單的「進步」不能滿足我們，每次瀏覽器大廠釋出新版本，不過就是效能進步 20、30％ 或者更些微，而近年學術論文天馬行空的點子也都屬於「進步」而已。不是說一直有進步不好，但我們渴望徹底不一樣。也許是因為我們被現有的架構所束縛，以致難以發揮，像是 Firefox 這類的瀏覽器早已是龐然大物，幾千萬行的程式碼，想改都改不了。所以後來就有一些新的瀏覽器專案誕生，也有好幾家新創公司開發新型瀏覽器，目的就是從頭開始，希望一開始在架構上就採用更新穎的技術，但開發一個瀏覽器是一個漫長的過程，新的專案剛開始一兩年可能都可以盡如人意，但一但專案發展持續到十年、二十年，又是同樣的瓶頸，我們看 Chrome 的壽命也不過十年而已。

更多時候可能是外在因素導致無法進步，可能是佔據優勢，可能是大公司包袱。Chrome 身為瀏覽器的第一巨頭，要說最有資本和能力進步的非他莫屬，但 Chrome 這幾年卻沒有再有突破，甚至效能反而慢慢下降。Chrome 最令人詬病就是很耗記憶體，我相信這絕對有辦法解決，只是願不願意投入資源、花時間。我想原因大概就是，因為 Chrome 市佔率過五成，已經是第一名了，那他再進步也只會是第一名，就算他真的變兩倍厲害，使用者恐怕也不太會有感，很多時候人們是透過比較來分出好壞。除非哪天 Firefox 徹底比 Chrome 快三倍，讓 Chrome 的消費者流失，才可能會讓 Chrome 不得不加重技術研發。還記得當年的 IE 嗎？ [Chrome 已經快成為新的「IE」了](https://www.theverge.com/2018/1/4/16805216/)，我由衷期盼有新的競爭對手直接撕破這個局面。換個說法，雖然大家還是在競爭，但有點像是烏龜們賽跑，太安逸而不刺激。

大公司也容易被包袱所限制。例如某個技術已經花了幾百萬美金投入研發，日後想丟都不容易丟掉，你能說這東西很爛我不想用嗎？開發人員只好硬著頭皮把所謂的「新技術」導入新版本當中，至於是不是真的好就不得而知。又或著，Firefox 有可能丟掉 Gecko 換成 Servo 嗎？還記得我們提到 Gecko 用 C++ 寫會有很多問題，所以才有新的瀏覽器引擎 Servo 使用 Rust 撰寫。明明知道 Gecko 有缺陷，論理而言最終該被丟掉，但卻一直花大量力氣在做維護，而 Servo 卻一直沒辦法增加研發資源，最後發展演變成 Gecko 和 Servo 漸漸融合，雖然說也不是不好，但從這點就可以看到歷史包袱絕對是一種阻礙。

後來雲端技術浮上檯面，各種 XXX as a service（例如 PaaS, IaaS）大家朗朗上口，瀏覽器又有新的趨勢是把所有東西轉移到伺服器上，讓瀏覽器變成只是個顯示介面，這麼做好處就是計算、數據都在伺服端，不用靠客戶端運算，客戶端也不會有資安問題（除非伺服端徹底淪陷）。聽起來算是一個新的發展，至於算不算突破？若是以本文的定義，徹底改變人類的生活，恐怕還沒有。但雲端服務正在快速發展，可能要未來才能見證，期待在發展過程中能看到真正的「創舉」。

講了這麼多，其實我們就是在思考，怎麼樣才能讓瀏覽器變得更好？瀏覽器太重要了，重要到大家已經視為理所當然。在這種氛圍下，除非是轟動性的改變，否則就不痛不癢。我相信絕對有可以突破的地方，現在的我們就像剛爬上一個高原，一望無際的平原近在眼前，我們不知道的是，在遙遠的盡頭還有無數的險坡等著我們攀上。而我，希望能當下一個里程碑的第一人！

---

希望有幫到大家，大家明天見！

