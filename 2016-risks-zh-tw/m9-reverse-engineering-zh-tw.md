---

layout: col-sidebar
title: "M9: 逆向工程"
---

# 威脅主體

**應用層面 特定**

攻擊者通常會從應用程式商店下載目標應用程式，並使用一套不同的工具在自己的本地環境中進行分析。  

# 攻擊媒介

**利用難度 簡單**

攻擊者必須對最終的核心二進制進行分析，以確定其中包含的原始字符串表、原始碼、函式庫、演算法以及應用程式內嵌的資源。攻擊者將使用相對價格較為合理且廣為人知的工具，如IDA Pro、Hopper、otool、strings，以及攻擊者環境中的其他二進制檢測工具。 

# 安全層面的強度	

**普及性 常見** <br />
**偵測性 簡單**

一般來說，所有的行動應用程式程式碼都容易受到逆向工程的影響，但有些應用程式比其他更容易受到攻擊。使用允許在運行時進行動態內省的語言/框架（如Java、.NET、Objective C、Swift）編寫的程式碼特別容易受到逆向工程的風險。檢測對逆向工程的敏感性相對較簡單。首先，解密應用商店版本的應用程式（如果應用了二進制加密）。然後，對二進制程式碼使用本文「攻擊媒介」部分概述的工具。如果能夠相對輕鬆地理解應用程式的控制流程、字符串表以及這些工具生成的任何偽程式碼/原始碼，那麼程式碼就容易受到攻擊。

# 技術性影響

**影響程度 中等**

攻擊者可能利用逆向工程實現以下任一目標:
- 揭示有關後端伺服器的信息;
- 揭示加密常數和密碼;
- 偷竊知識產權;
- 對後端系統進行攻擊; 
- 獲取執行後續程式碼修改所需的情報

# 業務影響
	
**應用程式/業務 特定** 
		
逆向工程可能對業務產生各種不同的影響，包括:
- 智慧財產權被盜竊;
- 聲譽損害;
- 身份盜竊;
- 後端系統被駭。

# 我是否容易受到「逆向工程」的攻擊？

一般而言，由於程式碼的固有特性，大多數應用程式都容易受到逆向工程的影響。當今大多數用於編寫應用程式的語言都包含豐富的詮釋資料，這在除錯應用程式時對程式設計師非常有幫助。這種相同的能力也極大地幫助了攻擊者理解應用程式的運作方式。

如果攻擊者可以執行以下任一操作，則認為應用程式容易受到逆向工程的影響:

- 清晰理解二進制字符串表的內容
- 準確執行跨功能分析
- 從二進制程式碼中推導出相當精確的原始碼重建
儘管大多數應用程式容易受到逆向工程的影響，但在考慮是否要降低這種風險時，重要的是要檢視逆向工程可能對業務造成的潛在影響。請見下方關於逆向工程的舉例。

# 如何防止「逆向工程」?

為了防止有效的逆向工程，必須使用混淆工具。市場上有許多免費和商業級的混淆器。相反，市場上也有許多不同的去混淆工具。為了測試所選擇的任何混淆工具的效果，可以使用IDA Pro和Hopper等工具進行去混淆程式碼。

一個良好的混淆器應該具有以下能力:

- 縮小需要混淆的方法/程式碼範圍;
- 調整混淆程度以平衡性能影響;
- 抵禦來自IDA Pro和Hopper等工具的去混淆;
- 對字符串表和方法進行混淆

# 攻擊情境舉例

**情境1**: 字符串表分析:

攻擊者對未加密的應用程式運行 'strings'。由於字符串表分析，攻擊者發現一個硬編碼的連接字符串，其中包含對後端數據庫的身份驗證憑證。攻擊者使用這些憑證來訪問資料庫，並竊取了大量有關應用程式用戶的個人身份信息（PII）數據。

**情境2**: 跨功能分析:

攻擊者使用IDA Pro對未加密的應用程式進行分析。由於字符串表分析結合功能交叉引用，攻擊者發現越獄檢測程式碼。攻擊者在後續的程式碼修改攻擊中利用這一知識來禁用行動應用程式中的越獄檢測。攻擊者隨後部署了一個利用方法替換（method swizzling）來竊取客戶信息的應用程式版本。

**情境3**: 原始碼分析:

考慮一個銀行Android應用程式。APK文件可以使用7zip/Winrar/WinZip/Gunzip等工具輕鬆提取。一旦提取，攻擊者就獲得了清單文件、資產、資源，最重要的是 classes.dex 文件。

然後，使用 Dex to Jar 轉換器，攻擊者可以輕鬆將其轉換為 jar 文件。在下一步中，Java反編譯器（如JDgui）將為您提供程式碼。

# 參考資料

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