---

layout: col-sidebar
title: "M10: Lack of Binary Protections"
---

# Threat Agents

**Application Specific**

Typically, an adversary will analyze and reverse engineer a mobile app's code, then modify it to perform some hidden functionality.	

# Attack Vectors	

**Exploitability MEDIUM**

An adversary will use an automated tool to reverse engineer the code and modify it using malware to perform some hidden functionality.	

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability EASY**

**Prevalence**
A lack of binary protections within a mobile app exposes the application and it’s owner to a large variety of technical and business risks if the underlying application is insecure or exposes sensitive intellectual property. A lack of binary protections results in a mobile app that can be analyzed, reverse-engineered, and modified by an adversary in rapid fashion. However, an application with binary protection can still be reversed by a dedicated adversary and therefore binary protection is not a perfect security solution. At the end of the day, binary protection only slows down a security review.

It is extremely common for apps to be deployed without binary protection. The prevalence has been extensively studied by a large number of security vendors, analysts, and researchers [1] [2] [3] [17].

**Detectability**

It is difficult to detect that an adversary has reverse engineered an app’s code. Typically, the app owner will realize reverse engineering was successful when the code shows up in another app in iTunes [4], Google Play [5] [16], or a third-party app store [6]. Usually, the owner discovers this by accident and not through active policing by an app store.

There are many different viable solutions to detect code modification at runtime and respond accordingly. At runtime, mobile apps should be enabled to detect if a runtime modification / injection has occurred and react in a number of different ways. Pre-determined reactions of the apps will vary from either attempting to thwart the attack or fail in a subtle way [7].

# Technical Impacts	

**Impact SEVERE**

The majority of mobile apps do not prevent an adversary from successfully analyzing, reverse engineering or modifying the app’s binary code [1]. Organizations should apply binary protections to a mobile app under a few different circumstances:

**Analysis and Reverse Engineering**

Binary protections slow down an adversary from analyzing exposed interfaces and reverse engineering code within the mobile app. All too often, the adversary will steal code and recycle it within another app for resell [16]. The app owner is often unaware that the app has been repurposed and sold elsewhere unless they utilize some form of appstore monitoring service or similar. If there is a likely chance that this may occur, the owner should consider binary protections to the app. But be warned, this protection only slows an attacker from reverse engineering. It does not prevent an attacker from doing so.

**Unauthorized Code Modification**

Binary protections slow an adversary from modifying the underlying code or behavior to disable or add additional functionality on behalf of the adversary. This is likely to occur if the application stores, transmits, or processes personally identifiable information (PII) or other sensitive information assets like passwords or credit cards. Code modification often takes the form of repackaging or insertion of malware into existing mobile apps [3] [18].


# Business Impacts
	
**Application / Business Specific** 
		

Typically, a lack of binary protection will result in the following business impacts:
- Privacy Related and Confidential Data Theft;
- Unauthorized Access and Fraud;
- Brand and Trust Damage;
- Revenue Loss and Piracy;
- Intellectual Property Theft;
- User Experience Compromise.
Many different analysts have provided policy guidance around minimizing this risk [8] [9] [10] [11] [12].

# Am I Vulnerable To 'Lack of Binary Protections'?

If you are hosting code in an untrustworthy environment, you are susceptible to this risk [1] [2] [3] [17]. An untrustworthy environment is defined as an environment in which the organization does not have physical control. This includes mobile clients, firmware in appliances, cloud spaces, or datacenters within particular countries.

If you answer yes to any of these questions, you are vulnerable to a binary attack:

- Can someone code-decrypt this app (iPhone specific) using an automated tool like ClutchMod or manually using GDB?
- Can someone reverse engineer this app (Android specific) using an automated tool like dex2jar?
- Can someone use an automated tool like Hopper or IDA Pro to easily visualize the control-flow and pseudo-code of this app?
- Can someone modify the app’s presentation layer (HTML/JS/CSS) of this app within the phone and execute modified JavaScript?
- Can someone modify the app’s binary executable using a hex editor to get it to bypass a security control?

# How Do I Prevent 'Lack of Binary Protections'?

First, the application must follow secure coding techniques for the following security components within the mobile app:

- Jailbreak Detection Controls;
- Checksum Controls;
- Certificate Pinning Controls;
- Debugger Detection Controls.

Next, the app must adequately mitigate two different technical risks that the above controls are exposed to:

1. The organization building the app must adequately prevent an adversary from analyzing and reverse engineering the app using static or dynamic analysis techniques;
2. The mobile app must be able to detect at runtime that code has been added or changed from what it knows about its integrity at compile time. The app must be able to react appropriately at runtime to a code integrity violation.

The remediation strategies for these types of risks are outlined in more technical detail within the OWASP Reverse Engineering and Code Modification Prevention Project.

**Android Specific Best Practices:**

**Android Root Detection**

There are a few common ways to detect a rooted Android device:
Check for test-keys

- Check to see if build.prop includes the line ro.build.tags=test-keys indicating a developer build or unofficial ROM

Check for OTA certificates

- Check to see if the file /etc/security/otacerts.zip exists

Check for several known rooted apk's

- com.noshufou.android.su
- com.thirdparty.superuser
- eu.chainfire.supersu
- com.koushikdutta.superuser

Check for SU binaries

- /system/bin/su
- /system/xbin/su
- /sbin/su
- /system/su
- /system/bin/.ext/.su

Attempt SU command directly

- Attempt the to run the command su and check the id of the current user, if it returns 0 then the su command has been successful

# Example Attack Scenarios

This section outlines typical app vulnerabilities that result from a lack of binary protection. Items within parenthesis indicate examples of tools you can use to test for these vulnerabilities.

**iOS Apps**
- Disabling Code Encryption (ClutchMod);
- Jailbreak Detection Evasion (xcon);
- Class Dumping (class-dump-z);
- Method Swizzling (Mobile Substrate);
- Runtime Code Injection (cycript);
- Runtime Monitoring (Snoop-It);
- Runtime Analysis (GDB); and
- Reverse Engineering ([IDA Pro](https://www.hex-rays.com/products/ida/); Hopper).

**Android Apps**

- Bytecode Conversion (apktool; dex2jar);
- Runtime Analysis (ADB);
- Reverse Engineering ([IDA Pro](https://www.hex-rays.com/products/ida/); Hopper);
- Disassembly (baksmali) and
- Code Injection (Mobile Substrate).

**Windows Phone Apps**

- .NET Decompiler ([JetBrains dotPeak](https://www.jetbrains.com/decompiler/); [ILSpy](http://ilspy.net/); [RedGate .NET Reflector](http://www.red-gate.com/products/dotnet-development/reflector/) );
- Runtime Analysis ([Tangerine](https://github.com/andreycha/tangerine); [XAPSpy](https://github.com/sensepost/xapspy));
- Reverse Engineering ([IDA Pro](https://www.hex-rays.com/products/ida/));
- Disassembly ([MSIL Disassembler (Ildasm.exe)](https://msdn.microsoft.com/en-us/library/f7dy01k1%28v=vs.110%29.aspx)) and

There are many well-established security experts within the mobile space that have written books on the topic of binary protection testing [13] [14] [15].

# References

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