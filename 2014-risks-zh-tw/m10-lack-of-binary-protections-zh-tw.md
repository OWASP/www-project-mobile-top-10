---

layout: col-sidebar
title: "M10: 缺少二進制保護"
---

# 威脅主體

**應用層面 特定**

通常，攻擊者會分析和逆向工程行動應用程式的程式碼，然後修改它以執行一些隱藏的功能。

# 攻擊媒介	

**利用難度 中等**

攻擊者將使用自動化工具對程式碼進行逆向工程，並使用惡意軟體對其進行修改以執行某些隱藏功能。	

# 安全層面的強度	

**普及性 常見** <br />
**偵測性 簡單**

**普及性**
如果底層應用程式不安全或會暴露敏感智慧財產權，則行動應用程式中缺乏二進制保護會使該應用程式及其所有者面臨各種技術和業務風險。缺乏二進制保護會導致行動應用程式可以被攻擊者快速分析、逆向工程和修改。然而，具有二進制保護的應用程式仍然可以被專門的攻擊者逆轉，因此二進制保護並不是完美的安全解決方案。歸根究底，二進位保護只會減慢安全審查速度。

在沒有二進制保護的情況下部署應用程式是非常常見的。許多安全供應商、分析師和研究人員已對普及性進行了廣泛研究 [1] [2] [3] [17].

**偵測性**

很難偵測到攻擊者對應用程式的程式碼進行了逆向工程。通常，當程式碼出現在 iTunes [4]、Google Play [5] [16] 或第三方應用程式商店 [6] 中的另一個應用程式時，應用程式擁有者會意識到成功的逆向工程。通常，所有者是偶然發現這一點的，而不是透過應用程式商店的積極監管。

有許多不同的可行解決方案可以在運行時檢測程式碼修改並做出相應的回應。在運行時，應啟用行動應用程式來檢測是否發生運行時修改/注入，並以多種不同的方式做出反應。應用程式的預定反應會有所不同，不是會嘗試阻止攻擊，就是會以隱晦的方式失敗 [7]。

# 技術性影響	

**影響程度 嚴重**

大多數行動應用程式不會阻止攻擊者成功分析、逆向工程或修改應用程式的二進制程式碼 [1]。組織應該在幾種不同的情況下對行動應用程式應用二進制保護：

**分析與逆向工程**

Binary protections slow down an adversary from analyzing exposed interfaces and reverse engineering code within the mobile app. All too often, the adversary will steal code and recycle it within another app for resell [16]. The app owner is often unaware that the app has been repurposed and sold elsewhere unless they utilize some form of appstore monitoring service or similar. If there is a likely chance that this may occur, the owner should consider binary protections to the app. But be warned, this protection only slows an attacker from reverse engineering. It does not prevent an attacker from doing so.二進制保護會減慢攻擊者分析行動應用程式中暴露的介面和逆向工程程式碼的速度。攻擊者常常會竊取程式碼並在另一個應用程式中回收它以進行轉售 [16]。應用程式所有者通常不知道該應用程式已被改變用途並在其他地方出售，除非他們使用某種形式的應用程式商店監控服務或類似服務。如果有可能發生這種情況，所有者應考慮對應用程式進行二進制保護。但請注意，這種保護只會減緩攻擊者進行逆向工程的速度。 它並不能阻止攻擊者這樣做。

**未經授權的程式碼修改**

二進制保護會減緩攻擊者修改底層程式碼，或一些替攻擊者停用或添加附加功能的速度的行為。如果應用程式儲存、傳輸或處理個人識別資訊 (PII) 或其他敏感資訊資產（例如密碼或信用卡），則可能會發生這種情況。程式碼修改通常採取重新打包或將惡意軟體插入現有行動應用程式的形式[3] [18]。

# 業務影響
	
**應用程式/業務 特定** 
		

通常，缺乏二進制保護會導致以下業務影響:
- 隱私相關和機密資料竊取;
- 未經授權的存取和詐欺;
- 品牌和信任受損;
- 收入損失和盜版;
- 智慧財產權盜竊;
- 使用者體驗損害.
許多不同的分析師提供了有關最大限度降低這種風險的政策指引[8] [9] [10] [11] [12]。

# 我是否容易受到「缺少二進制保護」的攻擊？

如果您在不可信的環境中託管程式碼，則很容易受到此風險的影響 [1] [2] [3] [17]。不可信環境被定義為組織沒有實體控制的環境。這包括行動用戶端、裝置中的韌體、雲端空間或特定國家/地區的資料中心。

如果您對以下任何一個問題的答案是“是”，則您很容易受到二進制攻擊：

