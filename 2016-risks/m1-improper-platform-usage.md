---

layout: col-sidebar
title: "M1: Improper Platform Usage"
---

# Threat Agents

**Application Specific**

This category covers misuse of a platform feature or failure to use platform security controls. It might include Android intents, platform permissions, misuse of TouchID, the Keychain, or some other security control that is part of the mobile operating system.

# Attack Vectors	

**Exploitability EASY**

The attack vectors correspond to the same attack vectors available through the traditional OWASP Top Ten. Any exposed API call can serve as attack vector here.

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability AVERAGE**

In order for this vulnerability to be exploited, the organization must expose a web service or API call that is consumed by the mobile app. The exposed service or API call is implemented using insecure coding techniques that produce an OWASP Top Ten vulnerability within the server. Through the mobile interface, an adversary is able to feed malicious inputs or unexpected sequences of events to the vulnerable endpoint. Hence, the adversary realizes the original OWASP Top Ten vulnerability on the server.

# Technical Impacts	

**Impact SEVERE**

The technical impact of this vulnerability corresponds to the technical impact of the associated vulnerability (defined in the OWASP Top Ten) that the adversary is exploiting via the mobile device.
		 	
For example, an adversary may exploit a Cross-Site Scripting (XSS) vulnerability via the mobile device. This corresponds to the OWASP Top Ten A3 - XSS Category with a technical impact of moderate.

# Business Impacts
	
**Application / Business Specific** 
		

The business impact of this vulnerability corresponds to the business impact of the associated vulnerability (defined in the OWASP Top Ten) that the adversary is exploiting via the mobile device.

For example, an adversary may exploit a Cross-Site Scripting (XSS) vulnerability via the mobile device. This corresponds to the OWASP Top Ten A3 - XSS Category's business impacts.

# Am I Vulnerable To 'Improper Platform Usage'?

The defining characteristic of risks in this category is that the platform (iOS, Android, Windows Phone, etc.) provides a feature or a capability that is documented and well understood. The app fails to use that capability or uses it incorrectly. This differs from other mobile top ten risks because the design and implementation is not strictly the app developer's issue.

There are several ways that mobile apps can experience this risk.

1. **Violation of published guidelines.** All platforms have development guidelines for security (c.f., ((Android)), ((iOS)), ((Windows Phone))). If an app contradicts the best practices recommended by the manufacturer, it will be exposed to this risk. For example, there are guidelines on how to use the iOS Keychain or how to secure exported services on Android. Apps that do not follow these guidelines will experience this risk.

2. **Violation of convention or common practice.** Not all best practices are codified in manufacturer guidance. In some instances, there are de facto best practices that are common in mobile apps.

3. **Unintentional Misuse.** Some apps intend to do the right thing, but actually get some part of the implementation wrong. This could be a simple bug, like setting the wrong flag on an API call, or it could be a misunderstanding of how the protections work.

Failures in the platform's permission models fall into this category. For example, if the app requests too many permissions or the wrong permissions, that is best categorised here.

# How Do I Prevent 'Improper Platform Usage'?

Secure coding and configuration practices must be used on server-side of the mobile application. For specific vulnerability information, refer to the OWASP Web Top Ten or Cloud Top Ten projects.

# Example Attack Scenarios

Because there are several platforms, each with hundreds or thousands of APIs, the examples in this section only scratch the surface of what is possible.

**App Local Storage Instead of Keychain** The iOS Keychain is a secure storage facility for both app and system data. On iOS, apps should use it to store any small data that has security significance (session keys, passwords, device enrolment data, etc.). A common mistake is to store such items in app local storage. Data stored in app local storage is available in unencrypted iTunes backups (e.g., on the user's computer). For some apps, that exposure is inappropriate.

Below, you can see that there are many risks and vulnerabilities that you must mitigate in order to satisfy M1:


![Cloud Top 10 Risks](https://wiki.owasp.org/images/f/fd/CloudTT_thum.png) <br />
![OWASP Top 10 - 2013](https://wiki.owasp.org/images/7/7e/WebTT_thumb.png)


**The Worst Offenders**
Below is a list vulnerability types that OWASP sees most often within mobile applications:

- **Poor Web Services Hardening**
  - Logic flaws
    - [Testing for business logic flaws](https://www.owasp.org/index.php/Testing_for_business_logic_(OWASP-BL-001))
    - [Business Logic Security Cheat Sheet](https://www.owasp.org/index.php/Business_Logic_Security_Cheat_Sheet)
  - Weak Authentication
    - [OWASP Top Ten Broken Authentication Section](https://www.owasp.org/index.php/Top_10_2013-A2-Broken_Authentication_and_Session_Management)
    - [Authentication Cheat Sheet](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
    - [Developers Guide for Authentication](https://www.owasp.org/index.php/Guide_to_Authentication)
    - [Testing for Authentication](https://www.owasp.org/index.php/Testing_for_authentication)
  - Weak or no session management
  - Session fixation
  - Sensitive data transmitted using GET method
- **Insecure web server configurations**
  - Default content
  - Administrative interfaces
- **Injection (SQL, XSS, Command) on both web services and mobile-enabled websites**
- **Authentication flaws**
- **Session Management flaws**
- **Access control vulnerabilities**
- **Local and Remote File Includes**

# References

- OWASP
  - [OWASP Top Ten](https://www.owasp.org/index.php/OWASP_Top_Ten)
- External
  - [External References](http://cwe.mitre.org/)
