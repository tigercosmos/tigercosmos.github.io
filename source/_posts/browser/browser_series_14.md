---
title: 瀏覽器開發進階實戰（一） value sanitization of input type
date: 2017-12-25 23:42:49
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
我們現在了解如何開發一個簡易版的瀏覽器了。在本系列的先前文章當中，已經帶大家一步一步完成一個「玩具」等級的瀏覽器，雖然功能很簡陋，很多東西不支援，但卻是貨真價實的瀏覽器！

但我們並不滿足，我們想做的是一個真正的產品，是功能齊全、設計良好、效能超棒的瀏覽器！這麼一個產品當然不可能隨手就做出來，市面上的瀏覽器，哪一個不是開發十年，由無數開發者所堆砌出來的呢？

本系列的進階實戰部分將以 [Servo](https://github.com/servo/servo) 專案為例，實作一些功能，讓大家了解真正開發瀏覽器是怎麼一回事。

我們都知道，一台機器是由好幾個大組件構成，大組建又是好多小零件所拼起來，小零件可能又是由幾個素材所製造。
好了，所以我們今天講的東西是，HTML > input 元素 > type > value sanitization(檢查數值)，這樣講大家可能不清處，究竟 type 是什麼？

input 的 type 就是：
```
<input type="month">
<input type="week">
<input type="time">
<input type="color">
```

然後 `type` 會有 `value` 就像是：
```
<input type="month" value="2014-09">
<input type="week" value="2014-W52">
<input type="time" value="17:30:23">
<input type="color" value="#ffffff">
```

可是問題就來了，誰知道你給的數值是不是正確的呢？
例如：
```
<input type="month" value="2014-29">
```
月份最高就到 12，所以上面的當然就是錯的！

所以針對這個，有 [WHATWG的文件](https://html.spec.whatwg.org/multipage/input.html)可以參考。

像是以 `week` 這個 type 為例：
文件有說明怎樣才是有效的數值：https://html.spec.whatwg.org/multipage/input.html#week-state-(type=week):value-sanitization-algorithm
判斷有效數值的演算法也有文件： https://html.spec.whatwg.org/multipage/#parse-a-week-string

然後我們就可以實作了，這段程式是我寫的，也是照著文件寫，每個步驟都有對應文件上的步驟編號。

---
首先從 input element 中取得對應的 type 的數值 ([Gthub](https://github.com/servo/servo/blob/7aae164fcdb8ab308bfa0806e1123e9b7eb73a7c/components/script/dom/htmlinputelement.rs#L1008-L1012))
```
InputType::Week => {
    // 取得數值
    let mut textinput = self.textinput.borrow_mut();
    // 判斷是否合理
    if !textinput.single_line_content().is_valid_week_string() {
        // 不是有效的數值就清除成 ""
        *textinput.single_line_content_mut().clear();
    }
}
```

上面可以看到 `is_valid_week_string()`，這串是 DOM 的 binding，也就是自身的方法，可以用來檢查數值。
```
pub fn is_valid_week_string(&self) -> bool {
    // 嘗試解析
    parse_week_string(&*self.0).is_ok()
}
```

檢查數值的時候會嘗試解析字串，這邊是解析的演算法，解析成功的話就會使上面的 `is_valid_week_string` 為真，就算通過檢查。([Github](https://github.com/servo/servo/blob/7aae164fcdb8ab308bfa0806e1123e9b7eb73a7c/components/script/dom/bindings/str.rs#L457-L497))
```
/// https://html.spec.whatwg.org/multipage/#parse-a-week-string
fn parse_week_string(value: &str) -> Result<(u32, u32), ()> {
    // Step 1, 2, 3 取得年份，為 "-" 切開的第一個字串
    let mut iterator = value.split('-');
    let year = iterator.next().ok_or(())?;

    // Step 4 如果年份不是四個數字，且從字串轉成數字出錯，就回傳錯
    let year_int = year.parse::<u32>().map_err(|_| ())?;
    if year.len() < 4 || year_int == 0 {
        return Err(());
    }

    // Step 5, 6 如果能解析下個字串，且為 W 才通過檢查
    let week = iterator.next().ok_or(())?;
    let (week_first, week_last) = week.split_at(1);
    if week_first != "W" {
        return Err(());
    }

    // Step 7 週數為兩個數字
    let week_int = week_last.parse::<u32>().map_err(|_| ())?;
    if week_last.len() != 2 {
        return Err(());
    }

    // Step 8 當年最大週數
    let max_week = max_week_in_year(year_int);

    // Step 9 週數必須在最大週數以內
    if week_int < 1 || week_int > max_week {
        return Err(());
    }

    // Step 10 如果字串還有東西，那就是錯的
    if iterator.next().is_some() {
        return Err(());
    }

    // Step 11 回傳解析結果
    Ok((year_int, week_int))
}
```

---
以上就是 value sanitization of input type  的示範，事實上瀏覽器中有很多這種小功能必須實作，也就是我一開始舉例的小零件，每個螺絲都很重要，才能完成我們最棒的瀏覽器！

希望有幫到大家，大家明天見！

