---
title: 來寫個氣象機器人吧！
date: 2018-05-21 00:00:00
tags: [weather bot,氣象機器人,bottender,line bot,]
---


## 來寫個氣象機器人吧！

### Let’s build a weather bot!

<img class="dz t u go ak" src="https://miro.medium.com/max/1156/1*FxN3aWN-o00AWTTi-ezajg.png" role="presentation"><br/>

## 簡介

沒有人會懷疑了解天氣的重要性，我們總是看氣象預報或查天氣來決定等下外出時要不要帶傘，衣服要穿多厚是否需要帶件外套，或是需不需要先擦防曬油戴一副墨鏡出門等等。

想查天氣的時候我想大部分人可能就是 Google 一下、上中央氣象局網站、使用 APP、看新聞。或是有種很潮的做法是問 Siri，不過效果可能不太好 ⋯⋯。

<!-- more --> 

<img class="dz t u go ak" src="https://miro.medium.com/max/1288/0*6g3mklj9wFm9l0Lf.png" role="presentation"><br/>

其實還有一種做法是建立一個<a href="https://www.facebook.com/WxKitty.tw" class="dj by im in io ip" target="_blank" rel="noopener nofollow">天氣機器人</a>，其實概念就是聊天機器人，讓我們可以和機器人對話取得天氣資訊。你可能會問那和查 App 或問 Siri 差在哪裡呢？首先氣象機器人因為著重在氣象資訊上，所以資料處理非常細膩，尤其是台灣地區的資料是處理得非常完善，並且國外地區也支援。再來就是聊天機器人最好玩的地方就是，大家可以一起跟機器人對話，這也是聊天機器人最好玩的地方！

<img class="dz t u go ak" src="https://miro.medium.com/max/2024/0*3vi3cauDUIUA6ycS.png" role="presentation"><br/>

機器人在群組中可以和大家一起互動，當有人提到天氣資訊的時候，機器人會自動回應，不僅少了查詢的時間，大家也都能一起得到氣象資訊。此外也可以做個人查詢使用，並且支援跨平台，可以在 Line 或 Messenger 甚至其他聊天軟體上使用。

氣象機器人的專案名稱是<strong class="ht iv">「氣象喵</strong>」，可以先玩看看，第一次使用請先輸入 <code class="gt iw ix iy iz b">help</code> 來查看指令：

<ul>
<li id="3b97" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie ja jb jc"><a href="https://line.me/R/ti/p/%40lbz9453s" class="dj by im in io ip" target="_blank" rel="noopener nofollow">氣象喵 Line Bot 連結</a></li>
</ul>

接下來我會介紹如何建立一個氣象機器人，一一介紹聊天機器人建立、使用 Bottender 框架、部署、比較細節的設定、氣象資料的來源和處理。本篇屬於進階的探討文章，基礎的部分不會特別著墨，但我會將需必備的基礎資料都提供給大家。

## 如何建立機器人

想要建立一個氣象機器人，最重要的當然就是先有個機器人（bot）。一般的聊天機器人原理大致都相同，你會需要建立一個伺服器，就類似網頁伺服器一樣，只是現在是伺服機器人。然後伺服器可以透過 Webhook 機制與聊天平台溝通，聊天平台藉由 Webhook 中的要求傳送給平台使用者。舉例來說，當某個人傳訊息給機器人，聊天平台的伺服器就會知道，並且透過 API 傳訊息告訴你的伺服器，說有人傳訊息給你喔！你的伺服器經過一番處理之後，可以呼叫 API 告訴聊天平台說，請讓機器人回覆他「xxxxx」，這個過程就是所謂 Webhook 了。

由於我想做跨平台的機器人，意味者要能在 Line、Messenger、Telegram、Slack 等等聊天平台上都能使用，但是每家平台的 API 都不盡相同，每個平台都要特別去針對他來改真的很麻煩，最佳的實作方式是使用框架（framework）當作底層，待會會細談。我們先來看怎麼申請、寫簡單的機器人吧！

