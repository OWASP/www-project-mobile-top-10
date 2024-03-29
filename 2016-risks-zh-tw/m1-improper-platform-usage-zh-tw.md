---

layout: col-sidebar
title: "M1: 不當的使用平台"
---

# 威脅主體

**應用層面 特定**

這個類別涵蓋了對平台功能的誤用或未使用平台安全控制的情況。這可能包括 Android intents、平台權限、對 TouchID 的誤用、Keychain 或其他作為行動作業系統一部分的安全控制的誤用。

# 攻擊媒介	

**利用難度 簡單**

此攻擊媒介與傳統OWASP十大中的攻擊媒介相同。在這裡任何公開的API呼叫都有可能成為攻擊媒介。

# 安全層面的強度	

**普及性 常見** <br />
**偵測性 平均**

要利用這個漏洞，組織必須公開一個被行動應用程式使用的 Web 服務或 API 呼叫。公開的服務或 API 呼叫是使用不安全的編碼技術實現的，這會在伺服器上產生OWASP十大漏洞。透過行動介面，對手能夠對弱點端點提供惡意輸入或預期外的事件序列。因此，攻擊者實現了伺服器上原初的OWASP十大漏洞。

# 技術性影響	

**影響程度 嚴重**

這個漏洞的技術影響相當於透過行動裝置利用的相關漏洞的技術影響（在OWASP十大中定義）。
		 	
例如，攻擊者可能透過行動裝置利用跨站腳本（Cross-Site Scripting，XSS）漏洞。這對應於OWASP十大的A3 - XSS類別，技術影響為中度。

# 業務影響
	
**應用程式/業務 特定** 
		
這個漏洞的業務影響相當於透過行動裝置利用相關漏洞的業務影響（在OWASP十大中定義）。

例如，攻擊者可能透過行動裝置利用跨站腳本（Cross-Site Scripting，XSS）漏洞。這對應於OWASP十大的A3 - XSS類別的業務影響。


# 我是否容易受到「不當的使用平台」的攻擊？

此風險類別的特徵是平台（iOS、Android、Windows Phone 等）提供了一個已經被記錄和深入了解的功能或能力。應用程式未能使用該功能或使用不當。這與其他行動的十大風險不同，因為設計和實施不僅僅是應用程式開發者的問題。

有許多方式會使行動應用程式遇到這種風險。

1. **違反發佈的指南** 如果應用程式違反了製造商建議的最佳做法，它將暴露於這個風險。例如，有關如何使用iOS Keychain 或如何保護Android上的輸出服務的指南。未遵循這些指南的應用程式將遇到這種風險。

2. **違反慣例或常見做法** 不是所有最佳做法都在製造商的指南中被規矩化。在某些情況下，行動應用程式中普遍存在的實務慣例就是這種情況。

3. **非故意誤用** 有些應用程式可能本來是想做對的事情，但實際上在執行時某個部分出現了錯誤。這可能是一個簡單的錯誤，例如在API調用上設置錯誤的標誌，或者可能是對保護工作的運作方式產生誤解。

平台權限模型的錯誤屬於這個類別。例如，如果應用程式請求了太多權限或錯誤的權限，那麼最好將其歸類到這裡。

# 如何防止「不當的使用平台」？

安全的編碼和配置實踐必須在行動應用程式的伺服器端使用。有關特定的漏洞信息，請參考OWASP Web 十大或 Cloud 十大專案。


# 攻擊情境舉例

由於有數個平台，每個平台都有數百或數千個API，本節中的例子僅表淺討論某些可能性。

**使用應用程式本地儲存而非 Keychain** iOS Keychain 是一個安全的儲存設施，用於存儲應用程式和系統數據。在iOS上，應用程式應該使用它來存儲任何具有安全意義的小數據（會話密鑰、密碼、設備註冊數據等）。一個常見的錯誤是將這些項目存儲在應用程式的本地存儲中。在應用程式的本地存儲中存儲的數據可以在未加密的iTunes備份中使用（例如，在用戶的電腦上）。對於某些應用程式來說，這樣的暴露是不合適的。

下面，您可以看到有許多風險和漏洞，您必須加以緩解以滿足M1的標準:


![Cloud Top 10 Risks](https://wiki.owasp.org/images/f/fd/CloudTT_thum.png) <br />
![OWASP Top 10 - 2013](https://wiki.owasp.org/images/7/7e/WebTT_thumb.png)


**最糟糕的行為**
以下是OWASP在行動應用程式中最常見的漏洞類型清單:

- **網路服務不安全**
  - 邏輯瑕疵
    - [Testing for business logic flaws](https://www.owasp.org/index.php/Testing_for_business_logic_(OWASP-BL-001))
    - [Business] Logic Security Cheat Sheet (https://www.owasp.org/index.php/Business_Logic_Security_Cheat_Sheet)
  - 脆弱的認證
    - [OWASP Top Ten Broken Authentication Section](https://www.owasp.org/index.php/Top_10_2013-A2-Broken_Authentication_and_Session_Management)
    - [Authentication Cheat Sheet](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
    - [Developers Guide for Authentication](https://www.owasp.org/index.php/Guide_to_Authentication)
    - [Testing for Authentication](https://www.owasp.org/index.php/Testing_for_authentication)
  - 不牢靠的或毫無會話管理
  - 會話固定
  - 敏感數據使用 GET 方法傳輸
- **不安全的網路伺服器設置**
  - 默認內容
  - 管理介面
- **在 Web 服務和支援行動裝置的網站上的注入（SQL、XSS、命令注入）**
- **身份驗證漏洞**
- **會話管理漏洞**
- **存取控制漏洞**
- **本地和遠端文件被包含其中**

# 參考資料

- OWASP
  - [OWASP Top Ten](https://www.owasp.org/index.php/OWASP_Top_Ten)
- External
  - [External References](http://cwe.mitre.org/)