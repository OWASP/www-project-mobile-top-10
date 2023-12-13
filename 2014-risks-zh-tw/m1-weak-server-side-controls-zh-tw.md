---

layout: col-sidebar
title: "M1: 不良的伺服器端控制"
---

# 威脅主體

**應用層面 特定**

威脅主體包括任何充當對後端 API 服務、網頁服務或傳統網頁伺服器應用程式提供不可信輸入的實體。此類實體的例子包括：使用者、惡意軟體，或是行動裝置上的易受攻擊的應用程式。

# 攻擊媒介	

**利用難度 簡單**

此攻擊媒介與傳統OWASP十大中的攻擊媒介相同。

# 安全層面的強度	

**普及性 常見** <br />
**偵測性 平均**

為了利用這個弱點，組織必須找到一個被行動應用程式使用的網頁服務或 API 呼叫。該服務或 API 呼叫是使用不安全的編碼技術實施的，這導致伺服器內出現 OWASP 十大弱點之一。透過行動界面，攻擊者能夠對弱點端點輸入惡意資料或非預期的事件序列。因此，攻擊者實現了伺服器上原初 OWASP 的十大弱點。

# 技術性影響

**影響程度 嚴重**

這個弱點的技術影響相當於攻擊者透過行動裝置正在利用的相關弱點（在 OWASP 十大中定義）。例如，攻擊者可能透過行動裝置利用跨站腳本（Cross-Site Scripting, XSS）弱點。這對應到 OWASP 十大中的 A3 - XSS 類別，其技術影響為中等。  

# 業務影響
	
**應用程式/業務 特定** 
		
這個弱點的業務影響相當於攻擊者透過行動裝置正在利用的相關弱點（在 OWASP 十大中定義）。例如，攻擊者可能透過行動裝置利用跨站腳本（Cross-Site Scripting, XSS）弱點。這對應到 OWASP 十大中的 A3 - XSS 的業務影響。  

# 我是否容易受到「不良的伺服器端控制」的攻擊?

M1 包含了幾乎所有可能在手機之外對手機應用程式造成不良影響的事情。這正是爭論點... 是否應該完全列在清單中呢？難道我們不是已經有一個針對 Web 應用程式的十大清單嗎？雲端也有一個對應的清單不是嗎？

事實上，是的。如果我們可以確保每個尋求有關行動安全性資訊的人也同時參考那些專案，那就太完美了。然而，通過從全球頂尖的評估團隊進行兩輪的數據收集，我們發現在行動應用程式中，伺服器端問題是如此普遍，以至於我們無法在 Mobile Top Ten 2014 的清單中忽視它們。經驗表明，幾個因素導致了伺服器端弱點的激增。這些因素包括：

- 急於上市;
- 由於新的語言而缺乏安全知識;
- 容易取得且不重視安全性的框架;
- 超出平均的外包開發;
- 行動應用程式的安全預算較低;
- 假設行動作業系統能完全負責安全性的部分; 
- 跨平台開發和編譯的弱點。

# 如何防止「不良的伺服器端控制」？

在行動應用程式的伺服器端必須使用安全編碼和配置實踐。有關具體的弱點資訊，請參閱OWASP Web Top Ten或Cloud Top Ten專案。

# 攻擊情境舉例

下方您可以看到有許多風險和弱點，您必須加以緩解，以滿足 M1：

![Cloud Top 10 Risks](https://wiki.owasp.org/images/f/fd/CloudTT_thum.png) <br />
![OWASP Top 10 - 2013](https://wiki.owasp.org/images/7/7e/WebTT_thumb.png)


**最嚴重的違規行為**

以下是OWASP在行動應用程式中最常見的弱點類型清單：

- **Web服務強化不足**
  - 邏輯缺陷
    - [Testing for business logic flaws](https://www.owasp.org/index.php/Testing_for_business_logic_(OWASP-BL-001))
    - [Business] Logic Security Cheat Sheet](https://www.owasp.org/index.php/Business_Logic_Security_Cheat_Sheet)
  - 脆弱的身分認證
    - [OWASP Top Ten Broken Authentication Section](https://www.owasp.org/index.php/Top_10_2013-A2-Broken_Authentication_and_Session_Management)
    - [Authentication Cheat Sheet](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
    - [Developers Guide for Authentication](https://www.owasp.org/index.php/Guide_to_Authentication)
    - [Testing for Authentication](https://www.owasp.org/index.php/Testing_for_authentication)
  - 脆弱或沒有會話管理
  - 會話固定
  - 使用 GET 方法傳輸敏感資料
- **不安全的網路伺服器配置**
  - 預設內容
  - 管理介面
- **注入（SQL、XSS、命令注入）在網頁服務和支援行動裝置的網站上**
- **身份驗證漏洞**
- **會話管理漏洞**
- **存取控制弱點**
- **包含本地和遠端文件**

# 參考資料

- OWASP
  - [OWASP Top Ten](https://www.owasp.org/index.php/OWASP_Top_Ten)
- External
  - [External References](http://cwe.mitre.org/)