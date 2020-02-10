---
title: 瀏覽器開發進階實戰（四）font-family
date: 2018-01-01 22:18:07
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
今天來介紹 `font-family`。

當我們對 CSS 定義「字形」的時候，會使用 `font-family`
```
p {
    font-family: "Times New Roman", Georgia, Serif;
}
```
`font-family` 由一串字型名稱組成，預設是瀏覽器會選取第一個字型來呈現，以上面例子來說，假設你的電腦有 `Times New Roman` 這個字型，就會用它來呈現文字；若是沒有的話，則檢查下一個，也就是 `Georgia` 是否有。如果 `font-family` 定義的字型都沒有，就會採用瀏覽器預設的字型。

想了解更多的話可以看 [MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/font-family) 或是 [W3C](https://www.w3.org/TR/CSS2/fonts.html#font-family-prop) 的文件。

而今天要特別講的是**預設字型的「回調」**！
以下這串字：
```
のコ Hello 你好嗎 안녕하세요 Cześć Olá Здравствуйте ♫
```
並不是單一字型就能處理的，即使是預設字型，也要好幾種才能把這串字呈現出來。

所以概念就是一串字，我們先試試看 `font-family` 的順序看能不能把字元呈現，不行的話就使用瀏覽器預設的字型，瀏覽器預設的一樣有順序，就照順序直到可以顯示出來為止。

---
本系列本來都是用 Servo 介紹，不過目前的寫法並沒有實踐 `font-family`，不管如何都直接採用預設的字型。相關的程式碼在[這邊](https://github.com/servo/servo/blob/master/components/gfx/platform/windows/font_list.rs)。但也因為還沒實踐，所以就不拿來舉例，若是大家有興趣可以一起來貢獻把它完成。

不過 Firefox 的 Gecko 理所當然有把它實踐囉！
這邊來看 Gecko 針對 Windows 平台的[程式碼](https://github.com/mozilla/gecko-dev/blob/153c591749d7807372a4ba99e2685b5461d36cf7/gfx/thebes/gfxWindowsPlatform.cpp#L604)，因為不同平台的處理方式還是有差異，所以處理字型的部分有特別切開。

Gecko 使用 `GetCommonFallbackFonts` 這個函式來處理字型。
```
gfxWindowsPlatform::GetCommonFallbackFonts(uint32_t aCh, uint32_t aNextCh,
                                           Script aRunScript,
                                           nsTArray<const char*>& aFontList)
{
    EmojiPresentation emoji = GetEmojiPresentation(aCh);
    if (emoji != EmojiPresentation::TextOnly) {
        if (aNextCh == kVariationSelector16 ||
           (aNextCh != kVariationSelector15 &&
            emoji == EmojiPresentation::EmojiDefault)) {
            // if char is followed by VS16, try for a color emoji glyph
            aFontList.AppendElement(kFontSegoeUIEmoji);
            aFontList.AppendElement(kFontEmojiOneMozilla);
        }
    }

    // Arial is used as the default fallback for system fallback
    aFontList.AppendElement(kFontArial);

    if (!IS_IN_BMP(aCh)) {
        uint32_t p = aCh >> 16;
        if (p == 1) { // SMP plane
            aFontList.AppendElement(kFontSegoeUISymbol);
            aFontList.AppendElement(kFontEbrima);
            aFontList.AppendElement(kFontNirmalaUI);
            aFontList.AppendElement(kFontCambriaMath);
        }
    } else {
        uint32_t b = (aCh >> 8) & 0xff;

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
        // 中間省略
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
```

可以看到光瀏覽器預設字型就超過四十種，這也是因為各種奇形怪狀的符號實在太多，不同國家的文字使用的字型也不一樣，為了讓各種字元都能顯示，才不會出現顯示不出來變成框框的情形。

---
希望對大家有幫助，我們明天見！
                                                        
