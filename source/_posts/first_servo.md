---
title: 你的第一份大型開源專案--Servo 瀏覽器
date: 2018-01-29 00:00:00
tags: [Chinese Posts,English Posts,Browsers,Servo,Open Source,Software Development,Chinese,]
---


## 你的第一份大型開源專案: Servo 瀏覽器

Your First Big OSS Project: Servo Browser

<img class="dz t u gw ak" src="https://miro.medium.com/max/2400/0*pEiDFJWNkrT9c5md.jpg" role="presentation"><br/>

## 前言

開放原始碼軟體，又稱開源軟體（Open Source Software），顧名思義是將軟體的原始碼公開。詳細介紹可以看<a href="https://zh.wikipedia.org/zh-tw/%E9%96%8B%E6%BA%90%E8%BB%9F%E9%AB%94" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">維基百科</a>介紹以及<a href="https://buzzorange.com/techorange/2014/12/19/what-is-open-source/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">什麼是開源</a>一文。

身為軟體開發者，我們常常會需要很多工具來幫助我們更簡單完成工作，而且我們都知道沒事不要自己造輪子，這時候就會看看網路上有沒有現成的工具。例如想要開發機器學習可能就會用 Tensorflow，想要開發網頁前端可能會使用 Angular，想要開發 Android App 可能會用 Kotlin，平常用的 gcc 或 clang，甚至 Linux 作業系統通通都是開源軟體。

<!-- more --> 

取之於社會，回饋於社會。在我們享受開源軟體的無窮好處之虞，也想為開源軟體盡一份心力，不僅讓更多人受惠，也滿足自己的成就感。貢獻開源有很多種，可以是協助建立文件、幫忙翻譯、解決 bug、開發新功能，此外開源軟體也有分大跟小，大的專案例如 Chrome 瀏覽器，小的專案可能只是 VSCode 的擴充功能。當我們野心比較大的時候，就會希望自己能貢獻一些大型專案，而不是小專案而已，而且會希望自己能開發出核心功能，不僅僅是改個小 bug 或幫忙翻譯文件而已。

但是大型開源軟體往往已經發展過於龐大，面對已經有數十萬、數百萬行的軟體而言，一個新手想要參一咖並不容易，更何況還沒有其他開源經驗。

本篇將選定 Servo 瀏覽器作為一個想要貢獻大型開源專案新手的第一份專案，目前我在 Servo 專案中在八百名貢獻者中排名約前五十，算是活躍貢獻者之一。此外因為我本身熱愛開源，所以也參加了不少開源專案。希望透過我的經驗，帶大家進入開源的世界！

## 什麼是 Servo 專案

Servo 專案是 Mozilla 的實驗性質瀏覽器引擎，目的是加強安全性以及採用平行化加速處理，並慢慢將成熟的模組移植到 Ｍozilla 旗下的瀏覽器 Firefox。Servo 以 Rust 語言開發，該語言強項正是安全性與平行化。當初就是發現很多 Firefox 有很多 bug 是 C++ 產生，其中最常見的問題便是記憶體錯誤，於是後來有了 Rust 語言的誕生。在使用 Rust 情況下，幾乎不會產生原本 C++ 導致的問題。

## Servo 有什麼好處

如果說將一個開源專案成熟度分為三級：成熟、中間、陽春，Chromium（Chrome 的開源版本）就是成熟，而 Servo 則是中間，因為 Servo 還在開發中，只完成最重要的工程，還有很多細節沒有實作。

不過這也是初學者學習 Servo 好處，因為專案還沒發展過於龐大，學習曲線相對 Chrome 這類專案來說，比較不那麼陡。藉由開發 Servo 的過程，更容易對瀏覽器有更完整的了解，之後去看 Webkit、Gecko、Blink 等發展已久的大型瀏覽器引擎時，也會更容易上手。