這邊我針對 Line 和 Ｍessenger 一起做介紹，Slack、Telegram 等等其他的由於我沒有去實作（考慮到使用人數的效益）以及原理和做法其實也不會差太多，就留給大家自行查詢了。

## Line Bot

想使用 Line Bot 的話，要先申請 <a href="https://developers.line.me/en/" class="dj by im in io ip" target="_blank" rel="noopener nofollow">Line@</a> 帳號，可以參考 OOXX 寫的 <a href="https://www.oxxostudio.tw/articles/201701/line-bot.html" class="dj by im in io ip" target="_blank" rel="noopener nofollow">LINE BOT 實戰 ( 原理篇 )</a>。這篇介紹非常完整，照著文章步驟，使用 NodeJS 可以快速建立一個 Hello World Bot。這邊可以試著寫一個，或是等下會介紹用框架來做。

Line Bot 建立非常方便，如果要開放公開給大家使用也很容易，只要讓別人加你的機器人好友就好。完全不需要其他的審查或申請（除非要申請認證帳號），相較於 Messenger 可說是非常友善。不過免費帳號只能夠「回應」，不能讓機器人主動「推播」，這是與 Messenger 非常不同的地方，如果要做到跨平台且都支援主動推播，就只好買付費服務了。

另外 Line Bot 所有 Post API 只接受內容為 HTTPS 的 URL，例如你要傳送圖片給使用者，你可以在 API 中附上圖片的 URL，但必須是 HTTPS 的連結，如果是 HTTP 的話，Line Bot 會不反應，且不會報錯誤訊息。希望大家不要在這地方被雷到了。

## Messenger Bot

Messenger Bot 相較於 Line Bot 來說更加強大，因為他有更多 API 可以呼叫，它支援語意分析等服務。不過 Messenger Bot 不直接支援群組聊天（可以透過外掛辦到），並且申請步驟真的煩瑣很多。首先要用 Messenger Bot 的話要申請 Facebook Developer，並且申請開發應用服務，並且機器人必須綁定一個粉絲專頁。詳細申請步驟可以參考<a href="https://blog.arvinh.info/2016/04/17/%E8%B6%85%E7%B0%A1%E6%98%93-Messenger-API-%E5%88%9D%E6%8E%A2/" class="dj by im in io ip" target="_blank" rel="noopener nofollow">超簡易-Messenger-API-初探</a>。可以只看如何申請，實作的部份先了解就即可。因為等下會介紹用框架做。

另外就是如果只要自己測試機器人的話，Webhook 設定好伺服器有架好就可以看到可以和機器人對話。但是如果要公開給使用者用的話，要先通過臉書的審查，可以看臉書官方文件「<a href="https://developers.facebook.com/docs/messenger-platform/app-review" class="dj by im in io ip" target="_blank" rel="noopener nofollow">提交您的 Messenger Bot</a>」來完成，通常要好幾天審查通過之後，你的 Messenger Bot 才能被其他使用者使用。

## Bottender 框架

如同先前提到，這是個百家爭鳴的時代，我們的力氣不足以應付各種標準，於是乎就誕生了框架。框架幫我們把最底層的麻煩事都打理好了，並且替我們考量到跨平台的議題。比方說就傳送訊息來說，每個平台需要呼叫的 API 不盡相同，原本你可能需要個別設定，但是在使用 Bottender 這類框架之後，一些參數設定好之後（token、secret 之類的），一律只需要呼叫 <code class="gt iw ix iy iz b">context.sendText</code> 函數，你什麼都別管，他就幫你搞定了！即使你只使用單一平台，框架幫你處理底層的 API 設定也非常方便，不一定要跨平台才能使用。

稍微介紹一下，這邊引用 <a href="https://blog.yoctol.com/yoctol-2017-review-1-6e876ad4de11" class="dj by im in io ip" target="_blank" rel="noopener nofollow">Bottender 團隊寫的文章</a>：

