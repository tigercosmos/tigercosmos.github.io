---
title: Mozilla / Servo 瀏覽器引擎開發環境架設
date: 2017-12-19 21:45:06
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
連續好幾天比較硬的解說文章，今天插入一篇比較輕鬆的文章。雖然是介紹 Servo，其實本篇也可以當作 Rust 的環境架設，因為使用 Rust 第一名的專案是 Servo，你說呢？ＸＤ

## Servo
> 此專案由 Mozilla 贊助，並以全新的系統級程式語言 Rust 編寫，Servo 專案旨在實現更好的平行化、安全性、模組化以及高效能。 

想了解更多可以進[官網](https://servo.org/zh-TW/index.html)看，開玩笑的 030 ，想從官網了解還不如訂閱我的文章 XD 我是說真的，官網真的沒啥內容，不過還是要推銷一下，因為是我翻譯的喔！

Servo 詳細在幹嘛，技術細節、突破留到以後的文章再說。 汪！汪！

![servo](https://download.servo.org/doge-tiny.png)

## Rust
因為 Servo 幾乎都是用 Rust 寫的，所以我們很大部分在設定語言的環境。
> Rust是一個由 Mozilla 主導開發的通用、編譯型程式語言。它的設計準則為「安全，並行，實用」支援函數式、平行化、程序式以及物件導向的程式設計風格。

## Envornment
安裝 [Servo](https://github.com/servo/servo) 的環境參考 `README` 做就好，因為各系統做法差異很大，直接照文件做最快。不過這邊還是貼上 macOS, Ubuntu, Windows 的做法。

### 取得 Servo
```
git clone https://github.com/servo/servo
cd servo
```

### macOS
首先你要有 `brew`，可以透過 App Store 下載 XCode，就會順便一起裝了
```
brew install automake pkg-config python cmake yasm
pip install virtualenv
brew install openssl
export OPENSSL_INCLUDE_DIR="$(brew --prefix openssl)/include"
export OPENSSL_LIB_DIR="$(brew --prefix openssl)/lib"
```
```
./mach build -d
```

### Ubuntu
```sh
sudo apt install git curl freeglut3-dev autoconf libx11-dev \
    libfreetype6-dev libgl1-mesa-dri libglib2.0-dev xorg-dev \
    gperf g++ build-essential cmake virtualenv python-pip \
    libssl1.0-dev libbz2-dev libosmesa6-dev libxmu6 libxmu-dev \
    libglu1-mesa-dev libgles2-mesa-dev libegl1-mesa-dev \
    pulseaudio dbus-x11 libavcodec-dev libavformat-dev \
    libavutil-dev libswresample-dev  libswscale-dev libdbus-1-dev \
    libpulse-dev clang
```
```
./mach build -d
```

### Windows
原本文件是寫裝 VS2017，這邊我建議裝 [VS2017 build tool](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=15) 就好。這是我花很多時間得出的心得，官方文件的這個方案也是我改的。不過後來我都不用 Windows 開發了。

1. 下載安裝 Build Tools for Visual Studio 2017
1. 安裝 python2.7 x86-x64 and `pip install virtualenv`
1. `Run mach.bat build -d` 就可以編譯了

## Rust
### Rust
1. 用 `rustup` 工具下載安裝最快，等同 `nvm` 安裝 `node`
   ```sh
   `curl https://sh.rustup.rs -sSf | sh`
   ```
1. `rustup` 來安裝 `rust` `2.1.1` 版本
    ```sh
    rustup install 2.1.1
    ```
### IDE
- 下載 [VSCode](code.visualstudio.com)，你當然可以用 Vim，但以下的功能就通通不能用
- 在外掛中安裝 Rusty Code

`cargo` 是 `rust` 的套件管理器，這邊我們要安裝 `racer` 才能自動提供語法建議
- `cargo install racer`
安裝 `rustfmt` 是自動對齊程式碼的工具，讓之後 VScode 支援「自動對齊」動作
- `cargo install rustfmt`

為了讓 `racer` 可以正常執行，我們要取得 `Rust` 的 repo，我們把它放在 home
```
cd ~
git clone https://github.com/rust-lang/rust.git
```

接者更改 VSCode 的 `setting.json`，左下角有個齒輪，點擊就可以看到。加入這兩行。
```
{
  "rust.rustLangSrcPath": "/Users/XXXX/home/rust/src",
  "rust.formatOnSave": true
}
```

- 最後在 VSCode 外掛下載 TOML extension，讓他可以支援 `.toml` 檔案。這相當於 node 中 `json` 的功能。

---

接著你就可以享受 rust 的 IDE 環境囉！開發 Servo 也變更加輕鬆，事實上因為 Servo 檔案已經非常多，不使用智慧連結的功能找函數定義會找到死，此外語法支援對開發來說只會更方便。

希望對大家有幫助，大家明天見！


