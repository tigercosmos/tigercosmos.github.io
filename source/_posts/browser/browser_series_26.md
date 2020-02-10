---
title: 市面瀏覽器個案分析：隱私篇
date: 2018-01-06 23:54:04
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
市面上的瀏覽器五花八門，各有各的優缺點。
俗話說知己知彼百戰百勝，想要在這片紅海殺出，勢必要了解對手。

我在網路上無意間找到一款手機瀏覽器 [Lightning Web Browser +](https://play.google.com/store/apps/details?id=acr.browser.lightning)。讓我們一探究竟！

來看看他的介紹吧：
> Lightning Browser Plus is a simple, fast web browser that focuses on design, security, and efficiency. It uses material design, doesn't track you, give you lots of options to protect your privacy. It gets out of the way of the user. I built this browser because I wanted something better.

詳細的介紹中他主打：

> - Speed - By utilizing the WebKit rendering engine that comes built into your Android device, Lightning can ensure a swift, lightweight experience.
> - Privacy - Use Incognito Mode to browse without leaving a footprint, download Orbot and turn on TOR proxy support to mask your identify and location, use StartPage or DuckDuckGo for your search engine, or disable settings that you think leave you at risk. Whatever your concern, Lightning will try to help.
> - Features - Full-screen, check. AdBlock, check. Inverted Rendering, check. All the search engines you want, check. Search Suggestions, Bookmarks, History, User Agents, Reading Mode, whatever you need, Lightning does it.
> - Open-source 

這是一款要收費的 App，一次性付費 50 NT。但很神奇的他有開源，那我自己 build 安裝就好了啊？

看以上說明就讓我想到另一款瀏覽器： [Firefox Focus: 隱私保護瀏覽器](https://play.google.com/store/apps/details?id=org.mozilla.focus&hl=zh_TW)

比較兩者，Focus 跟 Lightning 強調的重點有 3/4 吻合。
一樣都是採用 Webkit，也很強調隱私，同樣都開源。不過 Focus 是免費的。
至於在隱私方面誰優秀這我就不清楚了。
不過因為兩個瀏覽器都有開源，所以其實可以深入去分析誰比較強！

講到這裡，我們知道兩者差異只有介面設計不一樣了！
我稍微研究了一下 Lightning 的介面，發現其實也很簡單，左側可以叫出分頁，右側可以叫出書籤。

我覺得兩者瀏覽器差異沒有很大。所以最後我滿好奇到底 Lightning 是如何得到他的目標客群，可能可以以此做個小研究，我猜最有可能的原因是時間，Focus 的誕生時間明顯比較晚，而比較早上市的產品也就有一群早期的使用者，不過這也僅是我的猜測。

最後因為兩個都有開源，我把核心的部分找出來：
[Focus 原始碼](https://github.com/mozilla-mobile/focus-android/tree/master/app/src/main/java/org/mozilla/focus)
[Lighting 原始碼](https://github.com/anthonycr/Lightning-Browser/tree/dev/app/src/main/java/acr/browser/lightning)

我稍微看了一下兩者 App 的架構，長的其實滿像的，不過也不意外，畢竟都叫做瀏覽器，主要還是去看細節。像是兩者皆主打的隱私實作。

隱私的部分主要是在下載、搜尋、行為追蹤、擋廣告，直接從目錄資料夾不難找到相關程式碼，點進去看看怎麼做的其實滿有趣的！

---

希望有幫到大家，大家明天見！