<span style="font-size: 26px; color: #696969; font-style:italic">優拓投入近半年心力的產品 — 多平台 Chatbot 框架「Bottender」終於公開並在 GitHub 開源。Bottender 是我們分析多套既有開發框架 (Framework) 後，綜合了 Chatbot 開發上的實務經驗，以「Learn Once, Write Anywhere」為核心理念，所打造出的一款開源 Framework，具備靈活、模組化、多平台等優勢。</span>

<em class="at">優拓投入近半年心力的產品 — 多平台 Chatbot 框架「Bottender」終於公開並在 </em><a href="https://github.com/Yoctol/Bottender" class="dj by im in io ip" target="_blank" rel="noopener nofollow"><em class="at">GitHub 開源</em></a><em class="at">。Bottender 是我們分析多套既有開發框架 (Framework) 後，綜合了 Chatbot 開發上的實務經驗，以「Learn Once, Write Anywhere」為核心理念，所打造出的一款開源 Framework，具備靈活、模組化、多平台等優勢。</em>

使用 Bottender 真的很簡單，我假設你會用 NodeJS with Express，那麼概念根本是一樣的，這邊我們簡單建立一個 Line 的 Hello World Bot：

```javascript=
const { LineBot } = require('Bottender');
const { createServer } = require('Bottender/express');
  
const bot = new LineBot({
  channelSecret: process.env.channelSecret, // 填上 Channel Secret
  accessToken: process.env.accessToken // 填上 Access Token
});
  
bot.onEvent(async context => {
  await context.sendText('Hello World');
});
  
const server = createServer(bot);
  
server.listen(5000, () => {
  console.log('server is running on 5000 port...');
});
```

這樣寫完就是最簡單的 Hello World Bot 了，相較於上面幾篇我說只需要看概念就好的教學，是不是簡約多了？

參數設定的地方，可以看到 <code class="gt iw ix iy iz b">process.env.channelSecret</code> 這樣的寫法，這是代表我們不會把真的 Secret 放在程式碼中，所以我們讓程式從環境變數中取得，環境變數通常可以在你架設伺服器的服務商網站設定，以 Heroku 為例的話，建立一個 App 之後，可以在 <code class="gt iw ix iy iz b">Setting &gt; Config Vars</code> 中設定：

<img class="dz t u go ak" src="https://miro.medium.com/max/3516/0*iTUZl6v0DUaJNSii.png" role="presentation"><br/>

那假設我們想要跨平台呢？

理論上做法應該有好多種，這邊分享我的作法，不過可能不是最聰明的，我在 Heroku 建立兩個 APP，一個是給 Line 另個給 Messenger，然後兩個 Heroku 都綁定 Github repo 的 master：

```javascript=
const {
    LineBot,
    MessengerBot
} = require('Bottender');
  
const bot = (process.env.chatbotPlatform == 'messenger') ?
            new MessengerBot({
                accessToken: process.env.messengerAccessToken,
                appSecret: process.env.messengerAppSecret,
            }) : new LineBot({
                channelSecret: process.env.lineChannelSecret,
                accessToken: process.env.lineChannelAccessToken
            });
  
bot.onEvent(async context => {
  await context.sendText('Hello World');
});
  
const server = createServer(bot);
  
server.listen(5000, () => {
  console.log('server is running on 5000 port...');
});
```

因為我想要做到一份程式碼可以跨平台，這樣我只需要更新 master 主幹，就可以同時讓兩個 Heroku APP 一起更新，不需要再分別修改不同分支，因為是可以讓 Heroku 各別綁定不同的分支，但我不想要這樣。

所以我在環境變數中設定這個 Heroku 是給哪個平台用的，程式碼運行時會從環境變數 <code class="gt iw ix iy iz b">process.env.chatbotPlatform</code> 中得知，並初始化對應的平台，因此可以看到我把 <code class="gt iw ix iy iz b">LineBot</code> 和 <code class="gt iw ix iy iz b">MessengerBot</code> 同時寫進去了。這樣就是一種可以跨平台的方法。

至於 <code class="gt iw ix iy iz b">bot.onEvent()</code> 則是處理和使用者對話的部分，不同平台都可以共用。如果有特別需要針對不同平台客製的話，再用 <code class="gt iw ix iy iz b">if</code> 判斷即可，或是特別寫函數處理，如同以下問題：