此外因為很多功能還沒實作，初學者比較有機會直接對核心模組（Core Module）貢獻，通常發展已久的大型專案核心部分都已經非常龐大或完整，新手比較難有機會對其貢獻，即使是核心模組的 bug 難度通常也很高，畢竟那是程式最重要的部分，幾乎不會有低級的錯誤。

但由於 Servo 還處於中期，很多瀏覽器該有的重要功能，因為重要順序稍微低一點所以還沒實作，就是新手大展身手的好時機，並且瀏覽器都會遵循網頁技術的規範，所以開發時常常有文件可以對照著開發。

除了上述幾點之外，因為 Servo 是一個網路瀏覽器，意即就是在寫一個讓人可以打開網頁的程式，你會對瀏覽器如何處理網頁有更深入的理解。對前端工程師來說，也許瀏覽器就像個黑盒子，開發好的網頁給瀏覽器執行就會渲染出網頁畫面，但是對其中的機制卻不太了解。當我們了解一個網頁是如何從網頁原始碼被解析，到渲染出圖層被渲染出來之後，在寫網頁的時候就能針對瀏覽器運作的機制做優化。

## 在開始貢獻之前

有一些基礎知識我們必須先瞭解，首先 Servo 以及目前市面上數以百萬計的開源專案都是採用 Git 版本控制工具，以及 Github 這個網路協作平台，目的是要讓程式碼方便管理以及讓多人可以同時開發。

關於 Git 與 Github 的科普入門可以看<a href="https://kopu.chat/2017/01/18/git%E6%96%B0%E6%89%8B%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8-part-1/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">這篇(1)</a>和<a href="https://kopu.chat/2017/01/18/git%e6%96%b0%e6%89%8b%e5%85%a5%e9%96%80%e6%95%99%e5%ad%b8-part-2/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">這篇(2)</a>文章，作者本身並非工程師，相信對原本熱愛寫程式的大家來說應該會很好懂。如果還有一些不清楚，可以多 Google 幾篇文章應該就會有點感覺了！

當你會使用 Git 和 Github 之後，你需要知道什麼是 <a href="https://guides.github.com/activities/forking/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Fork 和 Pull Request</a>，這是 Github 上提交 Patch（補丁）的方式。當你有新的點子，或是想要修補臭蟲，就可以透過 Fork 動作複製一份原始碼，然後進行修改後。實際改好程式碼之後，就可以就可以發出 Pull Request（合併請求），請原本專案的管理者將你的更動，合併到原始的專案中。

再來就是 Servo 主要是以 Rust 語言當作軟體的開發語言，以 Python 作為輔助工具語言，所以需要先去了解一下語言怎麼寫，語法是怎樣等等。並且因為我們開發的是網路瀏覽器，最好要能懂怎麼寫一個簡單的網頁，包含 HTML、CSS、JavaScript。

此外每個開源專案都會有自己的「Code of Conduct」，裡面會規範貢獻者該遵守的規則，通常就是必須友善包容，不得污辱謾罵其他人。

## 瀏覽器原理

知道瀏覽器是怎麼一回事對我們開始開發瀏覽器會很有幫助，<a href="https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">How Browser work</a> 是一篇很好的起手文，他宏觀的解釋瀏覽器在幹嘛，也就是你打開 Chrome、Safari 這些軟體是怎麼去讓網頁變成看得見的網頁。比較深入可以看我寫的<a href="https://ithelp.ithome.com.tw/articles/10197966" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">《來做個網路瀏覽器吧！》</a>系列文章，此系列文章可以邊研究 Servo 專案邊看，應該會讓你更快上手！

## 取得源碼、編譯 Servo

在我們繼續了解怎麼參與貢獻專案之前，先來用源碼編譯看看，確定能編譯成功我們才能繼續下一個步驟。

首先到 Servo 的 <a href="https://github.com/servo/servo" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Github 頁面</a>，先點「Fork」複製一份原始碼到自己的帳號底下。

