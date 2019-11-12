---
title: 踏入 Mozilla Servo 兩個月的心得
date: 2017-10-17 00:00:00
tags: [Chinese Posts,English Posts,Mozilla,Mozilla Taiwan,Servo,Open Source,Chinese,]
---


## 踏入 Mozilla Servo 兩個月的心得

### 開發 Servo 有感而發寫下的紀錄

<img class="dz t u gs ak" src="https://miro.medium.com/max/2916/0*daP-rFRZjuTsI1mY.jpg" role="presentation"><br/>

不知不覺，兩個月下來已經在 Mozilla 的 <a href="https://github.com/servo/servo" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">Servo</a> 有 <a href="https://github.com/servo/servo/commits?author=tigercosmos" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow"><em class="hz">8 次 commits</em></a>。 Servo 為新一代 Firefox 的基石，所以做起來非常有成就感，也對瀏覽器本身開始有極大興趣。而且這個社群非常友善，開發過程讓人覺得很快樂，看著兩個月以來的紀錄，有感而發寫下這篇文章。

<!-- more --> 

<span style="font-size: 26px; color: #696969; font-style:italic">關於 Servo 可以看這邊的介紹：剖析極速 CSS 引擎：Quantum CSS</span>

關於 Servo 可以看這邊的介紹：<a class="dj by hv hw hx hy" target="_blank" rel="noopener" href="/@moz2000tw/剖析極速-css-引擎-quantum-css-原名stylo-上-723f08d064f1">剖析極速 CSS 引擎：Quantum CSS</a>

約兩個月前，我在 <a href="https://medium.com/u/3dde774e776b?source=post_page-----9eaf41e021f9----------------------" class="id az by" target="_blank" rel="noopener">Mozilla Taiwan</a> <a href="https://www.facebook.com/MozillaTaiwan/" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">粉專</a>底下留言，說我想參加 Mozilla 的開源專案。說到 Mozilla 最廣為人知的當然就是 Firefox，當然我也去看 MDN 的文件，甚至還去看社群一些過去的人的經驗分享，但就是覺得不得其門而入。這些都是大專案了，即便是小 Bug 對一個新手來說都不小。我覺得需要一個導師帶我入門，就突發奇想去粉專底下留言，碰碰運氣了。

本來想回去找我在粉專的留言，但不知道為甚麼被刪掉了(也許是覺得已經回復我所以可以刪掉？) 總之就好幾個人熱心的留言，丟了一些文件給我，更重要的是有個工程師(@<a href="https://github.com/shinglyu" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">shinglyu</a>)留言說可以幫我，真的很感動。@shinglyu 那時候負責的專案是 <a href="https://github.com/servo/servo" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">Servo</a>，而我只是希望能找大型開源專案參加，所以就順勢踏進 Servo 裡面。

既然有導師了，接下來就是找 Bug，通常第一步就是找「<a href="https://github.com/servo/servo/labels/E-easy" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">簡單</a>」標籤的的 Issue 來解決，但那時候全部都已經被 “Assigned”，也就是都有人認領，就沒簡單的東西可以做。但接觸一個專案的第一步，一定要 clone 下來 build 看看呀！神奇的事情就這麼發生了，Windows 上竟然 build 不成功，不管是換電腦或是換VM，總之就一直失敗，這麼大的專案竟然連最基本的 build 都成功不了，這真的很奇葩。然後去查 issue，的確也有人回報過，卻得不到解答。@shinglyu 和 Servo 的專案下的團隊成員，平常似乎也都只用 Linux 或 MacOS 開發，對於 Windows 狀況也不了解。

接下來的大約兩周，我都在摸索為甚麼 Windows 上會 build 失敗，後來發現主要卡在幾個點。這邊要先解釋一下 Servo 怎麼 Build 的，流程是：

<span style="font-size: 26px; color: #696969; font-style:italic">mach.bat(start)→ enter vs shell (C++ environment) -> python ( setting and download packages) -> build rust</span>

mach.bat(start)→ enter vs shell (C++ environment) -&gt; python ( setting and download packages) -&gt; build rust

Servo 在 Windows 上要 build 的時候，會先跑 bat 檔呼叫 Visual Studio 的 Shell (Unix like 就不用這麼麻煩)，但不知道為甚麼有時候裝的 VS 就可以順利啟動，有時候就不能啟動，後來我發現只裝 VS build tool 而不直接裝 VS Community 的話，幾乎可以保證一定可以過 bat 啟動 shell 的這一關，後來針對這個就發了 2 個 PR。

此外發現 python 在判斷系統環境時會出錯，經過多次嘗試，後來直接把判斷的地方 hack 掉，不知道為啥原本的寫法把邏輯弄得很複雜、很冗，於是就把感覺多餘的東西通通砍掉，後來就 pass 了，也發了 PR。只是這個 PR 卡很久，因為負責審 Windows 的 @<a href="https://github.com/larsbergstrom" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">larsbergstrom</a> 調到其他專案很忙，很少有空關心這邊狀況。這是我第一個發的 PR，最後卻是到目前最晚被 Merge 的 XD。

在這之後一直有持續關注 issue，並挑了幾個來做，從一開始覺得問問題有點怕怕的，漸漸地覺得有掌握整個專案的架構了，不再那麼陌生，到後來覺得跟主要的成員都有點熟了。我很謝謝 @larsbergstrom，他在每次回應時都給極大的鼓勵，且讓人覺得很真誠。也謝謝 @shinglyu 在一開始帶我入門，和我討論很多東西。<a href="https://github.com/ferjm" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">@ferjm</a> <a href="https://github.com/asajeffrey" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">@asajeffrey</a> 會很仔細地和我討論細節，即便有些問題我覺得有點蠢 XD。最後 Servo 成員中最熱心的莫過於@<a href="https://github.com/jdm" class="dj by hv hw hx hy" target="_blank" rel="noopener nofollow">jdm</a> 了，他會一直在 issue 和 PR 上面巡，幾乎都可以及時得到解答，甚至假日他都還會關心大家。整體而言，我覺得 Servo 和 Rust 的開源社群很活躍，裡面的人也很友善，對於一個新手來說絕對是很好的選擇，甚至在專案待久了，還有種親切的感覺，真的很棒！