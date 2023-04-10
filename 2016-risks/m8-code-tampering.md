---

layout: col-sidebar
title: "M8: Code Tampering"
---

# Threat Agents

**Application Specific**

Typically, an attacker will exploit code modification via malicious forms of the apps hosted in third-party app stores. The attacker may also trick the user into installing the app via phishing attacks.  

# Attack Vectors	

**Exploitability EASY**

Typically, an attacker will do the following things to exploit this category:
- Make direct binary changes to the application package's core binary
- Make direct binary changes to the resources within the application's package
- Redirect or replace system APIs to intercept and execute foreign code that is malicious

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability AVERAGE**

Modified forms of applications are surprisingly more common than you think. There is an entire security industry built around detecting and removing unauthorized versions of mobile apps within app stores. Depending upon the approach taken to solving the problem of detecting code modification, organizations can have limited to highly successful ways of detecting unauthorized versions of code in the wild.
This category covers binary patching, local resource modification, method hooking, method swizzling, and dynamic memory modification.

Once the application is delivered to the mobile device, the code and data resources are resident there. An attacker can either directly modify the code, change the contents of memory dynamically, change or replace the system APIs that the application uses, or modify the application's data and resources. This can provide the attacker a direct method of subverting the intended use of the software for personal or monetary gain.

# Technical Impacts	

**Impact SEVERE**

The impact from code modification can be wide ranging in nature, depending upon the nature of the modification itself. Typical types of impacts include the following:
- Unauthorized new features;
- Identity theft; or
- Fraud.

# Business Impacts
	
**Application / Business Specific** 
		

The business impact from code modification typically results in the following:
- Revenue loss due to piracy; or
- Reputational damage.

# Am I Vulnerable To 'Code Tampering'?

Technically, all mobile code is vulnerable to code tampering. Mobile code runs within an environment that is not under the control of the organization producing the code. At the same time, there are plenty of different ways of altering the environment in which that code runs. These changes allow an adversary to tinker with the code and modify it at will.

Although mobile code is inherently vulnerable, it is important to ask yourself if it is worth detecting and trying to prevent unauthorized code modification. Apps written for certain business verticals (gaming for example) are much more vulnerable to the impacts of code modification than others (hospitality for example). As such, it is critical to consider the business impact before deciding whether or not to address this risk.

# How Do I Prevent 'Code Tampering'?

The mobile app must be able to detect at runtime that code has been added or changed from what it knows about its integrity at compile time. The app must be able to react appropriately at runtime to a code integrity violation.

The remediation strategies for this type of risk is outlined in more technical detail within the [OWASP Reverse Engineering and Code Modification Prevention Project](https://www.owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project).

**Android Root Detection**
Typically, an app that has been modified will execute within a Jailbroken or rooted environment. As such, it is reasonable to try and detect these types of compromised environments at runtime and react accordingly (report to the server or shutdown). There are a few common ways to detect a rooted Android device: Check for test-keys

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

**iOS Jailbreak Detection**

# Example Attack Scenarios

There are a number of counterfeit applications that are available across the app stores. Some of these contain malware payloads. Many of the modified apps contain modified forms of the original core binary and associated resources. The attacker re-packages these as a new application and released them into third-party stores.

**Scenario #1:**

Games are a particularly popular target to attack using this method. The attacker will attract people that are not interested in paying for any freemium features of the game. Within the code, the attacker short-circuits conditional jumps that detect whether an in-application purchase is successful. This bypass allows the victim to attain game artifacts or new abilities without paying for them. The attacker has also inserted spyware that will steal the identity of the user.

**Scenario #2:**

Banking apps are another popular target to attack. These apps typically process sensitive information that will be useful to an attacker. An attacker could create a counterfeit version of the app that transmits the user's personally identifiable information (PII) along with username/password to a third-party site. This is reminiscent of the desktop equivalent of Zeus malware. This typically results in fraud against the bank.

# References

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