<img class="dz t u gw ak" src="https://miro.medium.com/max/3936/0*8GjJUhdyrAUJf-r3.png" role="presentation"><br/>

接著要把源碼從自己的複製的版本下載下來：

```undefined
git clone https://github.com/你的Github帳號/servo.git
```

接著照 Servo 的<a href="https://github.com/servo/servo#setting-up-your-environment" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">環境建設指南</a>，選擇你的系統環境，將需要的套件安裝和設定。

這邊假設你是使用 Ubuntu，那流程就會是：

```undefined
# rustup 是 rust 語言的工具，為 Servo 專案必備
curl https://sh.rustup.rs -sSf | sh

# 安裝套件
sudo apt install git curl autoconf libx11-dev \
    libfreetype6-dev libgl1-mesa-dri libglib2.0-dev xorg-dev \
    gperf g++ build-essential cmake virtualenv python-pip \
    libbz2-dev libosmesa6-dev libxmu6 libxmu-dev \
    libglu1-mesa-dev libgles2-mesa-dev libegl1-mesa-dev libdbus-1-dev \
    libharfbuzz-dev ccache clang
# Ubuntu 17.04 之後
sudo apt install libssl1.0-dev
# Ubuntu 17.04 之前
sudo apt install libssl-dev
```

這邊要注意的是，Servo 的源碼隨時在更新，需要用到的套件可能也會改動，這面這些只是我寫文章當下所需要的，時間久了可能就不準，到時候還是必須上 Servo 的 Github 去看比較準。

接著就可以試著編譯看看了，先進入專案，然後我們會用到 <code class="ha if ig ih ii b">mach</code> 工具，這是 Servo 專案的入口程式，用來執行各種指令。

```undefined
cd servo
# 編譯
./mach build -d
# 執行
./mach run -d https://google.com
```

原則上如果設定都照指南完成，應該可以順利編譯和執行，如果過程中產生任何無法解決的問題，可以在 Servo 專案上面發布 <a href="https://github.com/servo/servo/issues" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">issue</a>，說明你的環境設定和錯誤訊息。

順利執行的話應該能看到有視窗跳出來，並且將 Google 的頁面渲染出來了。

<img class="dz t u gw ak" src="https://miro.medium.com/max/2076/0*QUg8ii9oQvodAbl_.png" role="presentation"><br/>

## 開始貢獻

我覺得開源專案中最困難的一步，就是真的要來修改原始碼，一開始我們大概無法直接去實現新的功能、增加一個模組，通常是先去找有沒有簡單的 bug 可以解決。

多數待解決的問題都會列在 issue 頁面上。在 Servo 上可以去找「<a href="https://github.com/servo/servo/issues?q=is%3Aopen+is%3Aissue+label%3AE-easy" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">E-esay</a>」標籤的 issue 當作起手，通常是團隊成員認為最簡單適合新手的，才會標上此標籤。

Servo 專案事實上用到很多子專案以及衍伸專案，例如 <a href="https://github.com/servo/webrender" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">webrender</a> 模組就被獨立切出來。所以如果想要看看更多待解決的問題，可以使用 <a href="https://starters.servo.org/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Servo Starters</a> 這個網站來查詢議題，裡面收集包含 Servo 專案以及周遭專案的的各種起手問題。

由於我們第一次參加這個開源專案，從中選一個標有 <code class="ha if ig ih ii b">Easy</code> 或 <code class="ha if ig ih ii b">Good First Issue</code> 等標籤的問題會比較適合。接著就來介紹如何開發。

## 開發流程

這邊以 Servo 專案為例講解流程，而以 Github、Gitlab 為平台開發的大型專案工作，不管是不是開源（差別只是公開或是私有），其實流程都很類似，可以說是現代軟體開發的制式流程了！

大致可以歸納成以下步驟：