### Bottender 小細節

這邊必須提一下，由於我是 Line 免費版搭配 Messenger，所以 Line 只能回覆不能推播，但是臉書卻沒有這限制。這個特性使得我們用 Bottender 要特別注意，因為 Bottender 中沒有特別去區分，假設今天我要回覆照片，在 Line 上只能用 <code class="gt iw ix iy iz b">context.replyImage</code>，但 Messenger 要使用 <code class="gt iw ix iy iz b">context.sendImage</code>，可是我卻不能直接讓 Line 也使用 <code class="gt iw ix iy iz b">context.sendImage</code>，因為主動推播要使用付費版的 Line，並且 Messenger 並不能使用 <code class="gt iw ix iy iz b">context.replyImage</code>。於是就有了這樣尷尬的情況發生了！

為了讓平台可以共用，我又自己包裝了一層函數：

```javascript=
async function platformReplyImage(context, url) {
    if (process.env.chatroomPlatform == 'messenger') {
        await context.sendImage(url)
    } else {
        await context.replyImage(url);
    }
}
```

如此一來就解決了上述問題，此問題也發生在 <code class="gt iw ix iy iz b">sendText</code> 和 <code class="gt iw ix iy iz b">replyText</code> 中，希望 Bottender 可以針對這塊改善，我也發了一個 <a href="https://github.com/Yoctol/Bottender/issues/264" class="dj by im in io ip" target="_blank" rel="noopener nofollow">issue</a> 表達我的想法。

## 機器人回應設計思路

在繼續閱讀之前，希望大家能先看這篇「<a href="https://zake7749.github.io/2016/12/17/how-to-develop-chatbot/" class="dj by im in io ip" target="_blank" rel="noopener nofollow">聊天機器人的開發思路</a>」，這篇文章介紹了機器人回應的幾種模式，以及適用情況。那麼接著就是要考慮我在氣象機器人中，要採用下列模型的哪一種了：

<ul>
<li id="19f1" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie ja jb jc">樣板式模型 (Rule-based model)</li><li id="8f86" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">檢索式模型 (Retrieval-based model)</li><li id="36b3" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">生成式模型 (Generative model)</li>
</ul>

這個時候就要思考一下，使用者會如何對氣象機器人說話，以及氣象機器人會回應什麼資訊？

簡單舉例的話，大多數使用情形可能就是：「明天會下雨嗎？」、「今天天氣好嗎」、「明天氣象預報」、「台北天氣如何」、「台大現在空氣品質怎樣？」「需要帶傘嗎？」「要戴口罩嗎？」

上面我列出一個人想問天氣的時候最可能的問句，事實上如果你想查天氣，大概會對 Google 下搜尋的句子就是這樣。

<img class="dz t u go ak" src="https://miro.medium.com/max/2332/0*xBzHd1A_Io0Z2dCi.png" role="presentation"><br/>

簡單分析一下上面這些問句，每個句子都有關鍵字，例如：

<ul>
<li id="4551" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie ja jb jc">天氣關鍵字：「天氣」、「預報」、「空氣品質」</li><li id="8dea" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">天氣抽象名詞：「傘」、「口罩」</li><li id="c16e" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">時間關鍵字：「今天」、「明天」</li><li id="200f" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">地點關鍵字：「台北」、「台大」</li>
</ul>

你會發現，當你想要知道氣象資訊時，一個句子的組合大概就是:

[地點][時間][天氣關鍵字｜天氣抽象名詞]

在這個情況下，氣象機器人其實只需要用樣板模型就可以達成需求了，並且精準度也可以達到幾乎百分之百。因為在查詢天氣的時候，我們不需要判斷使用者的隱晦含義，或是句子是正向還是負向含義，因此不需要語意分析、機器學習等等方法介入。

此外即使是多輪對話的形式，還是可以只靠樣版模型就可以了，我們剛剛提到三要素，地點、時間、天氣關鍵字，所以最多只需要三輪對話，例如使用者只說了「台北」，機器人就問他說要哪個「時間」，再問他說要知道「空氣品質」還是「天氣狀況」。

