---
title: 深度分析 Puffin OS Phone—搶攻第三世界的智慧手機
date: 2020-01-29 00:00:00
tags: [Puffin Browser , Browsers, Puffin OS Phone, Cloudmosa,]
---


![puffin os phone photo](https://user-images.githubusercontent.com/18013815/73357418-4a4a3300-42d7-11ea-9456-7344680463ba.jpg)

Puffin OS Phone 是 CloudMosa 所研發，搭載其自家作業系統 Puffin OS 的低階智慧手機，CloudMosa 團隊開發的智慧手機將主打第三世界市場，以極低價的成本，藉由其在後端渲染瀏覽器的成熟技術，讓即便網速很低且硬體不強的情況下，仍有市面中階手機在穩定網路環境的使用體驗。本文將深入討論 Puffin OS Phone (之後以 POP 代稱) 的各種面向。

## 智慧手機與開發中國家

科技始於人性，科技更該是人權之一。

根據 [The World Bank](https://data.worldbank.org/) 報告，對比高收入國家和中低收入國家，截至 2017 年前者有 85% 網路普及率對比後者只有 43%；而令人訝異的是 2018 年手機訂閱普及率(每一百人)前者有 126%，後者則是 100%。也就是說這個世界幾乎每個人都有一台手機，但中低收入國家的網路普及率卻不及一半。

接著再比較不同世界國家每個人享有的頻寬大小(Kb/s)：

![bandwidth comparison](https://user-images.githubusercontent.com/18013815/73361354-c5174c00-42df-11ea-965b-120af2e600ca.jpg)
(來源：[The World Bank](https://tcdata360.worldbank.org/indicators/entrp.inet.bandwidth?country=USA&indicator=3405&countries=IND,IRQ,KEN,MYS,SOM,TUR,EGY,CHN&viz=bar_chart&years=2016&indicators=944))

圖中可以發現美國遠遠是世界平均兩倍，但是東南亞(印度、馬來西亞)、非洲(肯亞)或中東(埃及)國家卻低於世界平均，其中印度、中國、埃及更是遠遠低於平均。也就是說中低收入 43% 享有網路的人口，其享受的網路服務頻寬卻是十分有限的。

所以我們推斷甚麼？

中低收入國家的人民普遍有手機，但也許是低價的傻瓜手機，同時他們大多數人並沒有享有網路服務，即便有網路也比較慢。

事實上，Firefox 還要特別針對東南亞開發 Lite 版本，原因就是 100 Mb 的正常版本對他們來說已經太大，那幹嘛不去下載別家的 Lite 瀏覽器只要 20Mb，所以 Firefox 只好也跟著開發 Lite，衍伸出特別的市場文化，從這個現象也可以知道，網路頻寬在開發中國家是多麼奢侈的服務。

Puffin OS Phone 想要解決的問題便是針對上述問題而生，POP 希望讓開發中國家的人民可以用低價取得手機，同時在頻寬有限下，還可以享有好的手機上網體驗，所以他們基於原本有的 Puffin Browser 技術開發出 Puffin OS，並整合手機生產鏈，製造出價格非常親民的 POP 低階智慧手機，卻可以讓使用體驗堪比中階智慧收機。

## 開箱

開箱過程可以看劉胖胖拍開箱影片，裡面介紹 POP 包裝、手機介面、使用體驗、軟體安裝等等，所以我就不多作介紹。

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/z1HfsgXsFxg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Puffin OS Phone 技術原理

原本 CloudMosa 便有 Puffin Browser，其後端渲染瀏覽器的性質，其實在各種手機上都可以有效降低手機計算量和網路頻寬用量，瀏覽器的技術源里我寫在「[How the Puffin Browser Works](https://tigercosmos.xyz/post/2018/09/puffin/)」一文中，簡單來說 Puffin 背後有數據中心把原本瀏覽器要打開網頁下載資源和渲染網頁的步驟做掉，使用者因而減少計算資源和流量。

所以更進一步，反正 Web 已經可以打天下，大多數服務都可以用 Web App (就是開一個網頁當作是應用程式) 來取得，那麼何必都用 Native App (一般在 Play 商店下載的應用程式) 呢？例如 Instagram、Facebook、新聞、郵件等等，哪一個不是 Web App 辦不到的？一個全部基於 Web App 的作業系統油然而生，其實 Puffin OS 便是根據 Android 修改的簡化版，拔除所有 Google Service，因為非常佔空間，且不再需要 Play Store。

現在的痛點是，第三世界國家的人只負擔得起低階手機，但一般的應用程式占空間又吃計算效能，同時這些地區頻寬也不高，低階手機體驗可能會很差。即便都改成 Web App，不佔空間了，資料傳輸也會是瓶頸。因此 Puffin OS 就是基於 Puffin Browser 原理，將手機所有網路服務都用與 Puffin Browser 同樣手法處理，也就是說現在想要滑 Facebook 就是開 FB 的 Web App，因為 Puffin 把計算和頻寬問題都在其數據中心處理，手機其實不怎需要作計算且流量也大大減低，因此 Puffin OS 可以讓低階手機上順暢使用各種 Web App，也不用怕計算不夠快或頻寬有限造成卡頓。

## 效能實測

接下來要來做實驗，實驗設備分別是 Puffin OS Phone、Samsung J2、Sony Xperia 10 Plus 分別代表低階手機和高階手機，同時用 3G (低速) 和 4G (高速) 網路來測試，藉此來較：

- 低階手機配 Puffin OS 在低速和高速網路效能
- 低階手機用一般瀏覽器在低速和高速網路效能
- 高階手機用一般瀏覽器在低速和高速網路效能
- 高階手機用 Puffin Browser 在低速和高速網路效能

三台手機規格分別是：

- PUffin OS Phone: 4xARM Cortex-A53 @ 1.27 GHz / 1024 Mb RAM
- Samsung J2: 4xARM Cortex-A53 @ 1.44 GHz / 1407 Mb RAM
- Sony Xperia 10 Plus: Qualcomm Snapdragon 636 1.80 GHz / 5739 Mb RAM

實驗中 3G 速度為下行 4.46 Mb/s 上行 0.34 Mb/s。，4G 速度為下行 21 Mb/s 上行 4 Mb/s。

在繼續閱讀之前，大家可以看一下「[為什麼手機上網速度比較慢呢？](/post/2017/12/browser/browser_series_18/)」體會一下網速差異影響到底有多劇烈。

![4G 網頁速度比較](https://user-images.githubusercontent.com/18013815/73379487-47facf80-42fd-11ea-8815-e24e300037b8.png)
![3G 網頁速度比較](https://user-images.githubusercontent.com/18013815/73379501-50eba100-42fd-11ea-9fef-bfc456d4051f.png)
