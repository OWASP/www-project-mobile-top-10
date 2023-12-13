---

layout: col-sidebar
title: "M8: 程式碼竄改"
---

# 威脅主體

**應用層面 特定**

通常，攻擊者會通過在第三方應用商店中惡意的應用程式來利用程式碼修改。攻擊者還可能通過釣魚攻擊欺騙用戶安裝應用程式。

# 攻擊媒介

**利用難度 簡單**

通常，攻擊者將採取以下措施來利用這一類別的漏洞:
-對應用程式包的核心二進制文件進行直接二進制更改
- 對應用程式包內的資源進行直接二進制更改
- 重新定向或替換系統API以攔截並執行惡意的外部程式碼

# 安全層面的強度

**普及性 常見** <br />
**偵測性 平均**

修改過的應用程式形式比你想象的要常見得多。整個安全行業都建立在檢測並刪除應用商店中未經授權的行動應用程式版本。根據檢測程式碼修改的方法，組織可以擁有從有限到極其成功的方式，來檢測未經授權程式碼版本。

這一類別涵蓋了二進制修補、本地資源修改、方法吊取（hooking）、方法交換（swizzling）和動態記憶體修改

一旦應用程式被送到到行動裝置上，程式碼和數據資源就駐留在那裡。攻擊者可以直接修改程式碼，動態更改記憶體內容，更改或替換應用程式使用的系統API，或修改應用程式的數據和資源。這可以為攻擊者提供一種直接的方式，來翻轉本來該軟體作為個人或金錢收益的用途。

# 技術性影響	

**影響程度 嚴重**

程式碼修改可能產生不同性質的廣泛影響，具體取決於修改的性質。典型的影響類型包括:
- 未經授權的新功能;
- 身份盜竊;
- 詐欺。

# 業務影響
	
**應用程式/業務 特定** 
		

程式碼修改通常導致以下業務影響:
- 由於盜版而損失收入;
- 聲望受損。

# 我是否容易受到「程式碼竄改」的攻擊？

從技術上講，所有行動程式碼都容易受到程式碼篡改的威脅。行動程式碼運行在組織無法控制的環境中。同時，有很多改變程式碼運行環境的方式。這些變化允許攻擊者操縱程式碼並隨意修改它。

儘管行動程式碼本質上是容易受到威脅的，但重要的是要自問是否值得檢測並試圖防止未經授權的程式碼修改。某些業務領域（例如遊戲）編寫的應用程式比其他行業（例如酒店業）更容易受到程式碼修改的影響。因此，在決定是否應處理此風險之前，考慮業務影響至關重要。

#  如何防止「程式碼竄改」?

The mobile app must be able to detect at runtime that code has been added or changed from what it knows about its integrity at compile time. The app must be able to react appropriately at runtime to a code integrity violation.
行動應用程式必須在運行時能夠檢測到程式碼是否已經被添加或更改，與編譯時了解到的程式碼完整性不符。該應用程式必須能夠在運行時對程式碼完整性違規做出適當的反應。

對於這類風險的矯正策略在 [OWASP Reverse Engineering and Code Modification Prevention Project](https://www.owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project) 中以更多技術細節進行了概述。

**Android Root檢測**

通常，已經修改的應用程式將在已越獄（Jailbroken）或取得Root權限的環境中執行。因此，嘗試在運行時檢測這些受損環境並相應地做出反應（向伺服器報告或關閉應用程式）是合理的。有一些常見的方法可以檢測Rooted Android裝置：

檢查test-keys

- 檢查 build.prop 文件是否包含 ro.build.tags=test-keys 這一行，這表示是開發者版本或非官方ROM。

檢查OTA認證

- 檢查文件 /etc/security/otacerts.zip 是否存在。

檢查一些已知的Rooted應用程式

- com.noshufou.android.su
- com.thirdparty.superuser
- eu.chainfire.supersu
- com.koushikdutta.superuser

檢查SU二進制文件

- /system/bin/su
- /system/xbin/su
- /sbin/su
- /system/su
- /system/bin/.ext/.su

直接嘗試SU命令

- 嘗試運行su命令，檢查當前用戶的ID，如果返回0，則su命令執行成功。

**iOS 越獄(Jailbreak)偵測**

# 攻擊情境舉例

在應用商店中有許多偽造應用程式，其中一些包含惡意載體。許多修改過的應用程式擁有對原始核心二進制和相關資源的修改形式。攻擊者將這些重新打包成新的應用程式，並將它們釋放到第三方商店中。

**情境1:**

遊戲是使用這種方法進行攻擊的一個特別受歡迎的目標。攻擊者會吸引那些不願意支付遊戲的人。在程式碼中，攻擊者通過規避檢測應用程式內購是否成功的條件跳轉，使受害者可以在不支付的情況下獲得遊戲物品或新的能力。攻擊者還插入了間諜軟件，用於竊取用戶的身份信息。

**情境2:**

銀行應用程式是另一個受攻擊的熱門目標。這些應用程式通常處理對攻擊者有用的敏感信息。攻擊者可以創建該應用程式的偽造版本，將使用者的個人身份信息（PII）以及用戶名/密碼傳送到第三方網站。這類似於桌面版Zeus惡意軟體的行為。這通常導致對銀行的詐騙。

# 參考資料

- OWASP
  - [OWASP Reverse Engineering and Code Modification Prevention Project](https://www.owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project)
- External
- OWASP
  - [OWASP Reverse Engineering and Code Modification Prevention Project](https://www.owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project)
- External

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