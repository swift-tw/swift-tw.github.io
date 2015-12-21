---
layout: post
title: "Swift 1.2 與 Xcode 6.3 beta"
date: 2015-05-02 22:02:32 +0800
comments: true
paginate: true
categories: [Swift blog, Swift, Xcode]
---

原文 : [Swift 1.2 and Xcode 6.3 beta](https://developer.apple.com/swift/blog/?id=22)

Swift 1.2和Xcode6.3測試版一起發布了。這個測試版包括效能更強的Swift編譯器，還有Swift語言的新功能。完整的修改列表，請閱讀發行說明 。此文將專注在新特色上。

### 編譯器改善

Swift 1.2編譯器變得更加穩定，並改善在各方面的性能。讓Swift 在 Xcode 中更加好用了。明顯的改進包括：

- **漸進式編譯** -沒有被修改的原始碼將不會被重複編譯，大幅縮短一般情況下的編譯時間。大幅度的改動還是有可能需要重新編譯多個檔案。
- **更快的執行檔** -除錯版本執行速度變快了許多，新的最佳化讓發布版本也變的更快。
- **更好的編譯器診斷** -更清晰的錯誤和警告，還有新的修改建議，讓你更容易寫出高品質的Swift 程式。
- **穩定性改進** - 修復常見的編譯器當機。你應該會發現Xcode的編輯器出現SourceKit警告的次數變少了。

### 新的語言功能

Swift 1.2 得到了進一步的琢磨，來確保安全，可預測的行為。我們持續改善 Swift 和Objective-C之間的相容性。明顯的變化包括：

- **使用 `as!` 來做可能會失敗的轉型** - 可能會失敗的轉型(比如向下轉型) 現在使用新的 `as!` 運算子，讓可能失敗的情況變得更加清晰易讀。
- **Objective-C標頭檔中現在可以有Nullability** - Clang的新Objective-C 擴充讓你可以在Objective-C 中標示Pointer 和 Block 的 Nuallability。 讓Objective-C 的 Framework 和 Swift 相處得更融洽。 
- **Swift 的 enum 現在可以透過 `@objc` 屬性 來匯出到 Objective-C** - 例如下面的Swift 程式碼:

    @objc enum Bear: Int {
      case Black, Grizzly, Polar
    }

匯入 Objective-C 後就成為：

    typedef NS_ENUM(NSInteger, Bear) {
      BearBlack, BearGrizzly, BearPolar
    };

- **`let` 常數變得更加強大和一致** - 新的規則是，`let` 常數必須要在使用前定義( 像 `var` 變數一樣) ，而且只能被定義一次，不能重新定義或修改內容。

現在可以用下面的寫法了：

    let x : SomeThing
    if condition {
      x = foo()
    } else {
      x = bar()
    }
    use(x)

雖然沒有任何的值會改變，但是以前要用`var` 變數才能編譯。Property 現在也用這種新的作法來簡化 initializer。

- **更強大的`if let`** - 單一 `if let` 現在可以展開多個 optional，還可以有附加的布林條件。讓你省下煩人的巢狀結構。
- **新的`Set` 資料結構** - 一個`Set`資料結構用來存放未排序的獨特元素，可以 bridge到`NSSet`，並提供像`Array`和`Dictionary`的用法。

### 結論

感謝各位回報錯誤給我們，希望許多最常見的問題已在這個測試版得到修復。Swift 1.2 在語言和工具上都有重大進步。不過它包含了不相容的改變，所以Xcode 6.3 包含一個遷移工具，幫助自動修改程式相容性。如要使用，點擊 Edit 選單, 再選擇 Convert > To Swift 1.2...