但事實上，氣象機器人大多情況只需要一輪就夠了。因為假設使用者只說「地點」，那我們可以預期他就是問現在狀況，頂多一週天氣趨勢。當使用者只說「時間」或「天氣關鍵字」，我們可以預期地點是他發訊息的所在地。

因此其實氣象機器人不需要多輪式對話，因為查詢天氣就是一個很單純的動作，即便使用者輸入並未得到想要的資料，只要重新下夠明確的句子，例如「下週二紐約氣象預報」就可以得到答案。

## 樣板式模型實作

樣版式模型其實感覺也什麼技巧，但要注意樣板能應付所有情況。此外樣板模型其實就是決策樹，採用時要注意路徑的設計，例如以天氣查詢來說，路經應該是「天氣關鍵字」優先判斷，才會進入「地點」或「時間」的判斷。當句子只有地點或時間時，假設是一對一情況下，使用者只說「台北」，你大概能猜他想問台北天氣。但因爲機器人能在群組中使用，這時候有明確的「天氣關鍵字」出現，才能準確做出回應。

例如以「天氣」指令來說，我的邏輯是這樣：

```javascript=
// ...
// 一些預處理，抓地點、時間、氣象關鍵字等
// ...
} else if (isWeatherKeyword) {  // 如果是要回應「天氣」況狀，例如：天氣、濕度、溫度
    let replyMsg = ""; // 將回傳給使用者的資訊
    // ...
    if (isTimeKeyword) { // 如果有時間關鍵字，並且不是現在，就採用預報
        replyMsg = await getForecast(); // 取得氣象預報資料
    } else { // 不然就回答現在天氣
        replyMsg = await getWeather(); // 取得現在氣象狀況
    }
    await platformReplyText(context, replyMsg); // 回傳給 Line 或 Messenger
} else if(/* 其他氣象關鍵字，例如：空氣品質、 */) {
// ....
```

所以假設今天句子是「台北天氣」，就會是找台北現在天氣。如果句子是「明天台北天氣」，就會去找氣象預報的資料。你可能會好奇那「地點」呢？其實我是在 <code class="gt iw ix iy iz b">getForecast()</code> 和 <code class="gt iw ix iy iz b">getWeather()</code> 函數底下才處理地點。

決策樹的細節我就不多作介紹，大致上就是用這樣的判斷方式把所有使用者可能會下的問句都解析並回應。

## 資料來源

一個氣象機器人最重要的部分就是氣象資料了，一般來說資料取得有幾種方式：

<ul>
<li id="f3b7" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie ja jb jc">爬蟲</li><li id="9a03" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">公開 API</li><li id="93ae" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">隱藏版 API</li>
</ul>

## 爬蟲

所謂爬蟲就是去開網頁，找出網頁原始碼中的資料，並擷取出來，例如我可以去找氣象局網站中的氣溫數字，在原始碼中就會長這樣：

<img class="dz t u go ak" src="https://miro.medium.com/max/3968/0*wz4rOUNlCxj2ANPX.png" role="presentation"><br/>

## 公開 API

公開 API 就是一些開放平台，或是商業機構，提供正式的 API 服務，可以藉由這些 API 取得你要的資料。例如：

<ul>
<li id="2032" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie ja jb jc"><a href="https://opendata.cwb.gov.tw/index" class="dj by im in io ip" target="_blank" rel="noopener nofollow">氣象資料開放平臺</a>：氣象局的公開資料</li><li id="c2ee" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc"><a href="https://openweathermap.org/api" class="dj by im in io ip" target="_blank" rel="noopener nofollow">Open Weather Map</a>：國外的氣象資料服務商</li>
</ul>

還有很多，就不多列舉了。

## 隱藏版 API

這個技巧通常初學者都不知道，特別介紹一下。剛剛提到說，爬蟲是去抓 HTML 的欄位資料，但是很多時候 HTML 是透過 JS 事後補上去的。是的，這就是 MVC 框架下的網站架構。網站會先渲染版面，然後再由 HTTP Request 呼叫他自己的 API 取得剩下的資料，並用 JS 把資料補到渲染畫面上。

