---
title: 第一次 Probot 開發 Github App 就上手
date: 2018-06-02 00:00:00
tags: [Chinese Posts,English Posts,Probot,Github App,Bot,Chinese,]
---


## <strong class="bf">第一次 Probot 開發 Github App 就上手</strong>

The First Time Developing Github App via Probot

<img class="dz t u gw ak" src="https://miro.medium.com/max/3200/0*UZk2Fw5ruoYQ6qbJ.png" role="presentation"><br/>

## 前言

最近在開發<a href="https://github.com/weather-bot/weather-bot" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">氣象機器人</a>的時候，為了要促進工作流程的效率，不得不加入 bot（機器人） 進來工作流程。所以就邊研究邊實做了一個，在此記下開發心得。

Github 上的 bot 專有名詞稱為 Github App，其實原理跟 Line Bot、Messenger Bot 等等都差不多。

你可能在大型開源專案上看過以下情況：

範例一：<a href="https://github.com/servo/servo" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Servo</a> 專案 bot 對 Pull Request（PR，此文之後皆採縮寫） 的回應，其中 taskcluster 是回報持續整合測試結果，highfive 則會檢查 PR 的程式碼改動有沒有附上測試的程式碼。

<img class="dz t u gw ak" src="https://miro.medium.com/max/3876/0*D6pR4AFqmQFfS51l.png" role="presentation"><br/>

範例二：<a href="https://github.com/web-platform-tests/wpt" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">WPT</a> 專案是跨平台網頁測試，基本上所有瀏覽器都會用此測試當標準。下圖顯示 Chromium 的 bot 自動將新的 patch 送到 WPT 專案做檢查，wpt-pr-bot 跑完測試通過之後，Approve 這個 PR。

<img class="dz t u gw ak" src="https://miro.medium.com/max/3800/0*_hJyEWwr-7Yy-0N_.png" role="presentation"><br/>

好的，所以我們看到 bot 可以有效加速開發者的流程，幫我們省去很多麻煩事。事實上他還能做更多事，只要是你懶得做的，bot 一定都辦得到。例如每次有新的 PR，自動標註負責人，或是想要自動替 issue 或 PR 加標籤等等工作。

先來看看我開發的 bot — — <a href="https://github.com/weather-bot/snow-girl" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Snow Girl</a>。她是用來讓使用者可以在氣象機器人的 PR 中，將 PR 版本的程式碼送進測試機 Build，然後測試機就會是 PR 版的氣象機器人。因為即使有寫測試，有時候還是會有意外，所以有跟<strong class="fx il"><em class="im">正式版</em></strong>一樣設定的<strong class="fx il"><em class="im">測試版</em></strong>，可以供上線前人工做確認：

<img class="dz t u gw ak" src="https://miro.medium.com/max/3780/0*wwPX_NzBwznizKG3.png" role="presentation"><br/>

## 什麼是 Probot？

<a href="https://probot.github.io/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Probot</a> 是一個專門為 Github App 設計的框架，bot 的原理背後都是串連 Webhook，自己弄底層的話就是要串接、處理一堆 API 真的很麻煩，有框架當然拿來用，此外沒有框架的結果，其實就是自己會寫出跟框架差不多的東西，所以說沒必要自己造輪子。

開發方式也很簡單，如果你寫過 NodeJS 會覺得非常親切。

## 設定步驟

1、 NodeJS 版本必須為 8.3 之上

<img class="dz t u gw ak" src="https://miro.medium.com/max/2564/0*Nzy4HdV7WF1n0YRy.png" role="presentation"><br/>

2、輸入 <code class="ha ir is it iu b">npx create-probot-app my-first-app</code> 照著提示輸入資訊即可，然後就會看到路徑建立好 <code class="ha ir is it iu b">my-first-app</code> 資料夾，裡面檔案都幫你準備好了，包含 <code class="ha ir is it iu b">index.js</code>、<code class="ha ir is it iu b">package.json</code>等。

<img class="dz t u gw ak" src="https://miro.medium.com/max/4000/0*FR_Y3T8S9Hnk0pdF.png" role="presentation"><br/>

3、先進入 <code class="ha ir is it iu b">my-first-app</code> 專案，首先將 <code class="ha ir is it iu b">.env.example</code> 改名為 <code class="ha ir is it iu b">.env</code>