<ol>
<li id="2a01" class="fv fw em at fx b fy fz ga gb gc gd ge gf gg gh gi iq ir is">找到目標</li><li id="0dd4" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi iq ir is">參考文件</li><li id="42da" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi iq ir is">實際開發</li><li id="1647" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi iq ir is">單機測試</li><li id="4794" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi iq ir is">送出審查</li><li id="78b2" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi iq ir is">自動化測試</li><li id="266b" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi iq ir is">進入主幹</li>
</ol>

## 找到目標

首先就是要找想做什麼，一但選好你有興趣的 issue，確認對話串中沒有人聲明說目前正在進行中，你就可以聲明要認領這個問題。

如果看了問題覺得有興趣，可是卻還是沒概念，這時候不用怕，總之先喊說你想要解決。

通常標註 <code class="ha if ig ih ii b">E-esay</code> 標籤本來就是希望給新手練習的機會，此外即便沒有標註簡單標籤，任何的 issue 也可以大膽去接，因為在開源社群中大家都很樂於幫助新手和回答任何問題。

你可以在 issue 下這樣留言：

<span style="font-size: 26px; color: #696969; font-style:italic">Hi @someone, I would like to take this issue.</span>

<em class="at">Hi @someone, I would like to take this issue.</em>

<em class="jb">Someone</em> 可能是專案的成員，或著是發布 issue 的其他貢獻者，總之在你開始工作前記得先喊一聲，先搶先贏，喊到的人就必須試圖將 issue 解決，而其他人不應該再來跟你搶。

以 Servo 來說，你可以在下面留言 <code class="ha if ig ih ii b">@highfive: assign me</code>，<code class="ha if ig ih ii b"><em class="jb">highfive</em></code> 是此專案的機器人，它會替 issue 自動加上「被認領」標籤。

<img class="dz t u gw ak" src="https://miro.medium.com/max/3720/0*5sSoqL6m75PTaCEn.png" role="presentation"><br/>

有任何不懂，或是開發過程中遇到困難，千萬不要怕問很白痴的問題。大家都是從問白癡問題開始學起的，專家眼中的 <code class="ha if ig ih ii b">Easy</code> 可能是新手眼中的 <code class="ha if ig ih ii b">Super Hard</code>。

所以這時候你可以問更多細節：

<ul>
<li id="8117" class="fv fw em at fx b fy fz ga gb gc gd ge gf gg gh gi je ir is">Could you tell me where is the relevant code?</li><li id="c6a1" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is">What is the purpose of <code class="ha if ig ih ii b">Foo Function</code> and how it affects <code class="ha if ig ih ii b">bar Function</code>?</li><li id="ded3" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is">How could I test the result? How could I write a new test?</li><li id="2507" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is">Are there any specification? Where is it?</li>
</ul>

或是你覺得 issue 本身就描述的很難懂了，完全沒有概念要怎麼做。這時候可以直接問能不能給更多細節：

<span style="font-size: 26px; color: #696969; font-style:italic">Hi @someone, I would like to solve this issue. However I don’t know how to do. Could you tell more detail about how to implement/fix this issue.</span>

<em class="at">Hi @someone, I would like to solve this issue. However I don’t know how to do. Could you tell more detail about how to implement/fix this issue.</em>

發布 issue 的作者或是其他貢獻者會來回答你，如果你還是覺得不清楚，可以繼續追問，不用怕對方不耐煩或是覺得丟臉，開源社群就是這樣注重互相幫助，重點就是你敢不敢問。

## 參考文件

不同的專案都會有必須遵從的規範和文件，例如一個影音播放軟體，就需要遵從各種影片格式來做處理，或是模組與模組之間可能已經定義好 API 如何設計。

而瀏覽器開發最常參考的兩個文件分別是 W3C 和 WHATWG 兩個組織所規範的：

<ul>
<li id="d833" class="fv fw em at fx b fy fz ga gb gc gd ge gf gg gh gi je ir is"><a href="https://html.spec.whatwg.org/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">https://html.spec.whatwg.org/</a></li><li id="df83" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is"><a href="https://www.w3.org/TR/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">https://www.w3.org/TR/</a></li>
</ul>