所以我們要做的事情就是，攔截網站自己的 API，這些 API 不是公開的，但是我們也可以拿來用。不過風險是，因為這些 API 不是對外公開的，可能用法或是名稱常常再改變。

<img class="dz t u go ak" src="https://miro.medium.com/max/4000/0*a_8dEVjt34mrniiO.png" role="presentation"><br/>

以上圖為例，Breezo Meter 是一個可以查空氣品質的網站，我想看看它是不是有自己的 API，所以我打該網頁，然後開啟「開發者工具」，點開「網路」然後選「XHR」。

這時候我們會看到有好幾筆資料，我就每一筆都點開看看，然後看「回應」的部分，所謂回應就是 HTTP Request 的 Response，如果他是一隻 API，就會看到 Json 格式的資料，然後我們就成功攔截 API 了！我們就可以直接使用隱藏版 API 來取得資料，通常會比寫爬蟲還方便，但風險就是他可能隨時會變。

## 資料處理

## 資料庫

我有兩台伺服器分別處理不同聊天平台，但資料庫應該要共用，所以把資料部分獨立出來。資料庫部分我使用 Firebase，因為 Firebase 不需要去管伺服器的問題，比起我自己在弄一台專門的資料庫伺服器方便。

資料庫主要是用來記錄一些高成本的資訊，例如「空氣品質的圖」其實是兩張圖片合成，每次有使用者查詢都合成一次很浪費資源，所以在第一位使用者查詢時，跑過一次影像處理就把他存起來，在同時間內有其他查詢就直接調用資料庫。

這邊可能會有問題，為什麼不用伺服器定時跑資料存到資料庫？這是因為目前使用者大約一千，查詢頻率其實沒有到很高，所以想說愛地球，有需要再跑就好。

一般做法都是把所有可能會調用的資料都用固定排成先跑好，像是爬蟲、調用 API、圖片處理等等都每隔一段時間自動執行並儲存，只是我覺得使用量還沒那麼大所以沒這樣做。

## 圖片

氣象機器人可以直接下關鍵字得到天氣圖、衛星圖、預報圖等，甚至我連地震圖都支援。但是 Line 規定圖片來源要是 HTTPS，很遺憾中央氣象局只有 HTTP，所以我必須先把圖片傳給第三方圖片服務商，這邊我是用 Imgur。然後再把上傳 Imgur 的圖片傳到 Line 上。因為圖片轉介很花時間，而且同一張圖片其實可以再利用，所以最後傳到 Imgur 的圖片都會用 Firebase 記錄起來。

## 氣象資料

原始氣象資料可能會需要處理，例如:

<ul>
<li id="69e9" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie ja jb jc">體感溫度必須自己從測站資料去算</li><li id="4500" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">風向都是數字，要轉成方位</li><li id="9884" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">空氣品質好壞指標 AQI 是數值，要轉換成描述文字例如「對過敏族群不健康」</li>
</ul>

簡單明瞭地把數據呈現給使用者也很重要。

## 關鍵字的處理

## 時間

要能辨識句子的時間，才能知道要給哪個時間的資料，所以機器人要能辨識「明天晚上」、「今天 20:00」、「明天 6:30pm」這類的時間語句。

這邊我採用 <a href="https://github.com/wanasit/chrono" class="dj by im in io ip" target="_blank" rel="noopener nofollow">Chrono Node</a>，他辨識的能力真的滿不錯的，而且支援英文中文混雜。不過我後來發現他中文支援度不完整，例如中文的「前天」、「後天」、「大後天」並不支援，所以我有幫忙寫補丁，不過發 <a href="https://github.com/wanasit/chrono/pull/260" class="dj by im in io ip" target="_blank" rel="noopener nofollow">Pull Request</a> 之後作者一直沒有回應，感覺是沒在維護了。所以氣象機器人是安裝我自己修改過的 <a href="https://github.com/tigercosmos/chrono/" class="dj by im in io ip" target="_blank" rel="noopener nofollow">fork 版本</a>。

