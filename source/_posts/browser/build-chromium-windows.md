---
title: 在 Windows 上編譯 Chromium
date: 2020-02-17 22:56:34
tags: [chromium, browser, 瀏覽器, windows,]
---

Chromium 是 Chrome 的開源版本，與 Chrome 差異是 Chrome 多了一些 Google 服務，並且介面設計上也會不太一樣。Chromium 因為是開源軟體，所以被許多其他瀏覽器開發商拿來改造，像是 MicroSoft Edge、Opera、Puffin 等瀏覽器，而 Chromium 底下的 V8 JavaScript 引擎則被 NodeJS 使用。

<!-- more --> 
為甚麼要編譯 Chromium 呢？

> 因為很酷很爽很好玩啊！

Chromium 是一個百萬行程式碼等級的專案，編譯時可以看到 CPU 被操爆，就會有莫名的愉悅感，而我特地買了 16 核心的 CPU 不就是為了享受極致編譯的快感嘛！

此外感受一下，現代高科技 (瀏覽器) 是怎樣被編譯出來的，應該也很有意思的，推薦搭配「[《來做個網路瀏覽器吧！》](/post/2018/02/browser/browser_series_33/)」一起享用。

不過編譯這種大型專案最令人恐懼的不外乎是編譯卡關，因為程式碼數量龐大，稍微有個小環節有問題也很難找到根源，最怕的就是明明都照著說明步驟走，結果還是編譯不過，也不知問題出在哪。

Chromium 的流程已經簡化的滿簡單了，基本上裡面的腳本已經替我們處理好很多事情了，之前在 Linux 和 MacOS 上都試過，基本上都照著指令打就沒問題。不過在 Windows 上我是第一次編譯，所以還是卡了滿久的，這篇記錄我編譯的流程。

本文可能隨著時間與最新版不太一樣，請以[官方的指南](https://chromium.googlesource.com/chromium/src/+/master/docs/windows_build_instructions.md)為準。

## 前置動作

1. 先下載 VS2019，選擇社群版本(community)，可以的話建議裝英文版就好，因為比較好跟官方文件用的名字對照。
    
    VS 會有個安裝工具，主頁勾選「Desktop development with C++” component (桌面開發 C++)」，然後去個別元件的選單，Windows SDK 勾選最新的，此外搜尋「MFC」、「ATL」都勾選最新版本。如果你是 AMD 的裝置，AMD 支援相關的元件最好也都勾選。

2. 此外你需要手動安裝「[Debugging Tools For Windows](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/)」。

3. 接著你會需要安裝「[depot_tools bundle](https://storage.googleapis.com/chrome-infra/depot_tools.zip)」，這是 Chromium 開發用的一些工具程式，會需要用它來抓 Chromium 程式碼和編譯。

4. 然後要修改環境變數，左下角 Windows 選單點擊齒輪(設定)，搜尋「環境變數」，並以系統管理員身分修改。假設你把 `depot_tools` 解壓縮在 `C:\src\depot_tools`，那環境變數 `PATH` 中把這個路徑加進去，記住要把這個路徑放在第一條，以免你的系統中已經有 Python 或其他工具干擾編譯。此外在環境變數新增 `DEPOT_TOOLS_WIN_TOOLCHAIN` 並設為 `0`。

之後編譯的時候盡量用原生的 `cmd` 來做事，使用其他的 shell (cygwin、PowerShell) 可能都會出問題。

## 取得 Code

先設定一下 Git：

```shell
$ git config --global user.name "My Name"
$ git config --global user.email "my-name@chromium.org"
$ git config --global core.autocrlf false
$ git config --global core.filemode false
$ git config --global branch.autosetuprebase always
```

建立資料夾作為 Chromium 的專案資料夾：

```shell
$ mkdir chromium && cd chromium
```

用 `depot_tools` 來拿程式碼：

```shell
$ fetch chromium
```

如果不要歷史紀錄的話，可以加上 `--no-history` 會下載比較快，如果你是要提交 patch 的話，就一定要有完整歷史紀錄，反之只是編譯好玩就可以加上這條參數。但如果想編譯穩定釋出版本，還是要有歷史紀錄，我個人認為不趕時間的話，還是把歷史紀錄都抓下來。

```shell
$ cd src
```

進入 `src` (fetch 後就會有)，以下的所有操作都在 `src` 裡面。

由於 Chromium 是一個快速開發的專案，每天都會有幾百條 commit 進入 master，直接編譯當前最新 commit 的版本很可能會出問題，所以我們要切換成穩定釋出版本，我的作法是選擇當下 Chrome 最新的穩定版本號。

以下為切換版本的指令，更多細節可以參考[這篇](https://www.chromium.org/developers/how-tos/get-the-code/working-with-release-branches)。

```shell
$ gclient sync --with_branch_heads --with_tags
$ git fetch --tags
$ git checkout -b my_branch tags/80.0.3987.106
$ gclient sync --with_branch_heads --with_tags
```

這邊的 `80.0.3987.106` 是 Chrome 正式版本 (你可以打開 Chrome 去設定查當下最新版本號)，`tags` 會自己去抓那個版本 tag 對應的 commit 是哪一條。

## 編譯

Chromium 使用 Ninja 來編譯，首先需要用 GN 工具來產生設定檔：

```shell
$ gn gen out/Default
```

`Defualt` 可以是任何你想要的名字，也可以用 `Debug` 來設定除錯版本。

官方指南有更多參數設定上的建議。

接著就是開始編譯：

```shell
$ autoninja -C out\Default chrome -j16
```

`autoninja` 會自動設定參數去執行 `ninja`，而 `ninja` 則是類似 `make` 的編譯工具，我們靠它編譯和連結 Chromium，`-jN` 則是你電腦的核心數量。

我編譯時，可能是 Python 沒有用 `depot_tools` 裡面的，編譯到一半他說缺某個 module，於是我就手動 `pip install` 那個 module，然後就順利編譯了。

編譯完後就能執行啦！

```shell
$ out\Default\chrome.exe
```

![chromium image](https://user-images.githubusercontent.com/18013815/74681074-69185700-51fd-11ea-8504-0a775aebeb37.png)