針對不同的技術部份，會有<a href="https://github.com/servo/servo/wiki/Relevant-spec-links#spec-links" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">各種文件</a>明確規範，如 DOM、XHR、CSS 等等。

<img class="dz t u gw ak" src="https://miro.medium.com/max/2212/0*rzlYwYz_OfwJpixj.png" role="presentation"><br/>

基本上所有開發都必須遵從規範，瀏覽器開發者依照規範設計瀏覽器，網頁開發者依照規範設計網頁，規範可以說是兩者的橋樑，確保網站設計者心中想的網頁，可以正確被瀏覽器渲染出來。並且因為大家都遵照同一份規範設計瀏覽器，才能讓 Chrome 顯示的畫面跟 Firefox 一樣，不然網頁開發者豈不是要針對不同瀏覽器都寫一份程式碼？

## 實際開發

這邊以這個 issue: <a href="https://github.com/servo/servo/issues/13282" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Support cloning steps for textarea/input</a> 為例，假設我們選定這個當作要解決的目標。

這個 issue 是因為 WHATWG 的 HTML 文件有更新，所以要讓 Servo 與最新的標準一致。而要修正的地方就是直接對照文件變動的部分。

對應的 <a href="https://github.com/servo/servo/pull/21015/files" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Pull Request</a> 是這一支，可以看到我改了兩個檔案，一個是 <code class="ha if ig ih ii b">htmltextareaelement.rs</code> 另個是 <code class="ha if ig ih ii b">cloning-steps.html.ini</code>。

<code class="ha if ig ih ii b">rs</code> 即為 Rust 檔案，顧名思義是處理 HTML text area element，所以針對這個檔案做改動。

<code class="ha if ig ih ii b">.ini</code> 檔比較特殊，他是指通過不了 WPT 測試（等等會介紹）的檔案，例如 <code class="ha if ig ih ii b">cloning-steps.html</code> 還通過不了，所以有 <code class="ha if ig ih ii b">cloning-steps.html.ini</code> 來記錄。因為這邊實作之後可以通過了，所以就把 <code class="ha if ig ih ii b">.ini</code> 檔案刪除。

總之這步驟就是將 issue 中所描述的問題解決，可能是除 bug，或是增加新功能。過程中碰到問題都可以在 issue 上發問。

## 單機測試

<a href="https://github.com/web-platform-tests/wpt" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Web Plateform Tests</a>(WPT) 是 W3C 的專案，針對目前網路文件的規範制定的測試，用意是確保大家都有乖乖遵守規範走。Chrome、Firefox、Safari、Edge 等主流瀏覽器，都會確保新的 commit 通過測試，才會合併進 master。

在 Servo 專案中，大多數的程式碼都會對應到 WPT 測試的某部分。例如你改了 Canvas 的相關程式碼，WPT 裡面就有關於 Canvas 的測試。

如果不清楚改動 Servo 的程式碼對應到的是什麼 WPT 測試，可以直接在 issue 或 PR 上發問。

而在其他專案中，可能會要求你針對改動的部分，寫新的 Unit Test，總之測試是為了證明自己改動的程式碼是有效的。

## 送出審查

你改好程式碼之後，就可以發 Pull Request(PR)，意思是希望你的改動可以被放進專案中。

首先將改好的 branch 先 push 進入自己倉庫，然後上 Github 自己的倉庫，點擊「New Pull Request」

<img class="dz t u gw ak" src="https://miro.medium.com/max/3996/0*OWYcLLCwDuDzTxFX.png" role="presentation"><br/>

接著會進入比較頁面，先選取你剛剛新改的 branch，這邊假設是 <code class="ha if ig ih ii b">fix</code>（記得要把你的改動上傳到 Fork 的 Repo）。

Github 會將你自己的 <code class="ha if ig ih ii b">fix</code> 這個分支與 servo 專案的 <code class="ha if ig ih ii b">master</code> 做比較。然後就可以點「Create new pull request」。