Chrono 處理中文時間方法我覺得滿不錯的，這邊簡單示例：

由於中文表示時間的組合就那麼多，所以全部列出來。

```javascript=
var PATTERN = new RegExp(
    '(而家|立(?:刻|即)|即刻)|' +
    '(今|明|前|大前|後|大後|聽|昨|尋|琴)(早|朝|晚)|' +
    '(上(?:午|晝)|朝(?:早)|早(?:上)|下(?:午|晝)|晏(?:晝)|晚(?:上)|夜(?:晚)?|中(?:午)|凌(?:晨))|' +
    '(今|明|前|大前|後|大後|聽|昨|尋|琴)(?:日|天)' +
    '(?:[\\s|,|，]*)' +
    '(?:(上(?:午|晝)|朝(?:早)|早(?:上)|下(?:午|晝)|晏(?:晝)|晚(?:上)|夜(?:晚)?|中(?:午)|凌(?:晨)))?', 'i');
```

根據中文描述轉換成時間概念。

```javascript=
// .....
} else if (match[DAY_GROUP_1]) { // 處理中文字有關於「天」的部分
    var day1 = match[DAY_GROUP_1];
    var time1 = match[TIME_GROUP_1];

    if (day1 == '明' || day1 == '聽') {
        // 如果半夜說明天，通常是今天的概念
        if(refMoment.hour() > 1) {
            startMoment.add(1, 'day');
        }
    } else if (day1 == '昨' || day1 == '尋' || day1 == '琴') {
        startMoment.add(-1, 'day');
    } else if (day1 == "前"){
        startMoment.add(-2, 'day');
    } else if (day1 == "大前"){
        startMoment.add(-3, 'day');
    } else if ( day1 == "後"){
        startMoment.add(2, 'day');
    } else if (day1 == "大後"){
        startMoment.add(3, 'day');
    }

    if (time1 == '早' || time1 == '朝') {
        result.start.imply('hour', 6);
    } else if (time1 == '晚') {
        result.start.imply('hour', 22);
        result.start.imply('meridiem', 1);
} else if (match[TIME_GROUP_2]) { // 處理中文字有關於「時」的部分
```

上面只是中文處理的部份而已，可以把「明天晚上」、「後天早上」等時間概念轉換成 <code class="gt iw ix iy iz b">Date()</code> 物件。此外 Chrono 最好用的部分是不同語言的模組互通，所以可以混搭例如「明天 8:00pm」。中文數字處理以及英文時間判斷就留給讀者自行去看原始碼囉！

此外在開發過程中我被「時間」折騰個半死，因為伺服器在美國，使用者應該是在台灣（很不嚴謹的假設，我還沒去研究如何從 line 或 messenger 中取得使用者時區），中央氣象局資料時間是台灣時間，所以要一直轉換來比對時間。

轉換時間真的是暈頭轉向：

<ol>
<li id="8a92" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie kh jb jc">伺服器收到訊息，要判斷句子中的時間，然後假設使用者是在台灣，以此換成 UTC 標準時間。</li><li id="61ac" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie kh jb jc">再將伺服器時間也轉成 UTC 標準時間，比較句子時間與伺服器時間，檢查時間是否在未來。</li><li id="1a6d" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie kh jb jc">是未來就去撈氣象局預報資料，並將氣象局資料轉成 UTC 標準時間，找出與句子時間符合的氣象數據。</li>
</ol>

此外 NodeJS 的國際化元件（ICU）原來預設是裝 <code class="gt iw ix iy iz b">small-icu</code>，想要完整的話要裝 <code class="gt iw ix iy iz b">full-icu</code>。國際化元件可以讓時間表達成中文，原本 NodeJS 會直接將晚上八點表達成 <code class="gt iw ix iy iz b">20:00</code>，但是完整的國際化元件可以讓他表示成 <code class="gt iw ix iy iz b">下午8:00</code>。

<code class="gt iw ix iy iz b">npm install full-icu --save</code>

執行 NodeJS 的時候要這樣來使用完整的國際化元件：

