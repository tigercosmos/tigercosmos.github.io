---
title: 談談 Servo 專案
date: 2017-12-27 23:33:38
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


## 前言
什麼是 Servo?
> Servo 是一款專為應用軟體和嵌入式應用而設計的現代化的高效能瀏覽器引擎 

## 緣起
C++ 一直以來都是很棒的語言，尤其在處理低階的程式更是適合，但他畢竟也不是萬能的，事實上他在處理記憶體多程序時，會有安全性的疑慮，像是記憶體未如期清除。

當然我們可以用個嚴謹的方式寫 C++，那麼很多不安全的邏輯可能就不會產生，但這畢竟不是一個好的解決方式。我們希望開發者不犯錯，但事實上最會犯錯的就是開發者！

Mozilla Firefox 瀏覽器的核心引擎是 Gecko，就是由 C++ 所撰寫。而 Mozilla 深知安全性問題必須解決，所以便有了 Rust 語言以及 Servo 專案的誕生。

簡單來說，
Rust 取代 C++
Servo 取代 Gecko

任一個都是驚天動地，還一次兩個！

## Rust
Rust 最早由 Mozilla 資助開發，後來因為 Dropbox 使用 Rust 改寫檔案系統服務而聲明大噪。目前 Rust 是很活躍的開源專案，有超過兩千名開發者共同開發，大約一至兩個月就會有一次 minor release。Rust 的目標是成為高效率、易於平行運算的系統程式語言，因此它選擇了以下的特性：

* 靜態型別 (static-typed)
* 區分 mutable 與 immutable，所有變數預設為 immutable，盡可能減少 mutable state
* 使用 tagged union 與 pattern matching
* 不使用動態垃圾回收 (garbage collection)，而使用靜態的 RAII
* 使用 Move semantics 避免複製物件
* 使用 borrow checker 確保 memory safety 與 thread safety

## Servo
Servo 專案最早從 2012 年開始為實驗性質，後來 2015 在 CSS 上有重大突破，2016 時正式釋出第一版，並可以正確渲染以及效能比 Gecko 更好，於是 Mozilla 便有了量子專案，把 Servo 專案中最成熟的 CSS 模組，也就是 Stylo 整合進 Gecko，使得速度和效能變更好，也就是今年 2017/11 正式發表的新版 Firefox。

本來預期是希望 Servo 能完全取代 Gecko，不過光是維護 Firefox，Mozilla 就幾乎沒什麼餘力了，投入新的 Servo 的人力就很少，進展也就很困難。長遠來看 Servo 和 Gecko 應該會互相搭配，要達到完全切割取代恐怕很難。雖然能投入的人力很少，值得慶幸的是 Servo 的志願貢獻者數量可觀，這是因為不同於 Firefox 舊時代的開發流程，Servo 採用 Github 經營社群，並透過許多 bot 來達到自動化的步驟，整體的開發體驗非常順暢，社群也非常友善，讓 Servo 上的開發者非常蓬勃。至於我則是渴望看到 Servo 完全成熟的一天，覺得將會是劃時代的突破！

此外 Servo 和 Rust 有共生關係，基本上 Servo 可以說是 Rust 的最大試驗平台。Servo 專案同時也和 W3C 的[網路平台測試](https://github.com/w3c/web-platform-tests) 專案同步，後者是專門測試瀏覽器是否符合 W3C 標準的測試專案。此外 Servo 專案也完全照 [WHATWG](https://whatwg.org/) 的瀏覽器規範實作。
> 網頁超文字應用技術工作小組（Web Hypertext Application Technology Working Group, WHATWG），是一個以推動網路HTML標準為目的而成立的組織。在2004年，由Apple公司、Mozilla基金會和Opera軟體公司所組成。

---
## 連結
[Servo Github](https://github.com/servo/servo)
[下載 Servo](https://download.servo.org/zh-TW/index.html) 來體驗看看
[Servo 中文官網](https://servo.org/zh-TW/index.html)
[Rust](https://www.rust-lang.org/en-US/)
[Rust book](https://doc.rust-lang.org/book/first-edition/)
[how stylp brough rust and servo to firefox](http://bholley.net/blog/2017/stylo.html)

---

希望有幫到大家，大家明天見！

