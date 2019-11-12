---
title: How the Puffin Browser Works
date: 2018-09-08 00:00:00
tags: [Chinese Posts,English Posts,Puffin Browser,Browsers,Browser Architecture,Cloudmosa,English,]
---


## How the Puffin Browser Works

### Puffin is wicked fast. Let’s dig deeper into it.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2238/0*dWo9qcDgSr-F1adr.png" role="presentation"><br/>

This summer, I have been a software engineering intern at <a href="https://www.cloudmosa.com/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">CloudMosa, Inc.</a>, a company which develops <a href="https://www.puffinbrowser.com/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Puffin Browser</a>.

During two months of the summer, I have participated in some features development and fixed some bugs. Meanwhile, I have a look at the whole picture of Puffin Browser.

<!-- more --> 

Puffin is a well-known remote browser with many users all over the world, and it is famous for Flash support on iOS and Android devices. Leveraging resources on remote servers allows Puffin to be faster than regular browsers, especially when browsing bandwidth-hogging or data-intensive websites on low-end mobile devices or with a low-bandwidth connection.

As a remote browser, Puffin has many advantages over other popular browsers on the market, and I will discuss what makes Puffin stand out in this article.

## Regular browser mechanisms

Before introducing Puffin, it is important to know how a regular browser works. Note that when I use the term “regular”, I refer to popular browsers on the market such as Google Chrome and Mozilla Firefox, but not Puffin. Puffin has a very different architecture from others.

A browser enables us to surf the internet. I will introduce the main concept of a browser in the following sections. There are still further details of browsers not covered in this article, but there is an article, “<a href="https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">How Browsers Work</a>”, which explains the mechanisms of browsers very well. I’d highly recommend you to read it first if you’re not so familiar with how browsers work.

## How we browse the Internet

Let’s talk about how a browser in your PC or smartphone reaches a website, in order to introduce what’s going on in a browser later.

When users want to browse a website, they will type a URL at the search bar in the browser. Once they press <code class="gw im in io ip b">Enter</code> and go, the browser will connect to the server of the target website on the Internet. Then the browser will ask for resources from the server.

A website is hosted on a server, and there are files, including <code class="gw im in io ip b">html</code>, <code class="gw im in io ip b">css</code>, <code class="gw im in io ip b">javascript</code>, and other media resources on the server. The server will send these files to the browser, and then the browser can use these resources to parse and render the page.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2628/0*PUX4OoW2yEwaCe4R.jpg" role="presentation"><br/>

## GUI application

A browser is a kind of graphic user interface (GUI) applications just like all the other types of software.

There are also many features on a browser, such as the URL bar, the bookmark bar, History, go back, go forward, download, etc. These functions make a browser more useful. But the most important part is the window canvas for rendering web pages.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2750/0*iMsRnZuyes6JyrTX.jpg" role="presentation"><br/>

Many browsers just focus on developing an unique GUI, which means they use an open source browser engine, which might be Firefox Gecko or Chromium Blink, and they don’t develop the browser engine themselves. Puffin, Opera, Brave, Vivaldi, etc., all belong to this kind of browsers.

This is similar in the Android smartphone market in which there are many smartphones made by HTC, LG, Samsung, etc., but they all use Android as their OS.

Thus, even though browsers use the same engine, they could still be very different and unique on certain features.

## Browser engines

Now that we have gathered the resources to parse websites, we need to make sure they are properly displayed on the screen in the browser window. That’s what browser engines do. There are mainly two engines in a browser, namely, the rendering engine and the JavaScript engine. The rendering engine is also known as the layout engine.

The browser engine will process the website source code to visual pixels on the screen. The whole process could be quite complicated. A simplified process is shown in the figure below.

<img class="dz t u gs ak" src="https://miro.medium.com/max/3724/0*wR75PWGzz9fSgjf6.png" role="presentation"><br/>

## DOM

The file format of HTML is just like a tree structure, so the DOM parser can parse HTML files as a DOM tree. A DOM (Document Object Model) refers to a component in a page. A DOM tree could be understood as how components in a page form a tree.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2806/0*l9Dnc5NBafUrlNKg.jpg" role="presentation"><br/>

## Rules

CSS is also a tree structure, and will be parsed as a rule tree. CSS decorates the nodes in the DOM tree, and we can view it as a rule, such as one that makes the text in the DOM red. There may be many rules in CSS, and a DOM could follow multiple rules, so there may be many rule trees which all point to the same DOM, and the combination of DOM and CSS works like a forest.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2816/0*LhHwL8l_De2gX1nf.jpg" role="presentation"><br/>

