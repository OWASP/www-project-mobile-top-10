---

layout: col-sidebar
title: "M7: Client Side Injection"
---

# Threat Agents

**Application Specific**

Consider anyone who can send untrusted data to the mobile app, including external users, internal users, the application itself or other malicious apps on the mobile device.	

# Attack Vectors	

**Exploitability EASY**

The adversary loads simple text-based attacks that exploit the syntax of the targeted interpreter within the mobile app. Almost any source of data can be an injection vector, including resource files or the application itself.	

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability EASY**

Client-side injection results in the execution of malicious code on the mobile device via the mobile app. Typically, this malicious code is provided in the form of data that the threat agent inputs to the mobile app through a number of different means. The data is malformed and is processed (like all other data) by the underlying frameworks supporting the mobile app. During processing, this special data is forces a context switch and the framework reinterprets the data as executable code. The code is malicious in nature and executed by the app. In the "best-case" scenario, the code runs with the same scope and access permissions as the user that has unintentionally executed this code. In the worst-case scenario, the code executes with privileged permissions and much greater scope leading to much greater damage potential than in the "best-case" scenario. There are other forms of client-side injection that involve direct injection of binary code into the mobile app via binary attacks. This brute-force approach to malicious code execution may lead to even greater potential for damage than data injections. For more information on binary attacks, see M10.	

# Technical Impacts	

**Impact MODERATE**

To properly determine the technical impact, you must threat model the application. Injection attacks such as SQL Injection on mobile devices can be severe if your application deals with more than one user account on a single application or a shared device or paid-for content. Other injection points are meant to overflow applications components but are less likely to achieve a high impact result because of the managed code protections of the application languages.	

# Business Impacts
	
**Application / Business Specific** 
		

The business impact of client-side injection is dependent upon the nature of the malicious code executed by the adversary. Typically, malicious code steals sensitive information (passwords; session cookies; personally identifiable information; etc). Hence, the associated business impacts include:
- Fraud; and
- Privacy Violations.


# Am I Vulnerable To 'Client Side Injection'?

The best way to find out if an application is vulnerable to injection is to identify the sources of input and validate that user/application supplied data is being subject to input validation, disallowing code injection. Checking the code is a fast and accurate way to see if the application is handling data correctly. Code analysis tools can help a security analyst find the use of interpreters and trace the data flow through the application. Manual penetration testers can confirm these issues by crafting exploits that confirm the vulnerability.

Since data can come from many sources in mobile applications, it is important to list them delineated by what they are trying to achieve. In general, injection attacks on mobile devices target the following:


**Data on the Device:**

- SQL Injection: SQLite (many phones default data storing mechanism) can be subject to injection just like in web applications. The threat of being able to see data using this type of injection is risky when your application houses several different users, paid-for/unlockable content, etc.
- Local File Inclusion: File handling on mobile devices has the same risks as stated above except it pertains to reading files that might be yours to view inside the application directory.

**The Mobile Users Session:**

- JavaScript Injection (XSS, Etc): The mobile browser is subject to JavaScript injection as well. Usually the mobile browser has access to the mobile applications cookie, which can lead to session theft.

**The Application Interfaces or Functions:**

- Several application interfaces or language functions can accept data and can be fuzzed to make applications crash. While most of these flaws do not lead to overflows because of the phone’s platforms being managed code, there have been several that have been used as a “userland” exploit in an exploit chain aimed at rooting or jailbreaking devices.

** Binary Code Itself:**

- Mobile malware or other malicious apps may perform a binary attack against the presentation layer (HTML; JavaScript; Cascading Style Sheets CSS) or the actual binary of the mobile app's executable. These code injections are executed either by the mobile app's framework or the binary itself at run-time.


# How Do I Prevent 'Client Side Injection'?

In general, protecting you application from client side injection requires looking at all the areas your application can receive data from and applying some sort of input validation. In certain cases this is simple but for others it is more complex, see below:


**iOS Specific Best Practices:**


- **SQLite Injection:** When designing queries for SQLite be sure that user supplied data is being passed to a parameterized query. This can be spotted by looking for the format specifier used. In general, dangerous user supplied data will be inserted by a “%@” instead of a proper parameterized query specifier of “?”.
- **JavaScript Injection (XSS, etc)**: Ensure that all UIWebView calls do not execute without proper input validation. Apply filters for dangerous JavaScript characters if possible, using a whitelist over blacklist character policy before rendering. If possible call mobile Safari instead of rending inside of UIWebkit which has access to your application.
- **Local File Inclusion**: Use input validation for NSFileManager calls.
- **XML Injection**: use libXML2 over NSXMLParser
- **Format String Injection**: Several Objective C methods are vulnerable to format string attacks:
  - NSLog, [NSString stringWithFormat:], [NSString initWithFormat:], [NSMutableString appendFormat:], [NSAlert informativeTextWithFormat:], [NSPredicate predicateWithFormat:], [NSException format:], NSRunAlertPanel.
  - Do not let sources outside of your control, such as user data and messages from other applications or web services, control any part of your format strings.
- **Classic C Attacks**: Objective C is a superset of C, avoid using old C functions vulnerable to injection such as: strcat, strcpy, strncat, strncpy, sprint, vsprintf, gets, etc.

**Android Specific Best Practices:**


- **SQL Injection**: When dealing with dynamic queries or Content-Providers ensure you are using parameterized queries.
- **JavaScript Injection (XSS)**: Verify that JavaScript and Plugin support is disabled for any WebViews (usually the default).
- **Local File Inclusion**: Verify that File System Access is disabled for any WebViews (webview.getSettings().setAllowFileAccess(false);).
- **Intent Injection/Fuzzing**: Verify actions and data are validated via an Intent Filter for all Activities.

**Binary Injection / Modification Prevention for Android and iOS:**


- See M10 for more information on best practices around preventing, detecting, and reacting to binary injection by an adversary.

# Example Attack Scenarios

Classic client-side injection scenarios include the following:

1. SQL Injection - Data retrieved from a mobile app's server contains malformed data that results in a local SQL injection within the mobile device's local databases. Local SQL injections may result in local malware injection, information theft, and much more;
2. Cross-Application Scripting Attacks - Malicious intents fed from one Android application to another may result in buffer overflows that allow for malicious code execution;
3. Cross-Site Script Attacks - Local HTML modifications via malware or other apps results in execution of malicious JavaScript in the presentation layer of the app. This may result in information theft.

# References

- [Apple’s Secure Coding Guide](https://developer.apple.com/library/mac/#documentation/security/conceptual/SecureCodingGuide)
- [Fortify Software: Format Strings - Is Objective C Objectively Safer?](http://blog.fortify.com/blog/2012/07/25/Format-Strings-Is-Objective-C-Objectively-Safer)
- [Ilja Van Sprundel – Auditing iPhone and iPad Applications](http://www.youtube.com/watch?v=FJvyLUjbAy0)
- [Adventures with Android WebViews](http://labs.mwrinfosecurity.com/blog/2012/04/23/adventures-with-android-webviews/)