- 有人可以使用 ClutchMod 等自動化工具或手動使用 GDB 對這個應用程式（特定於 iPhone）進行程式碼解密嗎？
- 有人可以使用 dex2jar 這樣的自動化工具對這個應用程式（特定於 Android）進行逆向工程嗎？
- 有人可以使用 Hopper 或 IDA Pro 等自動化工具來輕鬆視覺化此應用程式的控制流程和偽程式碼嗎？
- 有人可以在手機內修改此應用程式的應用程式表示層 (HTML/JS/CSS) 並執行修改後的 JavaScript 嗎？
- 有人可以使用十六進制編輯器修改應用程式的二進制可執行檔以使其規避安全控制嗎？

# 如何防止「缺少二進制保護」？

首先，應用程式必須遵循行動應用程式中以下安全元件的安全編碼技術：

- 越獄檢測控制;
- 校驗控制(Checksum Controls);
- 證書固定控制(Certificate Pinning Controls);
- 除錯檢測控制

接下來，應用程式必須充分緩解上述控制項面臨的兩種不同的技術風險:

1. 建立應用程式的組織必須充分防止攻擊者使用靜態或動態分析技術對應用程式進行分析和逆向工程;
2. 行動應用程式必須能夠在執行時間根據其在編譯時了解的完整性來檢測程式碼是否已新增或變更。應用程式必須能夠在運行時對程式碼完整性違規做出適當的反應。

OWASP 逆向工程和程式碼修改預防專案中更詳細地概述了針對這些類型風險的補救策略。

**針對 Android 的最佳實踐:**

**Android Root 偵測**

有幾種常見方法可以偵測已取得 root 權限的 Android 裝置:

檢查測試金鑰

- 檢查 build.prop 是否包含 ro.build.tags=test-keys 行，意味開發人員版本或非官方 ROM

檢查 OTA 認證

- 檢查檔案 /etc/security/otacerts.zip 是否存在

檢查幾個已知的 root apk

- com.noshufou.android.su
- com.thirdparty.superuser
- eu.chainfire.supersu
- com.koushikdutta.superuser

檢查 SU 二進制文件

- /system/bin/su
- /system/xbin/su
- /sbin/su
- /system/su
- /system/bin/.ext/.su

直接嘗試 SU 命令

- 嘗試執行su指令並檢查目前使用者的id，如果回傳0則su指令成功

# 攻擊情境舉例

本節概述了由於缺乏二進制保護而導致的典型應用程式漏洞。括號內的項目表示可用於測試這些漏洞的工具範例。