## Style

Once DOM and rules have been parsed, the browser engine will combine these two trees into a style tree. A style tree is like a tree with decorators. Each node is a component decorated by its own rules in the page.

## Layout

Each component in a page is a box. A box has its own width, height, position, border. A website is stacked by many boxes, and we call it the layout.

This picture is a box. A box includes margin, border, padding, and content. We use these properties to control the appearance of a box.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2448/0*zz_-MSU4FheHNpEc.png" role="presentation"><br/>

Now we have derived the style tree, but we only know what components we have and how they look like. So in the layout step, we need to layout these components by their box properties.

After the laying out, a page has already calculated to a layout structure. But we cannot see the page now, because it is still a structural format. We need to output the page to the screen in the next step.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2966/0*So8f-dYLbbSJ06Hl.jpg" role="presentation"><br/>

## Paint

After we get the layout of a page, we can draw the page by a graphics library (GL). The engine will translate the layout to GL script, and then GL will output pixels. Then we could render pixels on the screen of the application window to show the website.

## JavaScript

JavaScript can change HTML or CSS, and cause DOM and rules changed. Once the DOM and rules structure change, the whole process will need to run again. The JavaScript works are done by the JavaScript engine, and the other works about parsing and layout are done by the rendering engine.

## Browser bottlenecks

Browsers are fast. No matter Chrome, Firefox or any others, their rendering speed are fine for normal users. However, people would like to see pages as fast as possible for a better experience. The term “fast” here means loading, parsing, rendering a page in a short time.

The fact is that progress of browsers are slow in these years. What’s wrong for browsers? There are several factors which are very important to a browser to show a page fast. The main factors are internet connection and calculation of parsing and rendering.

## Internet Connection

Bandwidth influences the downloading rate on the resources, and round-trip time (RTT) restricts the minimum time we will spend.

Bandwidth is very straightforward. The bigger, the faster.

<img class="dz t u gs ak" src="https://miro.medium.com/max/1986/0*A75uljUvFa73GDsb.jpg" role="presentation"><br/>

Round-trip time is more complicated. When you ask server for a file or communicate to server, your device(client) will send an HTTP request to server, and the server will respond data or file to you. This cycle is called a round-trip.

If we don’t count the time for downloading and just count the time that client and server make a request and a response, it is the round-trip time (RTT).

<img class="dz t u gs ak" src="https://miro.medium.com/max/2658/0*MGTfZWbG-AbMT-ZC.jpg" role="presentation"><br/>

The following table shows the RTT time of a HTTP request with 3G and 4G internet connection. The paper &lt;<a href="http://www.ruf.rice.edu/~mobile/publications/wang11hotmobile.pdf" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Why are Web Browsers Slow on Smartphones?</a>&gt; has argued that the RTT is the reason why browser is slow on smartphones.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2584/0*49Q9E1KMFb0CdHZ6.png" role="presentation"><br/>

A HTTP request will introduce a RTT, and there might be many HTTP requests in a website. Hence there would be lots of RTTs, which means a lot of times. So, decreasing the time of RTTs and reducing number of RTTs will be helpful for a fast rendering.

## Calculation

A powerful computer with strong CPU does make the calculating time to be fast, but most of computers just have normal CPU. So, if we want to make the rendering process fast, we need to either have a better algorithm or reduce calculating.

## Puffin Architecture

These bottlenecks are not easy to solve. Chromium and Firefox have made a lot of effort on improve the performance. With changing partial algorithm, it might only help improve little performance but it cannot be a breakthrough for browsers. If we want a breakthrough, we must try a new architecture.

<a href="https://github.com/servo/webrender" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Firefox Webrender</a> is a kind of new architecture. The concept is rendering web pages just like rendering a game. It’s very cool. You might want to know more <a href="https://hacks.mozilla.org/2017/10/the-whole-web-at-maximum-fps-how-webrender-gets-rid-of-jank/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">about it</a>.

Puffin browser also has a cutting-edge architecture, which is a remote browser. A remote browser means the most of parts of rendering a page is done at data center, and the client side, which is PC or smartphone, only need to show the rendering result.

So the simplified process of a remote browser might be:

<img class="dz t u gs ak" src="https://miro.medium.com/max/3528/0*o4sihV5Grsihmzaa.png" role="presentation"><br/>

Puffin is a browser based on Chromium, which means we use Blink, V8, Skia, and so on. What we do is separating the origin rendering process to two parts. Those heavy works before painting are done in the data center level, and then server will send the rendering result to client, so client just need to draw the page.