4、去 <a href="https://smee.io/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">smee.io</a>，點選首頁中間的「Start a new channel」，然後把得到的 Webhook Proxy URL 拷貝，在 <code class="ha ir is it iu b">.env</code> 裡面的 <code class="ha ir is it iu b">WEBHOOK_PROXY_URL</code> 貼上連結。使用 Proxy 的好處是，你可以用 Local 進行開發，也不需要真的有實體 IP。

5、接下來我們要去<a href="https://github.com/settings/apps/new" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">申請建立 Github App</a>（要注意，這邊會進入個人設定頁面的建立，，假設你只想讓 Github App 只給特定組織使用，你必須從組織的設定去建立）。

<ul>
<li id="07fb" class="fv fw em at fx b fy fz ga gb gc gd ge gf gg gh gi ix iy iz">Webhook URL: 填上剛剛得到的 <code class="ha ir is it iu b">WEBHOOK_PROXY_URL</code></li><li id="0098" class="fv fw em at fx b fy ja ga jb gc jc ge jd gg je gi ix iy iz">Webhook Secret：填上 <code class="ha ir is it iu b">development</code>（也可以自訂啦）</li><li id="4af7" class="fv fw em at fx b fy ja ga jb gc jc ge jd gg je gi ix iy iz">Permissions &amp; events：看你想要讓 Github App 可以做到什麼事情，欄位都有說明，可以自己選擇。例如想要讓 bot 可以查看、編輯 issue，issue 欄位就要勾選「Read &amp; Write（可讀寫）」。這邊我們練習用的話，把所有 issue 關鍵字都勾選可讀寫。</li>
</ul>

6、在 <code class="ha ir is it iu b">.env</code> 填上 <code class="ha ir is it iu b">APP_ID</code>，可以在組織/個人的「Setting」，底下的「Github App」中，點選剛剛建立的 App，進去之後在「General」最底下就可以看到 ID 啦，此外也可以在這邊重新點選要求的權限。

<img class="dz t u gw ak" src="https://miro.medium.com/max/4000/0*cU2hQ59kMzSmTZti.png" role="presentation"><br/>

7、在同一個頁面下找到「Private keys」，點下載會有 <code class="ha ir is it iu b">xxx.pem</code> 的金鑰檔，把他放入專案裡面，此外雖然 <code class="ha ir is it iu b">.gitignore</code> 有排除 <code class="ha ir is it iu b">*.pem</code>，但千萬不要不小心進入 commit。

8、再來要把剛剛建立的 App 安裝，進入你的 App 頁面 <code class="ha ir is it iu b">https://github.com/apps/你的APP名稱</code> 中點「Install」。

9、終端機進入專案，輸入 <code class="ha ir is it iu b">npm start</code>，你應該會看到類似：

```undefined
$ npm start

> snowgirl@1.0.0 start /Users/tigercosmos/Desktop/snowgirl
> probot run ./index.js

13:00:53.203Z  INFO probot: Yay, the app was loaded!
...
```

## 開發 bot

一開始 <code class="ha ir is it iu b">index.js</code> 裡面長這樣

```javascript=
module.exports = (robot) => {
  // Your code here
  robot.log('Yay, the app was loaded!')
  
  // For more information on building apps:
  // https://probot.github.io/docs/
  
  // To get your app running against GitHub, see:
  // https://probot.github.io/docs/development/
}
```

框架採用模組的載入的形式，所以程式碼就這麼簡單！

## 接收 Webhook

我們可以改成這樣：

```javascript=
module.exports = robot => {
  robot.on(['issues.opened', 'issues.edited'], async context => {
    console.log(context.payload.issue.user.login)
  })
}
```

先講解上半段，這樣代表說，issue 被新開或是被編輯的時候，Webhook 就會通知並產生 <code class="ha ir is it iu b">context</code>。其中 <code class="ha ir is it iu b">issues.opened</code> 是由 <a href="https://developer.github.com/v3/activity/events/types/#issuesevent" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">Github Webhook Doc</a> 中去查。格式為 <code class="ha ir is it iu b">name.action</code>，就是我圖中圈起來的部分。

<img class="dz t u gw ak" src="https://miro.medium.com/max/2812/0*BaOuWz5aUNYH8DkY.png" role="presentation"><br/>

然後我去讀這個被更動的 issue 的內容是由誰發佈的（<code class="ha ir is it iu b">context.payload.issue.user.login</code>）。