<code class="gt iw ix iy iz b">node --icu-data-dir=./node_modules/full-icu index.js</code>

## 地點

要判斷句子中的地點真的很難，世界的地名五花八門，連「<a href="https://chimei.jitenon.jp/data/kanji.php?kanji=%E5%A4%AA%E9%99%BD&amp;search=id" class="dj by im in io ip" target="_blank" rel="noopener nofollow">太陽</a>」都可以是地名。我的處理辦法是分台灣地區和國外地區。

<ul>
<li id="1236" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie ja jb jc">台灣地區：台灣的行政區最低層級是村或里，全部加起來也才不到一萬個，所以台灣地區先建檔，可以很明確的辨識出來。檔案包含縣市、鄉鎮市、村里和經緯度資訊。</li><li id="0e11" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie ja jb jc">非行政地區、國外地區：如果是非行政區的地名，例如台灣大學、總統府等等，或是國外的地區，例如紐約、東京等。這時候我會用 <a href="https://developers.google.com/maps/documentation/geocoding/intro?hl=zh-tw" class="dj by im in io ip" target="_blank" rel="noopener nofollow">Google Map Api</a> 來查對應的經緯度。</li>
</ul>

為什麼都是經緯度呢？

<ol>
<li id="75a6" class="hr hs em at ht b hu if hw ig hy ih ia ii ic ij ie kh jb jc">台灣地區會去查使用者查詢地點的最近的測站，因為我有每個測站的經緯度，所以會去算彼此距離，並取得數據。例如查台北公館天氣狀況，因為台灣大學就有觀測站（台大就在公館），所以會得到台灣大學觀測站的數據資料。</li><li id="1f61" class="hr hs em at ht b hu jw hw jx hy jy ia jz ic ka ie kh jb jc">國外的氣象 API 通常都是用經緯度當參數。</li>
</ol>

值得一提的是，台灣的氣象測站真的很密，台灣的氣象測站大約有四百個，但是如果換在國外的話，一個台灣大小的區域，可能只有一個測站。所以國外服務商的氣象資訊常常都是使用內插外插來取得近似值，換言之就是很不精確啦！但台灣因為太密了，直接找最近的測站的數據就好，而且很準！

## 地名處理

由於中文字整串黏在一起的特性，要能準確判斷他是不是地名，不能直接用這樣判斷：

<code class="gt iw ix iy iz b">if(message.includes(&quot;北海道&quot;))</code>

因為原句可能是「北海、道路」，大概是這種感覺。

這邊我用<a href="https://github.com/yanyiwu/nodejieba" class="dj by im in io ip" target="_blank" rel="noopener nofollow">結巴分詞</a>，來把句子切割成一個個詞。這個模組簡單原理就是用詞頻來決定要不要做切割。不過其實在預設問句中一定要有地名的情況下，這樣做用處不大。實際比較有感可能是像 Siri 這種可以回答各種天馬行空問題的機器人才要能正確辨識是不是有地名的概念，還是只是湊巧兩個字連在一起罷了。但考量未來可擴充性，我先採用比較高級一點的方式處理。

## 總結

我大致上已經將我如何實作氣象機器人的技術都介紹了，未來我會持續讓他越來越好，目前樣板式模型最大缺點就是會有無法辨識的情況，這時候我會回應讓使用者直接查看使用說明，但真正好的服務是不需要使用說明的，一個好的聊天機器人應該跟人一樣聰明對吧？

很高興不知不覺就有超過一千名使用者，隨者使用者變多，未來架構可能也還會需要調整，如同所有規模逐漸成長的公司的後端架構一樣，A/B 測試、紅藍部署等等技術都是隨著規模擴大而將慢慢導入。

<span style="font-size: 26px; color: #696969; font-style:italic">你可以在這邊查看氣象喵的 Github Repo</span>

<em class="at">你可以在這邊查看</em><strong class="ht iv"><em class="at">氣象喵</em></strong><em class="at">的 Github Repo</em>

> [weather-bot/WxKitty](https://github.com/weather-bot/WxKitty)