<img class="dz t u gw ak" src="https://miro.medium.com/max/3996/0*so1Dp8CPLRm-qmTI.png" role="presentation"><br/>

接著在專案的 Pull Request 頁面就會有你剛剛發出的新 PR，接著就等待 Reviewer 來審查。

在這邊要插題一下，一般的開源一個專案中都大概可以分為三種職位，分別為 Member、Commmiter 或 Reviewer、Contributor。Member 為專案核心成員，可以決定專案的方針，大型變動都必須有核心成員同意，以及審查新的核心成員。Commiter 或 Reviewer 有權限直接對專案存取，同時也為專案的審查者，負責審查新的 PR，但無決定專案走向的權限。Contributor 為一般的貢獻者，必須提交 PR 給 Reviewer 審查，審核通過 Patch 才會被合併進專案中。

Reviewer 會針對你的 PR 給建議，然後你會需要改進你的程式碼。當你的改動被審查者同意之後，審查者會給你一個<code class="ha if ig ih ii b">r+</code> 代表同意讓 PR 被合併了。以 Servo 專案來說，審查者會呼叫機器人 <code class="ha if ig ih ii b">@bors-servo r+</code> 告訴機器人他同意變動，讓機器人去跑下一步驟的自動化整合測試。

每個專案在這邊的步驟可能不太一樣，但核心概念就是你的補丁必須要有審查者同意才行。而行話術語 <code class="ha if ig ih ii b">r+</code> 代表核可，<code class="ha if ig ih ii b">r-</code> 代表否決，不過被否決別灰心，持續與審查者討論並修改，最後拿到 <code class="ha if ig ih ii b">r+</code>！

## 自動化整合

任何大型軟體的開發週期，都會有<a href="https://zh.wikipedia.org/wiki/%E6%8C%81%E7%BA%8C%E6%95%B4%E5%90%88" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">持續整合</a>（CI）的步驟，開源專案自然也不例外。簡單來說，持續整合就是確保新的變動，可以順利編譯，可以順利通過所有測試，通過所有檢測項目之後，變動才能被整合進專案中。

在 Servo 專案中，被 <code class="ha if ig ih ii b">r+</code> 的 PR，機器人會讓這個 PR 去跑 CI，在這個<a href="http://build.servo.org/grid" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">網站</a>中可以觀察測試的情況，測試項目包含：Linux、Windows、macOS、Arm 編譯、Linux 和 MacOS 上跑 web platform tests（WPT）、<a href="https://zh.wikipedia.org/wiki/%E6%A8%A1%E7%B3%8A%E6%B5%8B%E8%AF%95" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">模糊測試</a>、單元測試、nightly Rust 編譯。

解釋一下，因為 Servo 是跨平台瀏覽器，所以要確保每個平台都能順利編譯。WPT 先前解釋過，所有瀏覽器會遵從文件規範。測試 nightly Rust 是因為 Servo 和 Rust 相輔相成，所以要確保最新版的 Rust 能順利編譯 Servo。

## 進入主幹

當 CI 順利跑完沒有錯誤，程式碼就可以順利安全地合併到專案中。通常這個步驟都是自動化的，Servo 中也是由機器人負責這步驟。

假若 CI 過程中發現有測試過不了，就會回到送出審查的步驟，你必須重新提交新的正確程式碼，然後讓審查者重新認可。如此循環直到 CI 能順利通過，你的改動才會被合併到主幹中。

如果你的 patch 順利被 merge 進專案中，恭喜你，你現在已經是這個專案的貢獻者之一了！

## 結論

本文大致介紹如何加入一個開源專案，雖然是以 Servo 瀏覽器為例，但其實大多數專案的流程和思維都差不多。不過開源流程可能會有所差異，像是 Apache、Linux 這類的就是採用 Mail List 的協作方式，貢獻者會直接將 patch 寄給審查者，並不透過平台。而本文則是以 Github 平台開發為例，目前 Github 上已經有數百萬的專案了！