## Remote browser engine

Puffin browser is a remote browser. As I mentioned above, a browser mainly are two parts in an application, which are GUI and engines. With the same concept, Puffin is a remote browser engine on server plus a client browser application.

So, you can imagine that using Puffin is just like connecting to a remote Desktop. Each user will use Puffin browser client connect to the Puffin browser engine instance on a server. The interesting part is that CloudMosa team uses fruits name as nickname for products. So the remote engine instance is named “Mango”.

Under this architecture, how many clients there are, how many Mangos run on our data centers. Since we have almost ten million active users each month, we need a huge amount of servers.

At early stages, we put our servers on cloud service, which is something like AWS. However, when our scale grows so big, we have no choice to create our own data center for decreasing cost of running servers.

Nowadays, we have more than ten thousands high level servers at twelve data centers in USA and Singapore. We use Docker as the server container. There is only one docker in a server, because we don’t use docker as a VM, but instead as an operation unit.

With a well designed load balance system, data centers can serve millions requests well. We can make sure our system will provide each Puffin users a best Mango instance. If anything go wrong on server, either the server system or Puffin client has capability of fault tolerance.

In other words, it is the data centers that powers the Puffin browser, because the remote browser engine is the key why Puffin run fast.

## Browser Client

Puffin supports many platforms, including Android, iOS, Windows and Linux. “Lemon” is Puffin on Android, “Cherry” is Puffin on iOS, “Papaya” is Puffin on Windows, and “Raspberry” is Puffin on Linux.

We use React Native to draw the UI of Puffin Windows and the next version of Puffin Android(Puffin 8, now the latest is Puffin 7.7 on Play Store). With React Native, we can develop the UI faster, and the UI modules are reusable.

We use GTK as the GUI for Puffin Linux. You might wonder why not React Native? Though we want to reuse modules, unfortunately, we hope Puffin Linux could run well on low-level devices, such as Raspberry Pi. React Native has too much CPU cost for Raspberry Pi; therefore Puffin Linux chooses GTK as an alternative.

Puffin browser client (hereinafter called “Puffin”) is designed to talk to Mangos. There is a protocol for communication between Puffin and Mango.

When browsing a page, Puffin will ask Mango to reach a web page and then to render the page. Once rendering has done, Mango will send rendered data to Puffin.

<img class="dz t u gs ak" src="https://miro.medium.com/max/3480/0*-jtSRbWPMRUM-HDF.jpg" role="presentation"><br/>

Besides, when a user interacts with pages, Puffin will also need to tell Mango what happens on the page by the user, including scrolling, JavaScript events, text input, etc. Then Mango will render the next frame to Puffin according the information.

As you can see, Puffin doesn’t do heavy works, because almost things are on Mango. Remember the bottlenecks of browsers? With this architecture, we don’t need to worry about the device calculating ability, because we let server do the works.

We don’t also need to worry about the bandwidth and round-trip time (RTT), since the bandwidth in data center are very very fast, and the data center of most services, including Facebook, Google, Yahoo, Amazon, etc., are just next to our data center, which means the RTT will be very short.

What I didn’t mention above is, Puffin also save much power and data traffic. It’s straightforward, because the power is consumed at data center, and Mango will just send the rendering result with compressed media data, which is much smaller than original sources in total.

The only shortage of our architecture is Puffin must communicate with Mango, which means we decrease a lot of bandwidth and RTTs, but we cannot avoid the RTTs between Puffin and Mango. So when we browse a website need a lot of communication, such as JavaScript animation, Puffin will not perform very well.

## Beyond the Remote Architecture

Puffin adopts the remote browser architecture, so it can either provide cloud services itself or connect to other cloud services in a convenient way.

Mango can do many things before sending the rendering result to user. Information security is an example. Before users touch the resources from websites, we have checked the file is safe and the content is not malicious. Even though the website is malicious, user is still safe, because Puffin only receive rendering result. In other words, we should worry about Mango instead. But don’t worry, we can handle bad pages.

There are some other services based on cloud with our architecture. Puffin enables users play Flash on Android and iOS. Puffin lets user be able to download files right to cloud storage service.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2362/0*21oMswZNtLMxibB5.jpg" role="presentation"><br/>

Regular browsers cannot provide services above, because they don’t use a remote browser to do those services. Browser engines on the cloud makes Puffin very special and powerful.

## Benchmarks

Seeing is believing. There are some famous benchmarks for browsers. I will run the tests and show you how fast Puffin is.