**iOS 應用程式**
- 禁用程式碼加密 (ClutchMod);
- 越獄檢測規避 (xcon);
- 類別擷取 (class-dump-z);
- 方法交換 (Mobile Substrate);
- 運行時代碼注入 (cycript);
- 運行時監控 (Snoop-It);
- 運行時分析 (GDB);
- 逆向工程 ([IDA Pro](https://www.hex-rays.com/products/ida/); Hopper).

**Android 應用程式**

- 字節碼轉換 (apktool; dex2jar);
- 運行時分析 (ADB);
- 逆向工程 ([IDA Pro](https://www.hex-rays.com/products/ida/); Hopper);
- 反編譯 (baksmali) 和
- 程式碼注入 (Mobile Substrate).

**Windows Phone 應用程式**

- .NET反編譯器 ([JetBrains dotPeak](https://www.jetbrains.com/decompiler/); [ILSpy](http://ilspy.net/); [RedGate .NET Reflector](http://www.red-gate.com/products/dotnet-development/reflector/) );
- 運行時分析 ([Tangerine](https://github.com/andreycha/tangerine); [XAPSpy](https://github.com/sensepost/xapspy));
- 逆向工程 ([IDA Pro](https://www.hex-rays.com/products/ida/));
- 反編譯 ([MSIL Disassembler (Ildasm.exe)](https://msdn.microsoft.com/en-us/library/f7dy01k1%28v=vs.110%29.aspx)) 和

行動領域有許多知名的安全專家撰寫了有關二進制保護測試主題的書籍 [13] [14] [15]。

# 參考資料

- [1] Arxan Research: [State of Security in the App Economy, Volume 2](https://www.arxan.com/assets/1/7/State_of_Security_in_the_App_Economy_Report_Vol._2.pdf), November 2013:

> “Adversaries have hacked 78 percent of the top 100 paid Android and iOS apps in 2013.”

  - [2] HP Research: [HP Research Reveals Nine out of 10 Mobile Applications Vulnerable to Attack](http://www8.hp.com/us/en/hp-news/press-release.html?id=1528865#.UuwZFPZvDi5), 18 November 2013:

> "86 percent of applications tested lacked binary hardening, leaving applications vulnerable to information disclosure, buffer overflows and poor performance. To ensure security throughout the life cycle of the application, it is essential to build in the best security practices from conception."

  - [3] North Carolina State University: [Dissecting Android Malware: Characterization and Evolution](http://www.csc.ncsu.edu/faculty/jiang/pubs/OAKLAND12.pdf), 7 September 2011:

> “Our results show that 86.0% of them (Android Malware) repackage legitimate apps to include malicious payloads; 36.7% contain platform-level exploits to escalate privilege; 93.0% exhibit the bot-like capability.”

  - [4] Tech Hive: [Apple Pulls Ripoff Apps from its Walled Garden](http://www.techhive.com/article/249310/apple_pulls_ripoff_apps_from_its_walled_garden.html) Feb 4th, 2012:

> “While Apple is known for screening apps before they are allowed to sprout up in its walled garden, clearly fake apps do get in. Once they do, getting them out depends on developers who raise a fuss.”

  - [5] Tech Crunch: [Developer Spams Google Play With RipOffs of Well-Known Apps… Again](http://techcrunch.com/2014/01/02/developer-spams-google-play-with-ripoffs-of-well-known-apps-again/), January 2 2014:

> “It’s not uncommon to search the Google Play app store and find a number of knock-off or “fake” apps aiming to trick unsuspecting searchers into downloading them over the real thing.”

  - [6] Extreme Tech: [Chinese App Store Offers Pirated iOS Apps Without the Need To Jailbreak](http://www.extremetech.com/mobile/153849-chinese-app-store-offers-pirated-ios-apps-without-the-need-to-jailbreak), April 19 2013:

> “The site offers apps for free that would otherwise cost money, including big-name titles.”

  - [7] OWASP: [Architectural Principles That Prevent Code Modification or Reverse Engineering](https://www.owasp.org/index.php/Architectural_Principles_That_Prevent_Code_Modification_or_Reverse_Engineering), January 11th 2014.

  - [8] Gartner report: Avoiding Mobile App Development Security Pitfalls, 24 May 2013:

> "For critical applications, such as transactional ones and sensitive enterprise applications, hardening should be used."

  - [9] Gartner report: Emerging Technology Analysis: Mobile Application Shielding, March 26th, 2013:

> "As more regulated and sensitive data applications move to mobile platforms the need to increase data protection increases. Mobile application shielding presents the opportunity to security providers to offer higher data protection standards to mobile platforms that exceed mobile OS security."

  - [10] Gartner report: Proliferating Mobile Transaction Attack Vectors and What to Do About Them, March 1st, 2013:

> "Use mobile application security testing services and self-defending application utilities to help prevent hacking attempts."

  - [11] Gartner report: Select a Secure Mobile Wallet for Proximity, March 1st, 2013:

> "Application hardening can fortify sensitive business code against hacking attempts, such as reverse engineering”

  - [12] Forrester paper: Choose The Right Mobile Development Solutions For Your Organization, May 6th 2013:

> “5 Key Protections: Data Protection, App Compliance, App-Level Threat Defense, Security Policy Enforcement, App Integrity”

  - [13] John Wiley and Sons, Inc: [iOS Hacker's Handbook](http://www.amazon.com/iOS-Hackers-Handbook-Charlie-Miller/dp/1118204123), Published May 2012, [ISBN 1118204123](https://wiki.owasp.org/index.php/Special:BookSources/1118204123).

  - [14] McGraw Hill Education: [Mobile Hacking Exposed](http://mobilehackingexposed.com/), Published July 2013, [ISBN 0071817018](https://wiki.owasp.org/index.php/Special:BookSources/0071817018).

  - [15] Publisher Unannounced: [Android Hacker's Handbook](http://www.amazon.com/Android-Hackers-Handbook-Joshua-Drake/dp/111860864X), To Be Published April 2014.

  - [16] Software Development Times: [More than 5,000 apps in the Google Play Store are copied APKs, or 'thief-ware'](http://sdt.bz/66393#ixzz2sHa7dFMp), November 20 2013:

> “In most cases, the 2,140 copycat developers that were found reassembled the apps almost identically, adding new advertising SDKs to siphon profits away from the original developers.

  - [17] InfoSecurity Magazine: [Two Thirds of Personal Banking Apps Found Full of Vulnerabilities](http://www.infosecurity-magazine.com/view/36376/two-thirds-of-personal-banking-apps-found-full-of-vulnerabilities/), January 3 2014:

> “But one of his more worrying findings came from disassembling the apps themselves ... what he found was hardcoded development credentials within the code. An attacker could gain access to the development infrastructure of the bank and infest the application with malware causing a massive infection for all of the application’s users.”

  - [18] InfoSecurity Magazine: [Mobile Malware Infects Millions; LTE Spurs Growth](http://www.infosecurity-magazine.com/view/36686/mobile-malware-infects-millions-lte-spurs-growth/), January 29 2014:

> "Number of mobile malware samples is growing at a rapid clip, increasing by 20-fold in 2013... It is trivial for an attacker to hijack a legitimate Android application, inject malware into it and redistribute it for consumption. There are now binder kits available that will allow an attacker to automatically inject malware into an existing application"