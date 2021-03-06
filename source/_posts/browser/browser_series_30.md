---
title: 手機上網好耗電，不如讓雲端幫手機省電吧！
date: 2018-01-10 23:47:50
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)

## 前言
今日論文：[Decision to offload the task to Cloud for increasing energy efficiency 
of Mobile Phones](https://irjet.net/archives/V4/i1/IRJET-V4I1133.pdf)

大家是否碰過一個情況，早上搭捷運在車上滑 instagram、facebook，再看一下幾個 youtube 影片，到公司的時候已經花掉 10% 的電量了，覺得還好嗎？上班過程再分心滑一下手機，中午休息時間再玩個遊戲，才不到下午，手機電量只剩下 50％下了。喔沒關係！反正我有帶行動充啊～但這就很詭異了，手機設計那麼輕薄，結果最後大家都在外接一個笨重的行動充？

好的，所以我們該怎麼解決「我就是不想帶行動充」的情況呢？絕對不是多買一顆電池。我們分析以上的活動，看照片、上網、看影片，假設我們都是經由瀏覽器來做這些事情好了，這時候瀏覽器又成為關鍵了！

## 雲運算
事實上瀏覽器可以不要那麼耗電的方式也有很多種，可以在瀏覽器架構上做優化，我們已經談了很多了！所以今天換口味，來討論雲運算（Offload）可以怎樣幫手機省電。

基本上分三種：
- `手機 <-> proxy <-> web`：手機發送請求，再由 proxy 對 web 請求，web 回傳給 proxy，這時候 proxy 可以做運算處理，讚回傳給手機。
- `手機 ->  web -> （local server <-> 手機）`：手機傳送要求給網站，網站回傳東西給手機，但手機旁邊有個高性能的伺服器與他區域連線，這時候手機把繁重的雲算丟給區域伺服器算，在取得最後結果。
- `手機 -> web -> cloud`：手機對網站做請求，但這請求可能是做運算、儲存資料，那麼網站直接在雲端把這些事情處理完，不需要再經過手機。（比方說從Ａ下載檔案，轉檔之後上傳到B)

今天我們挑第三種來講。

---
## 數學模型
為了先說服大家，論文中就用數學表示給大家看。
```sh
假設單件工作有 I 份量
伺服器運算速度 Sc
手機運算速度 Sm
所以
手機花費： I/Sm 時間
伺服器花費： I/Sc 時間

假設傳輸量為 L，寬頻為 B
那傳輸時間為： L/B

假設功率
Pm：手機運算
Pi：手機閒置
Pt：手機傳送
Pr：手機接受

消耗的能量 E：
經由手機上運算的消耗： Em = Pm * I/Sm
由雲端幫忙算手機的消耗： Ec = Pi * I/Sc + Pt * L/B + Pr * L/B

省下的能源 = Em - Ec

假設 Sc = Sm * N，意思是雲端上算比手機算快Ｎ倍

最後得到
省下的能源 Es = (Pm - Pi/N) * I/Sm - (Pt + Pr) * L/B
```
整個運算在「運算一個工作的時間內」條件下，交給手機算比較省電，還是經由網路傳輸交給雲端算比較省電。
從結論來看，當 L/B 比 I/Sm 小非常多，且Ｎ非常大的時候，我們可以省下很多資源。
聽起來很合理，L/B 夠小只要網路速度夠快，而手機計算速率 Sm 很小，雲端速度遠大於手機速度（Ｎ倍）也非常合理。

現在我們相信這個方式的確省電了，但省多少呢？
我們要來做實驗！

---
## 實驗
環境： 智慧型手機、WIFI連線、電表、雲端、筆電、手機轉影片的 APP
網路速度採用 [IEEE 802.11g 標準](https://zh.wikipedia.org/wiki/IEEE_802.11g-2003)。
架設如下（圖片來自論文）：
![](https://user-images.githubusercontent.com/18013815/34781610-3f83a33a-f661-11e7-9100-9228ef37fc38.png)
這邊用電腦假裝是雲端

實驗方式：將 30 MB 720p 的 flv 影片轉換成 11MB 320x240 的 mp4 影片。
- T1：影片在手機，也用手機轉檔
- T2：影片在手機，但上傳到雲端轉檔
- T3：影片在雲端，下載下來在手機轉檔
- T4：影片在雲端，手機傳訊息跟原端說要轉檔

詳細流程：
- T1:：手機上轉檔花了 180 秒，消耗 32 J
- T2：（1）30 MB 花費 63 秒上傳，消耗 15 J （2）雲端轉檔花了 30 秒，手機閒置消耗 1 J （3）下載檔案 11 MB 花了 120 秒，消耗 5 J （4）結論是共花 120 秒，消耗 21 Ｊ
- T3：（1）30 MB 花費 58 秒下載，消耗 13 J （2）手機轉檔花了 180 秒，手機閒置消耗 31 J （3)結論是共花 238 秒，消耗 44 Ｊ
- T4：手機傳送要求，花費 300ms，接著看著網頁進度條跑完。手機傳送請求加等待時間，花費 42秒，消耗 9.6 J

![](https://user-images.githubusercontent.com/18013815/34782644-5a4a1ffc-f664-11e7-9dbb-4187838daf15.png)

---
## 結論
實驗結果跟檔案大小、網路速度都有關係，但總之網路速度越快，省去上傳、下載和閒置的電源消耗，給雲端算(Offload)對手機省電的效果也就越好。雖然我們數學推導終究能預期結果，但實際看看實驗數據也是滿有意思的。在網路瀏覽過程中加上雲端計算，不僅可以省時間，同時手機也消耗更少電量。

雖然這邊用影片轉檔為例子，但其實可以把這個概念套用在一開始說的三種 offload 方法中，各種瀏覽網路的情境皆可以適用，例如瀏覽臉書的時候，藉由 proxy 將臉書圖片先壓縮並解碼，不僅傳輸量下降，也省去手機解碼的時間和電源消耗。此外這種伺服器端的瀏覽技術，還有其他好處，未來會再介紹，請拭目以待！

---
希望有幫到大家，大家明天見！