Since Puffin’s engines are based on Chromium and also Chrome is the lead of the market, we will compare the result of benchmarks between Puffin and Chrome.

Puffin is a remote browser, so when users use Puffin, they will use Mangos at data center. It’s no difference what devices users use, because they all connect to data center.

Therefore we don’t run Mango(Puffin engines) on local server for testing. In fact, if we run Mango on local (not Puffin anymore, isn’t it?), Puffin is almost the same as Chrome.

The test environment is on Ubuntu 16, with Intel® Core™ i7–4800MQ CPU @ 2.70GHz × 8, 8G RAM. We use Puffin 7.7(Chromium 66 engines base) and Chrome 68.

Result: Puffin wins Chrome for 4 of 5 benchmarks

<ul>
<li id="ad79" class="hc hd em at he b hf hg hh hi hj hk hl hm hn ho hp jv jw jx"><a href="https://webkit.org/perf/sunspider-1.0.2/sunspider-1.0.2/driver.html" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Sunspider Benchmark</a>: Puffin is 1.05x faster than Chrome</li><li id="75fa" class="hc hd em at he b hf jy hh jz hj ka hl kb hn kc hp jv jw jx"><a href="https://krakenbenchmark.mozilla.org/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Kraken JavaScript Benchmark</a>: Puffin is 1.11x faster than Chrome</li><li id="2f83" class="hc hd em at he b hf jy hh jz hj ka hl kb hn kc hp jv jw jx"><a href="http://principledtechnologies.com/benchmarkxprt/webxprt/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">WebXPRT3 Benchmark</a>: Puffin’s 166 higher than Chrome’s 88</li><li id="6bdb" class="hc hd em at he b hf jy hh jz hj ka hl kb hn kc hp jv jw jx"><a href="http://chromium.github.io/octane/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Chromium Octane Benchmark</a>: Puffin’s 33116 higher than Chrome’s 28829</li><li id="e9f3" class="hc hd em at he b hf jy hh jz hj ka hl kb hn kc hp jv jw jx"><a href="https://browserbench.org/Speedometer" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Speedometer</a>: Chrome’s 128 higher than Puffin’s 94.3</li>
</ul>

<img class="dz t u gs ak" src="https://miro.medium.com/max/2420/0*HbrhS49v2nCyTfvZ.jpg" role="presentation"><br/>

The result is very obvious. Puffin is wicked faster, and beats Chrome heavily. I am going to explain the meaning of the test.

I am using a powerful PC for testing, and Chrome is slower, which means if we use other devices lower than a strong PC, such as low-end notebooks, intermediate smartphones, the difference from benchmarks will be much bigger. That’s because Puffin’s engines runs at data center, so even a low-end device, Puffin is still fast.

We know Puffin runs faster than Chrome on a strong PC, so now imagine you are using Raspberry Pi to surf the Internet. You will feel Chrome is very slow on Pi, because Raspberry Pi is a low-end computer as we known. However, when you use Puffin on Pi, you will feel it is still fast as usual like you use PC.

The only one benchmark Puffin loses Chrome a little bit is Speedometer. Speedometer simulates a lots of DOM API manipulating, which costs a lot of RTTs between Puffin and Mango. As I mentioned before, this is the only cons of the remote browser architecture of Puffin.

So, we have proved that Puffin is indeed fast. The remote browser is indeed a super good idea. No matter what device is, Puffin always run fast, since the heavy works are done at data center.

## Conclusion

This article introduces how browsers work, especially how Puffin works. Puffin uses remote browser architecture. It’s unique and it works. The benchmarks shows that Puffin really does well.

The internet is fast. Browsers are fast. But not enough! I believe we can make the web even faster. Just like what Puffin is doing.

It’s the end of my journey in CloudMosa, but not the end of my enthusiasm for browsers. I will keep studying web technology and researching browsers.

---

### Special thanks

Thanks my coworkers <a href="https://medium.com/u/1e501bea16d7?source=post_page-----440c91cece8f----------------------" class="la az by" target="_blank" rel="noopener">Brian Wang</a> and Debby Peng for helping me review the article.

### About Me

Liu, An-Chi(劉安齊). A software engineer, who loves writing code and promoting CS to people. Welcome to follow me at <a href="https://www.facebook.com/CodingNeutrino/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Facebook Page</a>. More information on <a href="http://tigercosmos.xyz/" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Personal Site</a> and <a href="https://github.com/tigercosmos" class="dj by hq hr hs ht" target="_blank" rel="noopener nofollow">Github</a>.