如果你有興趣加入開源專案，從小型的專案開始會比較容易，但若是你和我一樣喜歡挑戰大型專案，我認為 Rust、NodeJS、React、Angular 或是 Servo 都是不錯的選擇，他們都是 Github 開發，且社群活躍。社群活躍與友善度對一個新手來說非常關鍵，能不能得到適當幫助是最重要的事情！

我覺得參與開源專案很有意思，可以學習新的知識，對軟體開發更加熟練，學習和世界各國的開發者溝通，且當自己的貢獻成為數百、數千萬使用者的軟體的一部分也會非常有成就感。

我想開發軟體絕對不是難事，在社群、專案成員的幫助下，即使有困難也容易得到幫助，但難的是如何與人溝通，開發者來自不同國家，如何用英文正確表達想法、說服對方才是最不簡單的地方。

最後，開源是一種無償付出的精神，你不會有實質回饋，但你可能因為自己做了一件了不起的事而有成就感。開源講求熱情，唯有持續從成就感中獲得動力，才有力氣繼續無私地為社會貢獻。

願大家都能從開源中找到自己的熱情！ &#x1F60B;

## 參考與延伸

<ul>
<li id="95e0" class="fv fw em at fx b fy ht ga hu gc hv ge hw gg hx gi je ir is"><a href="https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">How Browser work</a></li><li id="9498" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is"><a href="https://ithelp.ithome.com.tw/articles/10197966" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">來做個網路瀏覽器吧！</a></li><li id="12b4" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is"><a class="dj by hy hz ia ib" target="_blank" rel="noopener" href="/@aboodman/c479ba623a1b">How Chromium Works</a></li><li id="e897" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is"><a href="https://shinglyu.github.io/web/2018/05/12/how-to-contribute-to-open-source.html" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">如何貢獻開源專案？</a></li><li id="76ca" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is"><a class="dj by hy hz ia ib" target="_blank" rel="noopener" href="/@tigercosmos/67da54c02e01">How I &amp; how a newbie to become a member of open source community?</a></li><li id="594d" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is"><a class="dj by hy hz ia ib" target="_blank" rel="noopener" href="/@tigercosmos/9eaf41e021f9">踏入 Mozilla Servo 兩個月的心得</a></li><li id="4db9" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is"><a href="https://ithelp.ithome.com.tw/articles/10192277" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Mozilla / Servo 瀏覽器引擎開發環境架設</a></li><li id="5b63" class="fv fw em at fx b fy it ga iu gc iv ge iw gg ix gi je ir is"><a href="https://www.slideshare.net/AnChiLiu/ss-97986413" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">瀏覽器開發與開源經驗</a></li>
</ul>

---

<span style="font-size: 26px; color: #696969; font-style:italic">關於作者 劉安齊 軟體工程師，熱愛寫程式，更喜歡推廣程式讓更多人學會。歡迎追蹤 微中子，我會在上面分享各種新知與最新作品，也可以去逛逛我的 個人網站 或 Github。</span>

<strong class="fx jt">關於作者</strong><em class="at"> </em><strong class="fx jt"><em class="at">劉安齊</em></strong><em class="at"> 軟體工程師，熱愛寫程式，更喜歡推廣程式讓更多人學會。歡迎追蹤 </em><a href="https://www.facebook.com/CodingNeutrino/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow"><strong class="fx jt"><em class="at">微中子</em></strong></a><em class="at">，我會在上面分享各種新知與最新作品，也可以去逛逛我的 </em><a href="http://tigercosmos.xyz/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow"><strong class="fx jt"><em class="at">個人網站</em></strong></a><em class="at"> 或 </em><a href="https://github.com/tigercosmos" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow"><strong class="fx jt"><em class="at">Github</em></strong></a><em class="at">。</em>