---
layout: page
title: 關於Swift
---

Swift是一個安全，高效能的現代化通用程式語言，

Swift 的目標是創造一個對不管對系統程式設計，行動和桌上型應用程式，雲端服務來說，都是最棒的程式語言． 最重要的是，Swift被設計來讓撰寫和維護_正確的_程式變得簡單． 為了達到這個目標，我們相信Swift 的語法應該是：

**安全的．** 最直接的寫法應該也是安全的． 未定義的行為是安全的敵人．開發者的失誤應該要在程式公開發行前被發現． 專注於安全有時會讓人覺得Swift綁手綁腳，但我們相信長久來說，清晰的程式可以省下很多時間．

**快速的．** 我們希望Swift 可以取代 C-based 語言(C, C++, Objective-C)． 所以Swift 必須在大多數的情況下和這些語言有一樣好的效能． 效能必須是可預測且一致的，不能時快時慢． 擁有創新特色的程式語言有很多，但是跑得快的卻很少．

**簡潔的．** 感謝數十年來電腦科學的進步，Swift 可以提供易於使用的文法，搭配開發者想要的先進功能． 但Swift 不會停滯不前． 我們會觀察程式語言的進展，接納各種進步，持續改進Swift．

工具是Swift 生態圈重要的一部分． 我們努力得整合開發者工具，讓開發變得更快，讓錯誤訊息變得更清晰，提供互動式的開發體驗． 工具讓語言變得更有威力，像是Xcode 中的Swift Playground，或是web-based REPL．

## 特色

Swift 包含讓各種寫Code 和讀Code 更容易的特色，同時讓開發者獲得系統開發所需要的控制權． Swift 支援 inferred types(型態推斷) 讓程式更加清晰和不易出錯，而 module(模組) 消滅了header(標頭檔) 和提供了namespace(命名空間)。 全自動控管記憶體，而且不用打分號(;)． Swift 也從其他語言借了不少東西，比方說從 Objective-C 借來的 named parameters(具名引數) 讓 Swift 中的API 更加清晰易讀與容易維護．

Swift 的各種特色讓他成為一個威力強大且易於使用的語言． 其他的Swift 特色包括：

- Closures unified with function pointers(統一的閉包與函數指標）
- Tuples and multiple return values(多元組和多回傳值)
- Generics (泛型)
- Fast and concise iteration over a range or collection (快速且清晰的對集合或範圍做迭代)
- Structs that support methods, extensions, and protocols (支援方法，擴充與協議的結構體)
- Functional programming patterns(函數式程式設計模式), e.g., map and filter
- Powerful error handling built-in (內建強大的錯誤處理)
- Advanced control flow with `do`, `guard`, `defer`, and `repeat` keywords ( 先進的流程控制)

### 安全性

Swift 從一開始就被設計成比 C-based 語言更安全，避免了各種不安全的語法． Variable (變數) 一定要在使用前 initialize (初始化)，Array 和 Integer 有 overflow（溢位） 檢查，而記憶體有自動管理． 語法被設計成讓你的意圖明顯，舉例來說定義 variable 的 `var` 和定義 constant 的`let`就被區隔開來．

另一個安全機制是 Swift object 預設成不能是`nil`， 試圖使用`nil` object 會產生 compile-time 錯誤． 這讓程式變得更加清楚與安全，且預防了常見的runtime 錯誤． 然而， 有的時候還是需要 `nil` ，為此 Swift 有一個創新的功能， **optionals** ． 一個 optional 值有可能是 `nil` ，但 Swift 語法強制使用 `?` 來確認你知道自己在做什麼．而且你會安全地處理它．

## Swift.org 與 Open Source

在2015年12月3號，Swift 語言， supporting libraries, debugger, 與 package manager 使用 [Apache 2.0 license with a Runtime Library Exception](https://swift.org/LICENSE.txt) 發佈了，而 Swift.org 被創造來作為發佈平台． source code 在 [GitHub](http://github.com/apple) 上，任何人都可以很容易的拿到它，build 它，甚至創造 Pull Request 來做出貢獻． 歡迎大家加入，也歡迎大家 [回報問題](https://swift.org/contributing/#reporting-bugs)． 這裏也有很棒的 [新手指南(英文)](https://swift.org/getting-started/) ．

這個專案由核心工程師和社群一起決定未來的方向，一群程式碼負責人則會負責日常的管理． Technical leaders 來自社群的 contributors ，任何人都有機會領導 Swift 中的一塊領域． [社群指南(英文)](https://swift.org/community/) 包含 Swift 社群的運作詳情．

### 專案

Swift 語言包含了許多專案，每一個都有自己的 repositoriy． 目前的專案包含：

- [Swift 編譯器](https://swift.org/compiler-stdlib/) 
- [語言內建的 standard library](https://swift.org/compiler-stdlib/)
- 提供高階功能的 [Core libraries](https://swift.org/core-libraries/)
- [LLDB debugger](https://swift.org/lldb/) 包含 Swift REPL
- [Swift package manager](https://swift.org/package-manager/) 用來散佈和建構 Swift 程式碼

## 各平台支援

現在Swift可以被自由的移植到各個平台和裝置是開源 Swift 的最大好處之一．

我們的目標是保持程式碼在各平台上的通用性，雖然實作會和平台有關． 主要的例子像是，在 Apple 平台上 Swift 包含了 Objective-C runtime, 因為 Apple 平台的 Framework 像是 UIKit & AppKit 需要它． 在其他的平台上，比方說Linux，Swift 就不包含 Objective-C runtime，因為它不必要．

[Swift core libraries](https://swift.org/core-libraries/) 專案希望能加強 Swift 跨平台的能力，在不使用Objective-C runtime 的情況下，提供 portable 的基礎 Apple frameworks實作( 比方說 Foundation)． 雖然 core libraries 還在開發初期，最後一定能提升程式碼在各平台上的相容性．

### Apple 平台

Open-source Swift 可以在 Mac 對所有 Apple 平台做開發: iOS, OS X, watchOS, 與 tvOS. 除此之外，open-source Swift 的 binary build 能和 Xcode developer tools 結合，包含完整的 Xcode build system 支援，編輯器內的自動完成，和整合式的除錯，讓任何人都能在熟悉的 Cocoa 與 Cocoa Touch 環境內試驗最新版的 Swift．

### Linux

Open-source Swift 可以在 Linux 開發 Swift 程式庫與應用程式． open-source binary builds 包含 Swift compiler, standard library, Swift REPL 與 debugger (LLDB), 以及 [core libraries](https://swift.org/core-libraries/), 所以任何人都可以立刻開發 Swift．

### 新平台

我們期待看到 Swift 能在其他的新地方使用． 我們真心相信這個語言能讓程式更安全，更快速，更容易維護． 我們期待你幫助移植 Swift 到更多的平台上．

Copyright © 2015 Apple Inc. All rights reserved.

Swift and the Swift logo are trademarks of Apple Inc.

