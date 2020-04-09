---
title: Localize the Rust Website to Traditional Chinese
date: 2019-06-19 01:23:39
tags: [English Posts,Localization,Rust,English,Rust Taiwan,]
---

Record Rust Taiwan community’s work of translating the Rust website
紀錄 Rust 台灣社群將 Rust 官網翻譯成正體中文的過程

<img class="dz t u gs ak" src="https://miro.medium.com/max/2292/1*Glon_ud1Q-gmHrpQtKi45w.png" role="presentation"><br/>

<strong class="hj hv"><em class="hw">TL;DR</em></strong> <br>I am glad to announce that the Traditional Chinese (正體中文) version of the Rust official website has been launched. Thanks to all contributors in the community. This article records our experience to achieve the work.

<!-- more --> 

<strong class="hj hv"><em class="hw">What is Rust? </em></strong><br>It is a language empowering everyone to build reliable and efficient software, the toast in the software town.

Rust website in traditional Chinese: [Rust 程式設計語言](https://www.rust-lang.org/zh-TW/)

---

## How to localize?

Back to around May, the Rust team made all strings in the Rust website being localizable so that the communities from all over the world can localize the Rust website to different languages.

Issue: [[meta] Add localization strings everywhere · rust-lang/www.rust-lang.org](https://github.com/rust-lang/www.rust-lang.org/issues/798)

Now you can see all locale files in the repo <a href="https://github.com/rust-lang/www.rust-lang.org/tree/master/locales" class="dj by kl km kn ko" target="_blank" rel="noopener nofollow">www.rust-lang.org/locales </a>on Github and all translations are in the <code class="gw kp kq kr ks b">.ftl</code> format-type files, and these <code class="gw kp kq kr ks b">.ftl</code> files are synchronized to <a href="https://pontoon.rust-lang.org/" class="dj by kl km kn ko" target="_blank" rel="noopener nofollow">Pontoon</a>.

Rust team uses Pontoon, which is developed by Mozilla and also used in its products for localization, to empower translators to translate the strings easily.

<img class="dz t u gs ak" src="https://miro.medium.com/max/2292/1*cS3nUGj6n4RQ5qhMKNV2Ww.png" role="presentation"><br/>

The photo above is the dashboard of Pontoon. In a particular <code class="gw kp kq kr ks b">.ftl</code> file, all strings are listed in the left and shown in English, there is an input block to enter the translation sentence at the upper right part, and there are history sentences at the lower right part.

It always takes two people to finish each translation of a string, including a “suggestor” who promotes a translation and an approver who agrees with a new or modified string. Note that the condition of suggestions and approvements within the same person is forbidden.

## The gathering of Rust Taiwan community

I first saw the twitter by <a href="https://twitter.com/ManishEarth" class="dj by kl km kn ko" target="_blank" rel="noopener nofollow">Manish</a> and started to think about leading the Rust Taiwan community to deal with this, but I was busy at that moment.

At the same time, the community in China had been working on this issue. They formed up a group and started to translate the website. Alex, who is one of the contributors, had recorded the process of the translation for Simplified Chinese in the post below (in Chinese).

> Alex's post: [Rust官网翻译那些事](https://zhuanlan.zhihu.com/p/71899874)

Several weeks later, I became the organizer of the localization of traditional Chinese, leading the Rust Taiwan Community to engage in this work. Since Alex and the simplified Chinese working group already has experience about the localization task, I asked Alex for help and suggestion. Later, I connected to <a href="https://twitter.com/Argorak" class="dj by kl km kn ko" target="_blank" rel="noopener nofollow">Florian Gilcher</a>, and he helped me to create the ZH-TW team in Pontoon, which requires a member in Rust team to doing that.

If any communities want to localize their own version of the Rust website, all they need is just a team on Pontoon. It takes at least three people to assemble a working team, and the manager who is assigned in the Pontoon has the permission to assign people as either contributors, who can just give suggestions, or translators, who can approve the suggestions, as well as to add a new manager.

We the Rust Taiwan team translated the website at 6/29 (Sat.) on the regular meetup per month. Armed with the efforts of all people in the community, we finished the task after about 3 hours fighting.

Once the localization is done, there is a staging website for testing: <a href="https://www-staging.rust-lang.org/zh-TW/" class="dj by kl km kn ko" target="_blank" rel="noopener nofollow">https://www-staging.rust-lang.org/zh-TW/</a>. We invited more people from other communities, such as the Mozilla community in Taiwan, to help review the correctness and give suggestions. After many times of revisions, the <a href="https://www.rust-lang.org/zh-TW/" class="dj by kl km kn ko" target="_blank" rel="noopener nofollow">ZH-TW version</a> has finally released in threes days just after we published the first staging version.

Cheers! A thousand of champagne bottles uncorked at the same time.

---

## Thanks to committers

<img class="dz t u gs ak" src="https://miro.medium.com/max/2546/1*Vpiblcggu9obdKK0E7wMBw.png" role="presentation"><br/>

<pre><span id="4403" class="ld jt em at ks b fn le lf r lg">The list of contributors up to 2019/7/7</span><span id="564d" class="ld jt em at ks b fn lh li lj lk ll lf r lg">(Order by the list of Pontoon above)<br>吳昱緯/Yu-Wei Wu<br>劉安齊/Liu, An-Chi<br>鄭弘昇/Hong-Sheng Zheng<br>楊善詠/Shan-Yung Yang<br>彭勝宇/Sheng-Yu Peng<br>Weihang Lo<br>許世豪/Shih-Hao Hsu<br>孟昭宏/Paul Meng<br>洪慈吟/Ballfish<br>徐永軒/YongB<br>Cybai<br>謝禹沆/Jezrien Hsieh<br>廖家緯/Chia-Wei Liaw</span></pre>

<img class="dz t u gs ak" src="https://miro.medium.com/max/11668/1*dWIXW3yWFTdOoY1gLL9hXg.png" role="presentation"><br/>
