---
title: Windows 平台打造極致の程式開發工作環境 
date: 2020-06-14 00:00:00
tags: [windows, 工作環境]
---

## 前言

老實說，過去我曾經是 Linux 和 Mac 的忠實用戶，覺得 Unix 才是工程師最舒服的工作環境。但隨著 Windows 近年來的進步，加上我頻繁切換使用 Windows、Mac、Linux，對我來說作業系統其實沒啥差別，就像同時會講好多種語言一樣，視情況和環境使用而已。

我覺得王垠「[谈 Linux，Windows 和 Mac」(https://www.yinwang.org/blog-cn/2013/03/07/linux-windows-mac)>的論點跟我想法很像，說到底就是使用者體驗好不好的問題，過去 Windows 開發體驗真的很差，但現在我覺得用起來挺方便的，程式開發已經滿足我需求，加上平常還需要用 Unity、Adobe、Visual Studio、打 LOL 這些都是僅限 Windows 的程式，所以主要時間都在 Windows 上了。

但我覺得許多同學的 Windows 都沒有調校到最好用的狀態，我常常幫同學看問題時，用他們的 Windows 覺得很訝異，天啊！好用的工具怎麼在你電腦上都沒有？或是你竟然不知道可以這樣用？

為此來介紹一下我的 Windows 工作環境長怎樣。

## Windows Subsystem for Linux

Windows Subsystem for Linux (WSL) 讓你在 Windows 底下不需要開虛擬機 (VM) 或 Docker 就可以直接跑 Linux。

![WSL](https://user-images.githubusercontent.com/18013815/84588789-c85d3f80-ae5c-11ea-9d40-4a9395456e35.png)


安裝細節可以參考「[Windows Subsystem for Linux Installation Guide for Windows 10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)」，或是搜尋一下網路上別人分享的中文教學。

WSL 有啥好處呢？

以前 Windows 最讓人詬病的是環境設定、安裝程式、跑程式都很麻煩，舉例來說要安裝各種函式庫在 Ubuntu 底下只要 `apt install` 就好了，但在 Windows 底下要把 tool chain 弄起來真的要人命。不過近年來有類似 Chocolate 的工具可以簡化這些流程了，不過在此不討論。還有 Unix 有很多實用小工具，向是 `curl`、`wget`、`gcc`、`make`，這些東西不是在` Windows 下不能裝，但步驟繁瑣的要命。

不過 WSL 解決這最根本的問題了，我現在有需要跑的東西，如果他是跨平台的，那我就選擇採用 Linux 版，直接在 Windows 下呼叫 WSL 進入 Linux 殼層，像是 curl 一個檔案，或是簡單用 gcc 編譯一個 c 程式。使用起來的感覺很像用 Docker 或 VM 開共享資料夾，總之因應特定需求可以快速切換系統來達成目標。

有了 WSL 實在沒必要多搞一個 VM，不過有時候為了能重複在乾淨環境下測試，還是會用的到 VM 或 Docker 就是了。

## 文字編輯器 & IDE

拜託不要再用 Notepad++ 了 (用記事本的...)，那真的不適合寫程式，只能拿來寫 Hello World。

我最推薦用 [VSCode](https://code.visualstudio.com/) 做一般程式開發，基本上他是文字編輯器但也可以當作是半個 IDE，整合查詢、版本控制、可擴充外掛，讓 VSCode 輕量下又非常強大。

![VSCode](https://user-images.githubusercontent.com/18013815/84588950-0eff6980-ae5e-11ea-9b9c-39da3a6654d5.png)

我最喜歡他的部分是他完美整合 Git，每次改完程式碼可以很速辨識更動部分和要 commit 那些檔案。VSCode 也有各種好用的外掛，可以應付各種使用需求，像是程式語法檢查、拼字檢查、風格建議等，VSCode 目前也是全世界開源貢獻者最多的地方，無人能敵。

VSCode 還有一個超級強大的功能，他現在可以打開遠端 Linux Server 的工作目錄，等於你在 Windows 下打開 VSCode 編輯程式，用終端機下指令，用起來跟在 Linux 下開發一模一樣。

IDE 我個人沒太大偏好，但地表最強大 Visual Studio 你應該是一定會安裝的 (因為各種開發都會使用到他的 Tool Chain)，VS 的 Debugger 真的很好用，CGDB 或 GDB 是滿好用的沒錯，但都比不上 VS Debug 方便。

基本上就算我在開發 Visual Studio (VS) 或 Unity，我也都是拿 VSCode 來改 Code，VS 只會拿來做編譯和除錯。

## Python 環境

Python 我都會用 [Anaconda](https://docs.anaconda.com/anaconda/install/windows/) 安裝，這是一個 Python 管理套件，可以建立多種開發環境。如果直接下載 Python 的 Windows 安裝檔還要自己去改環境變數，而且很容易壞掉。細節可以去查一下 Anaconda 使用教學。

用 Anaconda 弄好一個 Python 環境之後，假設是 Python 3.7，一般開發小程式，如機器學習、NLP 這類型的，我會使用 [Jupyter Notebook](https://jupyter.org/) 來做快速測試開發，Jupyter 讓你可以把程式切成好多小區間，每個小區間會保留跑完的狀態。好處是像是在弄機器學習的時候常常只需要改某幾行 Code 的參數做測試，這時候 Jupyter 讓你只需要改動和重新跑那一個小區間，不需要重新跑全部的程式碼。當你用 Jupyter 一個區塊一個區塊測試好之後，再一次直接用 Python 執行程式碼。

```shell
$ pip install jupyter # 安裝
$ jupyter notebook # 開啟
```

## 終端機

傳統的 CMD 很好用，新版的 Power Shell 也不錯。不過最近微軟開發了新的 [Terminal](https://aka.ms/terminal)，可以開新分頁，每個分頁還可以決定背後要用哪一個 Shell (CMD, Power Shell, Linux)。

![Terminal](https://i.imgur.com/jUtCktp.png)

當然也有很多其他好用的 Terminal 可以用，像是 [Cmder](https://cmder.net/) 這款終端機我也覺得很好用。總之如果只是用原生的 CMD 或 Power Shell 那就少了許多方便好用的功能囉。

此外，你知道按住 `Shift` 點右鍵，可以直接在當前目錄叫出終端機嗎？

## Windows 內建小工具

好像很多人不知道其實 Windows 本身就有好用的小工具。

附屬應用程式底下的擷取工具 (Snipping Tool) 可以讓你輕鬆截圖。

想要截圖的時候，如果來不及開擷取工具，可以按住 PrintScreen 鍵，然後開啟小畫家，`Ctrl + v` 把截圖貼在小畫家上再做修改。

在設定中開啟 Windows 的遊戲模式之後，在你想錄影的程式視窗底下，可以用 `Win + G` 開啟錄影工具，錄製當前程式畫面的操作。

Windows 其實內建壓縮工具，如果沒有 RAR 需求的人不需要特地裝壓縮工具，但裝 WinRAR 也沒啥不好，畢竟他也不肥又滿好用的，除了每次都會跳廣告很煩。

另外你知道使用注音輸入法，按下 `Ctrl + Alt + <` 可以叫出標點符號嗎？
而 `Win + .` 可以叫出表情符號喔！

## 網頁瀏覽器

基本上我都會裝 Chrome + Firefox，這樣裝是有學問的。

因為 Firefox 內建 Proxy 但 Chrome 沒有，所以我 Firefox 會設定 Proxy 綁定實驗室 Server，當我需要用學校 IP 搜尋論文時，只要開啟 Firefox 就好，不需要在 Windows 下開啟和關掉 Proxy。

但平常又不需要一直開著 Proxy 上網，這時候就會用 Chrome 滿足一般需求。不過 Chrome 輸入法很有問題，會一直吃字，所以需要打字的時候我就會切回用 Firefox。

## 結語

以上就是我的小小分享，Windows 其實可以很方便的，讓你的工作環境更方便吧！

如果還有任何我沒分享到的好用工具或方法，歡迎留言寫信告訴我！
