---

layout: col-sidebar
title: "M2: 不安全的資料存儲"
---

# 威脅主體

**應用層面 特定**

威脅主體包括以下情況：取得了遺失/被盜的行動裝置的攻擊者；惡意軟體或其他經重新打包的應用程式，代替攻擊者在行動裝置上執行。

# 攻擊媒介	

**利用難度 簡單**

在攻擊者實際取得行動裝置的情況下，他們會將行動裝置連接到一台裝有免費軟體的電腦。這些工具允許攻擊者查看所有第三方應用程式目錄，通常包含存儲的個人身份信息（PII）或其他敏感信息資產。攻擊者可能會構建惡意軟體或修改合法應用程式，以竊取這些信息資產。

# 安全層面的強度	

**普及性 常見** <br />
**偵測性 簡單**

不安全的數據存儲漏洞發生在開發團隊假設使用者或惡意軟體無法訪問行動裝置文件系統及後續在裝置上的敏感信息數據存儲時。文件系統很容易被訪問。組織應該預期惡意用戶或惡意軟體會檢查敏感數據存儲。對行動裝置進行Rooting或jailbreaking可規避任何加密保護。當數據未得到適當保護時，只需要專門的工具即可查看應用程式數據。

# 技術性影響		

**影響程度 嚴重**

不安全的數據存儲，在最好的情況下是單一使用者數據損失，最壞的情況下可能是多個使用者。常見有價值的數據包括:
- 使用者名稱
- 身份驗證令牌
- 密碼
- Cookies
- 位置數據
- UDID/EMEI、設備名稱、網路連線名稱
- 個人信息：出生日期、地址、社交信息、信用卡數據
- 應用程式數據:
  - 儲存的應用程式日誌，例如對於Android應用程式的ADB logcat
  - 除錯信息
  - 緩存的應用程式訊息
  - 交易歷史

# 業務影響
	
**應用程式/業務 特定** 
		
不安全的數據存儲漏洞通常會使有風險應用程式的組織面臨以下業務風險:
- 身份盜竊
- 詐騙
- 名譽損害
- 外部政策違規（PCI）
- 或素材損失。

# 我是否容易受到「不安全的資料存儲」的攻擊?

對您的行動應用程式進行威脅建模是重要的，以了解它處理的信息資產以及底層 API 如何處理這些資產。這些 API 應該安全地存儲敏感信息。OWASP 最常見到數據存儲不安全的地方包括:

- SQL 資料庫;
- 日誌文件;
- Plist 文件;
- XML 數據存儲或清單文件;
- 二進制數據存儲;
- Cookie 存儲;
- SD 卡;
- 雲端同步.

在對敏感信息資產應用加密和解密時，惡意軟體可能對應用程式進行二進制攻擊，以竊取加密或解密金鑰。一旦竊取了這些金鑰，它將解密本地數據並竊取敏感信息。有關這個主題的更多信息，請參見OWASP Mobile Top Ten 2014 M10類別。


# 如何防止「不安全的資料存儲」?

行動應用程式的基本原則是除非絕對必要，否則不要儲存數據。作為開發者，您必須假設數據一旦觸及手機就被放棄。您還必須考慮因默默越獄或Root而損失行動用戶數據的連帶影響。如果在可用性與安全性之間的權衡對您而言過於困難，OWASP建議仔細檢查平台的數據安全性API，確保您正確地呼叫它們。這裡的告誡是了解哪些數據正在被儲存並適當地保護它。


**針對 iOS 最佳實踐:**

- 永遠不要將憑證儲存在手機文件系統上。強制用戶在每次打開應用程式時使用標準的 Web 或 API 登錄方案（通過 HTTPS）進行身份驗證，並確保會話超時設置至少滿足用戶體驗要求。
- 然而，對於特別敏感的應用程式，考慮使用白盒加密方案，以避免在常見加密函式庫中發現的二進制簽名的洩漏。
- 如果數據量較小，建議使用 Apple Keychain API，但一旦手機越獄或被利用，Keychain可以輕松被讀取。此外還存在設備PIN碼被暴力破解的威脅，如上所述，在某些情況下很容易達成。
- 對於資料庫，考慮使用 SQLcipher 進行 Sqlite 數據加密。
- 對於存儲在 Keychain 中的項目，利用最安全的 API 指定，即 kSecAttrAccessibleWhenUnlocked（現在是 iOS 5 中的默認值），對於企業管理的行動裝置，確保其強制使用強度高的PIN碼，包含字母，長度超過4個字符。
- 對於更大或更一般類型的消費者級數據，可以安全使用蘋果的文件保護機制（參見 NSData 型別參照以獲取保護選項）。
- 避免使用 NSUserDefaults 儲存敏感信息，因為它將資料存儲在 plist 文件中。
- 請注意，使用 NSManagedObjects 儲存的所有數據/實體將儲存在未加密的資料庫文件中。
- 在存儲敏感信息資產時，避免僅僅依賴硬編碼的加密或解密金鑰。
- 考慮在作業系統所提供的任何默認加密機制之外提供額外的加密層。

**針對 Android 的最佳實踐:**

- 對於本地存儲，可以使用企業 Android 裝置管理 API 來使用“setStorageEncryption”強制對本地文件存儲進行加密。
- 對於 SD 卡存儲，可以通過 'javax.crypto' 函式庫實現一些安全性，您有幾個選擇，但其中一個簡單的選擇就是使用主密碼和 AES 128 對任何純文本數據進行加密。
- 確保任何共享偏好屬性都不是 MODE_WORLD_READABLE，除非明確需要在應用程式之間共享信息。
- 在儲存敏感信息資產時，避免僅僅依賴硬編碼的加密或解密金鑰。
- 考慮在作業系統所提供的任何默認加密機制之外提供額外的加密層。


# 攻擊情境舉例

**可視的例子**

iGoat是一個特意製作成易受攻擊的行動應用程式，供安全社群第一手探索這些類型弱點。在下面的練習中，我們輸入我們的憑證並登入這個虛構的銀行應用程式。然後，我們導航到文件系統。在應用程式目錄中，我們可以看到一個名為“credentials.sqlite”的資料庫。探索這個資料庫顯示應用程式明文儲存我們的用戶名和憑證（Jason:pleasedontstoremebro!）。

![Local Data Storage](https://wiki.owasp.org/images/6/6d/Screen_Shot_2012-12-19_at_6.34.23_AM.png)
![Goat Hills Financial](https://wiki.owasp.org/images/9/98/Screen_Shot_2012-12-19_at_6.44.51_AM.png)
![Terminal](https://wiki.owasp.org/images/5/5a/Screen_Shot_2012-12-19_at_10.11.15_AM.png)

# 參考資料

- OWASP
  - [OWASP iOS Developer Cheat Sheet](https://www.owasp.org/index.php/IOS_Developer_Cheat_Sheet)
- External
  - [Google Androids Developer Security Topics 1](http://source.android.com/tech/security/)
  - [Google Androids Developer Security Topics 2](http://developer.android.com/training/articles/security-tips.html)
  - [Apple's Introduction to Secure Coding](https://developer.apple.com/library/mac/)
  - [Fortify On Demand Blog - Exploring The OWASP Mobile Top 10: Insecure Data Storage](http://h30499.www3.hp.com/t5/Application-Security-Fortify-on/Exploring-The-OWASP-Mobile-Top-10-M1-Insecure-Data-Storage/ba-p/5904609)