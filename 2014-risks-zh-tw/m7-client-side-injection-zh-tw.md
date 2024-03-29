---

layout: col-sidebar
title: "M7: 客戶端的注入"
---

# 威脅主體

**應用層面 特定**

考慮任何可以向行動應用發送不受信任數據的人，包括外部用戶、內部用戶、應用程式本身或行動上的其他惡意應用。

# 攻擊媒介	

**利用難度 簡單**

攻擊者載入簡單基於文本的攻擊，該攻擊利用行動應用程式中鎖定的詮釋器語法。幾乎任何數據源都可能成為注入媒介，包括資源文件或應用程式本身。	

# 安全層面的強度	

**普及性 常見** <br />
**偵測性 簡單**

客戶端注入導致能透過行動應用程式在行動裝置上執行惡意程式碼。通常，這種惡意程式碼以數據的形式提供給威脅主體，威脅主體通過多種不同的方式將其輸入到行動應用中。數據格式不正確，並且被支援行動應用程式的底層架構所處理（就像所有其他數據一樣）。在處理過程中，這個特殊的數據強制背景切換，框架將數據重新詮釋為可執行程式碼。程式碼具有惡意性質並由應用程式執行。在“最好的情況”下，程式碼以與無意中執行此程式碼的用戶在相同的作用域和訪問權限運行。在“最壞的情況”下，程式碼以特權權限運行，範圍更廣，損害潛力比“最好的情況”更大。還有其他形式的客戶端注入，涉及通過二進制攻擊將二進制程式碼直接注入到行動應用中。這種執行惡意程式碼的暴力法可能導致比數據注入更大的損害潛力。有關二進制攻擊的更多信息，請參見M10。

# 技術性影響	

**影響程度 中等**

為了正確評估技術影響，您必須對應用程式進行威脅建模。對於應用程式而言，注入攻擊(例如在行動裝置上的SQL注入)可能會非常嚴重，特別是如果您的應用程式涉及單個應用程式上的多個用戶帳戶、共享裝置或付費內容。其他注入點目的在於溢出(overflow)應用程式元件，但由於應用程式語言的託管程式碼保護，較不可能取得影響程度大的結果。

# 業務影響
	
**應用程式/業務 特定** 
		
客戶端注入的業務影響取決於攻擊者執行的惡意程式碼的性質。通常，惡意程式碼會竊取敏感信息（密碼；會話cookie；個人身份信息等）。因此，相關的業務影響包括：
- 欺詐; 以及
- 隱私侵犯。


# 我是否容易受到「客戶端的注入」的攻擊？

確定應用程式是否容易受到注入攻擊的最佳方法是識別輸入源，並驗證用戶或應用程式提供的數據是否受到輸入驗證，防止程式碼注入。檢查程式碼是查看應用程式是否正確處理數據的一種快速而準確的方法。程式碼分析工具可以幫助安全分析師找到詮釋器的使用並跟踪數據在應用程式中的流動。手動侵入測試人員可以通過製造破口來確認這些問題，以確認漏洞。

由於在行動應用中數據可以來自許多來源，因此重要的是按照它們試圖實現的目標將它們列出。一般來說，對行動裝置的注入攻擊主要針對以下方面：


**裝置上的數據:**

- SQL注入：SQLite（許多手機的默認數據存儲機制）可能會受到注入攻擊，就像在Web應用程式中一樣。當您的應用程式包含多個不同的用戶、付費/可解鎖的內容等時，使用這種注入查看數據的風險是危險的。
- 本地文件包含：行動裝置上的文件處理存在與上述相同的風險，除了它涉及讀取您可能在應用程式目錄中查看的檔案之外。

**行動用戶的會話:**

- JavaScript注入（XSS等）：行動瀏覽器也可能受到JavaScript注入的影響。通常，行動瀏覽器可以訪問行動應用程式的cookie，這可能導致會話被盜。

**應用程式介面或功能:**

- 許多應用程式介面或語言函數可以接受數據，並且可以進行模糊測試以使應用程式崩潰。雖然由於手機平台為託管程式碼而不會導致溢出，但有幾個缺陷已被用作旨在獲取 root 權限或越獄設備的漏洞鏈中的「用戶區」漏洞。。

