---

layout: col-sidebar
title: "M3: 不足的傳輸層保護"
---

# 威脅主體

**應用層面 特定**

在設計行動應用程式時，數據通常以客戶端-伺服器方式進行交換。當程式傳輸其數據時，它必須穿越行動裝置的電信網路和網際網路。威脅主體可能會利用弱點截取在傳輸過程中的敏感數據。存在以下威脅主體:

- 位於相同本地網路的攻擊者（被入侵或受監控的Wi-Fi）;
- 電信網路或網路設備（路由器、基站、代理等）; 
- 行動裝置上的惡意軟體.

# 攻擊媒介	

**利用難度 困難**

監視網路以進行不安全通信攻擊的可利用因素是有所差異的。監控電信網絡上的流量比監控本地咖啡店的流量更難。一般來說，有針對性的攻擊更容易執行。	

# 安全層面的強度	

**普及性 常見** <br />
**偵測性 簡單**

行動應用程式經常未對網路流量進行保護。它們可能在身份驗證時使用SSL/TLS，但在其他地方未使用。這種不一致性導致數據和會話ID有被截取的風險。

使用安全傳輸並不意味著應用程式正確執行它。

要檢測基本缺陷，要觀察手機的網路流量。更隱晦的缺陷需要檢查應用程式的設計和配置	

# 技術性影響	

**影響程度 中等**

這種缺陷使個人用戶的數據暴露，可能導致帳戶被盜。如果攻擊者截取了管理員帳戶，整個站點可能會受到威脅。不良的SSL設置還可能促使釣魚和中間人攻擊。因此，保護網路流量的重要性不言而喻，特別是在行動應用程式中，以防止這樣的攻擊和數據泄露。	

# 業務影響
	
**應用程式/業務 特定** 
		

通過通信渠道截取敏感數據最少將導致隱私侵犯。

對用戶保密性的侵犯可能導致:

- 身份盜竊;
- 詐騙;
- 聲譽損害

# 我是否容易受到「不足的傳輸層保護」的攻擊?

要確定應用程式是否具有足夠的傳輸層保護，可以通過代理查看應用程式流量。回答以下問題:

- 所有的連接，不僅僅是您擁有的伺服器的連接，是否都得到了正確的加密？
- SSL認證是否在有效期內？
- SSL認證是否是自簽名的？
- SSL是否使用足夠高的密碼強度？
- 應用程式是否接受被用戶接受的認證作為授權機構？

# 如何防止「不足的傳輸層保護」?

**一般情況的最佳實踐**

- 假設網路層不安全且容易被竊聽。
- 對行動應用程式用於傳輸敏感信息、會話令牌或其他敏感數據到後端API或Web服務的傳輸通道應用SSL/TLS。
- 對於外部實體（如第三方分析公司、社交網路等）而言，在應用程式通過瀏覽器/webkit運行例行程序時使用它們的SSL版本。避免混合SSL會話，因為它們可能會暴露用戶的會話ID。
- 使用強大的、符合行業標準的密碼套件和適當的金鑰長度。
- 使用由受信任的CA提供者簽署的認證。
- 絕不允許自簽名認證，對於有安全意識的應用程式，考慮使用認證固定。
- 總是要求SSL鏈驗證。
- 只有在使用金鑰鏈中受信任的認證驗證了端點伺服器的身份後，才建立安全連接。
- 如果行動應用程式檢測到無效認證，通過UI通知用戶。
- 不要通過替代通道（例如SMS、MMS或通知）傳送敏感數據。
- 如果可以，將任何敏感數據在提供給SSL通道之前應用一個獨立的加密層。如果未來發現SSL實現中的漏洞，加密數據將提供對保密性侵犯的次級防禦。

新的威脅使攻擊者能夠竊聽敏感流量，透過在行動裝置的SSL函式庫加密並將網路流量傳輸到目標伺服器之前，在行動裝置內部截取流量。有關此風險性質的更多信息，請參見M10。

**對於 iOS 的最佳實踐**
 
 在最新版本的iOS中，默認的類別非常好地處理SSL密碼強度協商。問題出現在開發人員臨時添加程式碼以規避這些默認值以應對開發障礙時。除了上述一般實踐之外：

- 確保憑證有效且失敗時關閉。
- 使用CFNetwork時，考慮使用Secure Transport API指定受信任的客戶端認證。幾乎在所有情況下，應使用NSStreamSocketSecurityLevelTLSv1以獲得更高的標準密碼強度。
- 在開發後，確保所有NSURL調用（或NSURL的包裝器）不允許自簽名或無效認證，例如NSURL類別方法setAllowsAnyHTTPSCertificate。
- 考慮使用認證固定，方法是將認證導出，包含在應用程式包中，並將其錨定到信任對象。使用NSURL方法connection:willSendRequestForAuthenticationChallenge:將能接受您的認證。

**針對 Android 的最佳實踐**

- 在開發週期後刪除所有可能使應用程式接受所有認證的程式碼，例如org.apache.http.conn.ssl.AllowAllHostnameVerifier或SSLSocketFactory.ALLOW_ALL_HOSTNAME_VERIFIER。這等效於信任所有認證。
- 如果使用擴展SSLSocketFactory的類別，請確保正確實現了checkServerTrusted方法，以便正確檢查服務器認證。

# 攻擊情境舉例

有一些常見的情景，侵入測試人員在檢查行動應用程式通信安全性時經常發現:

**缺乏認證檢查**

行動應用程式和端點成功連接並執行SSL/TLS握手以建立安全通道。但是，行動應用程式未檢查伺服器提供的認證，並且行動應用程式無條件地接受伺服器提供的任何認證。這破壞了行動應用程式和端點之間的任何相互身份驗證功能。行動應用程式容易受到SSL代理的中間人攻擊。

**握手協商不足**

行動應用程式和端點成功連接並作為連接握手的一部分進行密碼套件協商。客戶端成功地與伺服器協商而後使用一個導致弱加密的弱密碼套件。這將危害行動應用程式和端點之間通道的機密性;

**隱私信息泄漏**

行動應用程式通過非安全通道而不是通過SSL將個人身份信息傳輸到端點。這將危害行動應用程式和端點之間任何與隱私有關的數據的機密性。


# 參考資料

- [Fortify On Demand Blog - Exploring The OWASP Mobile Top 10: Insufficient Transport Layer Protection](http://h30499.www3.hp.com/t5/Fortify-Application-Security/Exploring-The-OWASP-Mobile-Top-10-M3-Insufficient-Transport/ba-p/5966473)
- [OWASP IOS Developer Cheat Sheet](https://www.owasp.org/index.php/IOS_Developer_Cheat_Sheet)
- [blog.securemacprogramming.com - SSL Pinning for Cocoa Touch](http://blog.securemacprogramming.com/2011/12/on-ssl-pinning-for-cocoa-touch/)
- [Why Eve and Mallory Love Android: An Analysis of Android SSL (In)Security](http://www2.dcsec.uni-hannover.de/files/android/p50-fahl.pdf)
- [Fortify VulnCat - A Taxonimy of Software Security Errors](http://www.hpenterprisesecurity.com/vulncat/en/vulncat/index.html)