Context 完整說明可以在<a href="https://probot.github.io/api/latest/Context.html" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">官網文件</a>中查到，不過我覺得寫得很難懂，所以我直接 <code class="ha ir is it iu b">console.log</code> 看會出現什麼。

## 讓 bot 對 Github 做改動

在繼續前，這邊要解釋一下 Github webhook event name 中什麼是 <code class="ha ir is it iu b">issue_comment</code>。我看了文件很久，想破頭為什麼沒有一個叫做 <code class="ha ir is it iu b">pull_request_comment</code>，也就是在 PR 下面留言。最接近的頂多叫 <code class="ha ir is it iu b">pull_request_review_comment</code>，但他是指直接在 PR 程式碼上面留言。

後來我知道原來不管是 issue 或是 PR，底下的留言通通叫做 <code class="ha ir is it iu b">issue_comment</code>，希望大家別踩雷了！

接下來我們可以把程式碼改成：

```javascript=
module.exports = robot => {
  robot.on('issues.opened', async context => {
    // 自動根據這個 context 把資料包裝
    const params = context.issue({body: 'Hello World!'})
    // 讓 bot 新建一個留言
    await context.github.issues.createComment(params)
  })
}
```

上面那段程式碼可以讓 bot 在 issue 被打開的時候，在底下留言說 <code class="ha ir is it iu b">Hello World!</code>。更多用法可以看<a href="https://probot.github.io/docs/github-api/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">文件</a>，還可以做到替 issue 加標籤、自動 assign 人、修改程式碼、編輯 PR 內容等等。

此外要小心的是，如果是這樣寫：

```javascript=
robot.on('issue_comment.created', async context => {
    const params = context.issue({body: 'Hello World!'})
    await context.github.issues.createComment(params)
  })
}
```

意思是，當有 PR 或 issue 有人留言，bot 就留言。然後就悲劇了！因為 bot 看到 bot 留言，bot 就繼續留言⋯⋯。所以這種情況要寫判斷，讓他不會陷入無窮迴圈中。

此外還可以這樣寫：

```javascript=
robot.on('issue_comment.created', async context => {
    const params = context.issue({body: '要開始工作囉！'})
    await context.github.issues.createComment(params)
    // 做了一些事情後
    const params = context.issue({body: '工作做完了！'})
    await context.github.issues.createComment(params)
    // 記得加判斷條件避免無窮迴圈
  })
}
```

善用 <code class="ha ir is it iu b">async</code> 和 <code class="ha ir is it iu b">await</code>，可以做到按步驟的對 Github 操作，切記 JS 是異步執行的語言，直接多個執行 <code class="ha ir is it iu b">context.github.XX()</code> 會導致順序錯亂！

改好之後，記得在用 <code class="ha ir is it iu b">npm start</code> 開始伺服，上 Github 的 issue 或 PR 做你規則的動作，看結果有沒有反應喔！

## 結論

用 Probot 建立 Github App 真的很簡單喔！善用 bot 可以讓專案進行得更有效率，Probot 有一個展示大家 bot 的<a href="https://probot.github.io/apps/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow">廣場</a>，也可以裝幾個玩玩看。最後有問題歡迎問我。

---

<span style="font-size: 26px; color: #696969; font-style:italic">關於作者劉安齊 軟體工程師，熱愛寫程式，更喜歡推廣程式讓更多人學會。歡迎追蹤 微中子，我會在上面分享各種新知與最新作品，也可以去逛逛我的 個人網站 或 Github。</span>

<strong class="fx il">關於作者<br><em class="at">劉安齊</em></strong><em class="at"> 軟體工程師，熱愛寫程式，更喜歡推廣程式讓更多人學會。歡迎追蹤 </em><a href="https://www.facebook.com/CodingNeutrino/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow"><strong class="fx il"><em class="at">微中子</em></strong></a><em class="at">，我會在上面分享各種新知與最新作品，也可以去逛逛我的 </em><a href="http://tigercosmos.xyz/" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow"><strong class="fx il"><em class="at">個人網站</em></strong></a><em class="at"> 或 </em><a href="https://github.com/tigercosmos" class="dj by hy hz ia ib" target="_blank" rel="noopener nofollow"><strong class="fx il"><em class="at">Github</em></strong></a><em class="at">。</em>