**二進制程式碼本身:**

- 行動惡意軟體或其他惡意應用程式可能會對表示層（HTML、JavaScript、 CSS）或行動應用程式執行檔的實際二進制檔案執行二進制攻擊。 這些程式碼注入由行動應用程式的框架或二進制檔案本身在運行時執行。


# 如何防止「客戶端的注入」？

一般來說，要保護應用程序免受客戶端注入的影響，需要查看應用程式可以從哪些地方接收數據，並應用某種形式的輸入驗證。在某些情況下，這很簡單，但對於其他情況，則更為復雜，請參見以下內容:


**針對 iOS 的最佳實踐:**


- **SQLite注入:** 在設計SQLite查詢時，確保用戶提供的數據被傳遞給參數化查詢。可以通過查看所使用的格式指定符來發現。一般來說，危險的用戶提供的數據將被插入“%@”而不是正確的參數化查詢指定符“?”。
- **JavaScript注入（XSS等）**: 確保所有UIWebView呼叫在沒有進行正確的輸入驗證之前不執行。如果可能，應用過濾器過濾危險的JavaScript字符，在渲染之前使用白名單而不是黑名單字元策略。如果可能，呼叫行動 Safari，而不是在可以存取您的應用程式的 UIWebkit 內部進行渲染。
- **本地文件包含**: 對 NSFileManager 呼叫使用輸入驗證。
- **XML 注入**: 使用 libXML2 而不是 NSXMLParser。
- **格式字串注入**: 幾種 Objective C 方法容易受到格式字串攻擊:
  - NSLog, [NSString stringWithFormat:], [NSString initWithFormat:], [NSMutableString appendFormat:], [NSAlert informativeTextWithFormat:], [NSPredicate predicateWithFormat:], [NSException format:], NSRunAlertPanel.
  - 不要讓您無法控制的來源（例如其他應用程式或 Web 服務的使用者資料和訊息）控制格式字串的任何部分。
- **經典 C 攻擊**: Objective C 是 C 的超集，避免使用容易受到注入的舊 C 函數，例如：strcat、strcpy、strncat、strncpy、sprint、vsprintf、gets 等。

**針對 Android 的最佳實踐：**


- **SQL 注入**: 處理動態查詢或內容提供者時，請確保您使用參數化查詢。
- **JavaScript 注入 (XSS)**: 驗證是否對任何 WebView 停用 JavaScript 和插件支援（通常是預設設定）。
- **本地文件包含**: 驗證是否對任何 WebView 停用檔案系統存取 (webview.getSettings().setAllowFileAccess(false);)。
- **意圖注入/模糊測試**: 驗證操作和資料是否經過所有活動的意圖過濾器進行驗證。

**Android 和 iOS 的二進位注入/預防修改：**


- 有關預防、檢測和應對對手二進制注入的最佳實踐的更多信息，請參閱 M10。

# 攻擊情境舉例

Classic client-side injection scenarios include the following:

1. SQL注入 - 從行動應用程式的伺服器檢索的數據包含格式不正確的數據，導致在行動裝置的本地資料庫中發生本地SQL注入。本地SQL注入可能導致本地惡意軟體的注入、信息竊取等；
2. 從一個Android應用程式傳遞到另一個應用程式的惡意意圖可能導致緩衝區溢出，從而允許執行惡意程式碼；
3. 跨站腳本攻擊 - 通過惡意軟體或其他應用程式對本地HTML的修改導致能夠在應用程式的表示層中執行惡意JavaScript。這可能導致信息竊取。

# 參考資料

- [Apple’s Secure Coding Guide](https://developer.apple.com/library/mac/#documentation/security/conceptual/SecureCodingGuide)
- [Fortify Software: Format Strings - Is Objective C Objectively Safer?](http://blog.fortify.com/blog/2012/07/25/Format-Strings-Is-Objective-C-Objectively-Safer)
- [Ilja Van Sprundel – Auditing iPhone and iPad Applications](http://www.youtube.com/watch?v=FJvyLUjbAy0)
- [Adventures with Android WebViews](http://labs.mwrinfosecurity.com/blog/2012/04/23/adventures-with-android-webviews/)