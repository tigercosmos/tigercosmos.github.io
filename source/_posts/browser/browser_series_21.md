---
title: 瀏覽器開發進階實戰（四）font-family
date: 2018-01-01 22:18:07
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x4ECA;&#x5929;&#x4F86;&#x4ECB;&#x7D39; <code>font-family</code>&#x3002;</p>
<p>&#x7576;&#x6211;&#x5011;&#x5C0D; CSS &#x5B9A;&#x7FA9;&#x300C;&#x5B57;&#x5F62;&#x300D;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x6703;&#x4F7F;&#x7528; <code>font-family</code></p>
<pre><code>p {
    font-family: &quot;Times New Roman&quot;, Georgia, Serif;
}
</code></pre>
<p><code>font-family</code> &#x7531;&#x4E00;&#x4E32;&#x5B57;&#x578B;&#x540D;&#x7A31;&#x7D44;&#x6210;&#xFF0C;&#x9810;&#x8A2D;&#x662F;&#x700F;&#x89BD;&#x5668;&#x6703;&#x9078;&#x53D6;&#x7B2C;&#x4E00;&#x500B;&#x5B57;&#x578B;&#x4F86;&#x5448;&#x73FE;&#xFF0C;&#x4EE5;&#x4E0A;&#x9762;&#x4F8B;&#x5B50;&#x4F86;&#x8AAA;&#xFF0C;&#x5047;&#x8A2D;&#x4F60;&#x7684;&#x96FB;&#x8166;&#x6709; <code>Times New Roman</code> &#x9019;&#x500B;&#x5B57;&#x578B;&#xFF0C;&#x5C31;&#x6703;&#x7528;&#x5B83;&#x4F86;&#x5448;&#x73FE;&#x6587;&#x5B57;&#xFF1B;&#x82E5;&#x662F;&#x6C92;&#x6709;&#x7684;&#x8A71;&#xFF0C;&#x5247;&#x6AA2;&#x67E5;&#x4E0B;&#x4E00;&#x500B;&#xFF0C;&#x4E5F;&#x5C31;&#x662F; <code>Georgia</code> &#x662F;&#x5426;&#x6709;&#x3002;&#x5982;&#x679C; <code>font-family</code> &#x5B9A;&#x7FA9;&#x7684;&#x5B57;&#x578B;&#x90FD;&#x6C92;&#x6709;&#xFF0C;&#x5C31;&#x6703;&#x63A1;&#x7528;&#x700F;&#x89BD;&#x5668;&#x9810;&#x8A2D;&#x7684;&#x5B57;&#x578B;&#x3002;</p>
<p>&#x60F3;&#x4E86;&#x89E3;&#x66F4;&#x591A;&#x7684;&#x8A71;&#x53EF;&#x4EE5;&#x770B; <a href="https://developer.mozilla.org/zh-TW/docs/Web/CSS/font-family" target="_blank">MDN</a> &#x6216;&#x662F; <a href="https://www.w3.org/TR/CSS2/fonts.html#font-family-prop" target="_blank">W3C</a> &#x7684;&#x6587;&#x4EF6;&#x3002;</p>
<p>&#x800C;&#x4ECA;&#x5929;&#x8981;&#x7279;&#x5225;&#x8B1B;&#x7684;&#x662F;<strong>&#x9810;&#x8A2D;&#x5B57;&#x578B;&#x7684;&#x300C;&#x56DE;&#x8ABF;&#x300D;</strong>&#xFF01;<br>
&#x4EE5;&#x4E0B;&#x9019;&#x4E32;&#x5B57;&#xFF1A;</p>
<pre><code>&#x306E;&#x30B3; Hello &#x4F60;&#x597D;&#x55CE; &#xC548;&#xB155;&#xD558;&#xC138;&#xC694; Cze&#x15B;&#x107; Ol&#xE1; &#x417;&#x434;&#x440;&#x430;&#x432;&#x441;&#x442;&#x432;&#x443;&#x439;&#x442;&#x435; &#x266B;
</code></pre>
<p>&#x4E26;&#x4E0D;&#x662F;&#x55AE;&#x4E00;&#x5B57;&#x578B;&#x5C31;&#x80FD;&#x8655;&#x7406;&#x7684;&#xFF0C;&#x5373;&#x4F7F;&#x662F;&#x9810;&#x8A2D;&#x5B57;&#x578B;&#xFF0C;&#x4E5F;&#x8981;&#x597D;&#x5E7E;&#x7A2E;&#x624D;&#x80FD;&#x628A;&#x9019;&#x4E32;&#x5B57;&#x5448;&#x73FE;&#x51FA;&#x4F86;&#x3002;</p>
<p>&#x6240;&#x4EE5;&#x6982;&#x5FF5;&#x5C31;&#x662F;&#x4E00;&#x4E32;&#x5B57;&#xFF0C;&#x6211;&#x5011;&#x5148;&#x8A66;&#x8A66;&#x770B; <code>font-family</code> &#x7684;&#x9806;&#x5E8F;&#x770B;&#x80FD;&#x4E0D;&#x80FD;&#x628A;&#x5B57;&#x5143;&#x5448;&#x73FE;&#xFF0C;&#x4E0D;&#x884C;&#x7684;&#x8A71;&#x5C31;&#x4F7F;&#x7528;&#x700F;&#x89BD;&#x5668;&#x9810;&#x8A2D;&#x7684;&#x5B57;&#x578B;&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x9810;&#x8A2D;&#x7684;&#x4E00;&#x6A23;&#x6709;&#x9806;&#x5E8F;&#xFF0C;&#x5C31;&#x7167;&#x9806;&#x5E8F;&#x76F4;&#x5230;&#x53EF;&#x4EE5;&#x986F;&#x793A;&#x51FA;&#x4F86;&#x70BA;&#x6B62;&#x3002;</p>
<hr>
<p>&#x672C;&#x7CFB;&#x5217;&#x672C;&#x4F86;&#x90FD;&#x662F;&#x7528; Servo &#x4ECB;&#x7D39;&#xFF0C;&#x4E0D;&#x904E;&#x76EE;&#x524D;&#x7684;&#x5BEB;&#x6CD5;&#x4E26;&#x6C92;&#x6709;&#x5BE6;&#x8E10; <code>font-family</code>&#xFF0C;&#x4E0D;&#x7BA1;&#x5982;&#x4F55;&#x90FD;&#x76F4;&#x63A5;&#x63A1;&#x7528;&#x9810;&#x8A2D;&#x7684;&#x5B57;&#x578B;&#x3002;&#x76F8;&#x95DC;&#x7684;&#x7A0B;&#x5F0F;&#x78BC;&#x5728;<a href="https://github.com/servo/servo/blob/master/components/gfx/platform/windows/font_list.rs" target="_blank">&#x9019;&#x908A;</a>&#x3002;&#x4F46;&#x4E5F;&#x56E0;&#x70BA;&#x9084;&#x6C92;&#x5BE6;&#x8E10;&#xFF0C;&#x6240;&#x4EE5;&#x5C31;&#x4E0D;&#x62FF;&#x4F86;&#x8209;&#x4F8B;&#xFF0C;&#x82E5;&#x662F;&#x5927;&#x5BB6;&#x6709;&#x8208;&#x8DA3;&#x53EF;&#x4EE5;&#x4E00;&#x8D77;&#x4F86;&#x8CA2;&#x737B;&#x628A;&#x5B83;&#x5B8C;&#x6210;&#x3002;</p>
<p>&#x4E0D;&#x904E; Firefox &#x7684; Gecko &#x7406;&#x6240;&#x7576;&#x7136;&#x6709;&#x628A;&#x5B83;&#x5BE6;&#x8E10;&#x56C9;&#xFF01;<br>
&#x9019;&#x908A;&#x4F86;&#x770B; Gecko &#x91DD;&#x5C0D; Windows &#x5E73;&#x53F0;&#x7684;<a href="https://github.com/mozilla/gecko-dev/blob/153c591749d7807372a4ba99e2685b5461d36cf7/gfx/thebes/gfxWindowsPlatform.cpp#L604" target="_blank">&#x7A0B;&#x5F0F;&#x78BC;</a>&#xFF0C;&#x56E0;&#x70BA;&#x4E0D;&#x540C;&#x5E73;&#x53F0;&#x7684;&#x8655;&#x7406;&#x65B9;&#x5F0F;&#x9084;&#x662F;&#x6709;&#x5DEE;&#x7570;&#xFF0C;&#x6240;&#x4EE5;&#x8655;&#x7406;&#x5B57;&#x578B;&#x7684;&#x90E8;&#x5206;&#x6709;&#x7279;&#x5225;&#x5207;&#x958B;&#x3002;</p>
<p>Gecko &#x4F7F;&#x7528; <code>GetCommonFallbackFonts</code> &#x9019;&#x500B;&#x51FD;&#x5F0F;&#x4F86;&#x8655;&#x7406;&#x5B57;&#x578B;&#x3002;</p>
<pre><code>gfxWindowsPlatform::GetCommonFallbackFonts(uint32_t aCh, uint32_t aNextCh,
                                           Script aRunScript,
                                           nsTArray&lt;const char*&gt;&amp; aFontList)
{
    EmojiPresentation emoji = GetEmojiPresentation(aCh);
    if (emoji != EmojiPresentation::TextOnly) {
        if (aNextCh == kVariationSelector16 ||
           (aNextCh != kVariationSelector15 &amp;&amp;
            emoji == EmojiPresentation::EmojiDefault)) {
            // if char is followed by VS16, try for a color emoji glyph
            aFontList.AppendElement(kFontSegoeUIEmoji);
            aFontList.AppendElement(kFontEmojiOneMozilla);
        }
    }

    // Arial is used as the default fallback for system fallback
    aFontList.AppendElement(kFontArial);

    if (!IS_IN_BMP(aCh)) {
        uint32_t p = aCh &gt;&gt; 16;
        if (p == 1) { // SMP plane
            aFontList.AppendElement(kFontSegoeUISymbol);
            aFontList.AppendElement(kFontEbrima);
            aFontList.AppendElement(kFontNirmalaUI);
            aFontList.AppendElement(kFontCambriaMath);
        }
    } else {
        uint32_t b = (aCh &gt;&gt; 8) &amp; 0xff;

        switch (b) {
        case 0x05:
            aFontList.AppendElement(kFontEstrangeloEdessa);
            aFontList.AppendElement(kFontCambria);
            break;
        case 0x06:
            aFontList.AppendElement(kFontMicrosoftUighur);
            break;
        case 0x07:
            aFontList.AppendElement(kFontEstrangeloEdessa);
            aFontList.AppendElement(kFontMVBoli);
            aFontList.AppendElement(kFontEbrima);
            break;
        case 0x09:
            aFontList.AppendElement(kFontNirmalaUI);
            aFontList.AppendElement(kFontUtsaah);
            aFontList.AppendElement(kFontAparajita);
            break;
        case 0x0a:
        case 0x0b:
        case 0x0c:
        case 0x0d:
            aFontList.AppendElement(kFontNirmalaUI);
            break;
        case 0x0e:
        // ...
        // ...
        // &#x4E2D;&#x9593;&#x7701;&#x7565;
        // ...
        // ...
       case 0xff:
            aFontList.AppendElement(kFontMicrosoftJhengHei);
            break;
        default:
            break;
        }
    }

    // Arial Unicode MS has lots of glyphs for obscure characters,
    // use it as a last resort
    aFontList.AppendElement(kFontArialUnicodeMS);
}
</code></pre>
<p>&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x5149;&#x700F;&#x89BD;&#x5668;&#x9810;&#x8A2D;&#x5B57;&#x578B;&#x5C31;&#x8D85;&#x904E;&#x56DB;&#x5341;&#x7A2E;&#xFF0C;&#x9019;&#x4E5F;&#x662F;&#x56E0;&#x70BA;&#x5404;&#x7A2E;&#x5947;&#x5F62;&#x602A;&#x72C0;&#x7684;&#x7B26;&#x865F;&#x5BE6;&#x5728;&#x592A;&#x591A;&#xFF0C;&#x4E0D;&#x540C;&#x570B;&#x5BB6;&#x7684;&#x6587;&#x5B57;&#x4F7F;&#x7528;&#x7684;&#x5B57;&#x578B;&#x4E5F;&#x4E0D;&#x4E00;&#x6A23;&#xFF0C;&#x70BA;&#x4E86;&#x8B93;&#x5404;&#x7A2E;&#x5B57;&#x5143;&#x90FD;&#x80FD;&#x986F;&#x793A;&#xFF0C;&#x624D;&#x4E0D;&#x6703;&#x51FA;&#x73FE;&#x986F;&#x793A;&#x4E0D;&#x51FA;&#x4F86;&#x8B8A;&#x6210;&#x6846;&#x6846;&#x7684;&#x60C5;&#x5F62;&#x3002;</p>
<hr>
<p>&#x5E0C;&#x671B;&#x5C0D;&#x5927;&#x5BB6;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x6211;&#x5011;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
<hr>
<blockquote>
<h3><em><strong>&#x95DC;&#x65BC;&#x4F5C;&#x8005;</strong></em></h3>
<h2>&#x5289;&#x5B89;&#x9F4A;</h2>
<p>&#x8EDF;&#x9AD4;&#x5DE5;&#x7A0B;&#x5E2B;&#xFF0C;&#x71B1;&#x611B;&#x5BEB;&#x7A0B;&#x5F0F;&#xFF0C;&#x66F4;&#x559C;&#x6B61;&#x63A8;&#x5EE3;&#x7A0B;&#x5F0F;&#x8B93;&#x66F4;&#x591A;&#x4EBA;&#x5B78;&#x6703;</p>
<ul>
<li>
<a href="https://tigercosmos.github.io" target="_blank">&#x500B;&#x4EBA;&#x7DB2;&#x7AD9;</a>
</li>
<li>
<a href="https://github.com/tigercosmos" target="_blank">Github</a>
</li>
<li>
<a href="https://www.facebook.com/CodingNeutrino/" target="_blank">FB&#x7C89;&#x5C08;--&#x5FAE;&#x4E2D;&#x5B50;</a>
</li>
</ul>
</blockquote>
 <br>
                                                    </div>
                    </div>
                
