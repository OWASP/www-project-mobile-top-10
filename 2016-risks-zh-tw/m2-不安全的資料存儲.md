---

layout: col-sidebar
title: "M2: 不安全的資料存儲"
---

# 威脅主體

**應用層面 特定**

威脅主體包括以下內容：取得遺失/被盜行動裝置的攻擊者；在行動裝置上執行，代替攻擊者執行的一個惡意軟體或另一個重新封裝的應用程式。

# 攻擊媒介	

**利用難度 簡單**

如果攻擊者實際獲得了行動裝置，該他將行動裝置連接到一台裝有免費軟體的電腦。這些工具允許攻擊者查看所有第三方應用程式目錄，這些目錄通常包含存儲的個人身份識別信息（PII）或其他敏感信息資產。攻擊者可能會建構惡意軟體或修改合法應用程式以竊取這些信息資產。

#  安全層面的強度

**普及性 常見** <br />
**偵測性 平均**

不安全的數據存儲漏洞發生在開發團隊假設用戶或惡意軟體將無法訪問行動裝置文件系統及隨後在裝置上的敏感信息數據存儲時。文件系統是容易訪問的。組織應該預期惡意用戶或惡意軟體可能會檢查敏感數據存儲。應避免使用不安全的加密函式庫。對行動裝置進行Root或越獄會規避任何加密保護。當數據未得到適當保護時，專門的工具就足以查看應用程式數據。

# 技術性影響

**影響程度 嚴重**

這可能導致數據丟失，在最好的情況下是對單個用戶，而在最壞的情況下可能影響多個用戶。這也可能導致以下技術影響：通過行動惡意軟體、修改的應用程式或鑑識工具提取應用程式的敏感信息。業務影響的性質高度依賴於被盜信息的性質。不安全的數據可能導致以下業務影響:

- 身份盜竊;
- 隱私侵犯;
- 詐騙;
- 名譽損害;
- 外部政策違規（PCI）; 
- 物質損失

# 業務影響
	
**應用程式/業務 特定** 
		

不安全的數據存儲漏洞通常會對擁有風險應用程式的組織產生以下業務風險:

- 身份盜竊
- 詐騙
- 聲望損害
- 外部政策違規（PCI）
- 物質損失

# 我是否容易受到「不安全的資料存儲」的攻擊？

這一類別涵蓋了不安全的數據存儲和預期外的數據洩漏。存儲不安全的數據包括但不限於以下內容:

- SQL 資料庫;
- 日誌文件;
- XML 數據存儲或清單文件;
- 二進制數據存儲;
- Cookie 存儲;
- SD 卡;
- 雲端同步。

預期外的數據洩漏包括但不限於以下來自漏洞的情況:

- 作業系統;
- 框架;
- 編譯器環境;
- 新硬體;
- Rooted 或 Jailbroken 的裝置

這明顯是在開發者認知外的情況下發生的。在行動開發中，這主要出現在未記錄或文檔不足的內部流程，例如:

- 作業系統緩存數據、圖像、按鍵、記錄和緩衝區的方式;
- 開發框架緩存數據、圖像、按鍵、記錄和緩衝區的方式;
- 數據廣告、分析、社交或被啟用框架的緩存數據、圖像、按鍵、記錄和緩衝區的方式或數量。

# 如何防止「不安全的資料存儲」？

對您的行動應用程式、作業系統、平台和框架進行威脅建模是很重要的，以了解應用程式處理的信息資產以及API如何處理這些資產。重要的是要查看它們如何處理以下功能:

- URL 緩存（包括請求和響應）;
- 鍵盤按鍵緩存;
- 複製/貼上 緩存;
- 應用程式背景執行;
- 中介數據;
- 日誌記錄;
- HTML5 數據存儲;
- 瀏覽器 cookie 對象;
- 分析數據發送給第三方.

# 攻擊情境舉例

**可視例子**

iGoat是一個特意設計成易受攻擊的行動應用程序，供資安社群親自探索這類漏洞。在下面的例子中，我們輸入憑證並登錄到假銀行應用程式。然後，我們導航到文件系統。在應用程式目錄中，我們可以看到一個名為“credentials.sqlite”的資料庫。探索這個資料庫後，顯示了應用程式以純文本形式存儲我們的用戶名和憑證（Jason:pleasedontstoremebro！）。

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