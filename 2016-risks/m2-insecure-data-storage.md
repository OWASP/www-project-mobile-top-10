---

layout: col-sidebar
title: "M2: Insecure Data Storage"
---

# Threat Agents

**Application Specific**

Threats agents include the following: an adversary that has attained a lost/stolen mobile device; malware or another repackaged app acting on the adversary's behalf that executes on the mobile device.  

# Attack Vectors	

**Exploitability EASY**

In the event that an adversary physically attains the mobile device, the adversary hooks up the mobile device to a computer with freely available software. These tools allow the adversary to see all third party application directories that often contain stored personally identifiable information (PII) or other sensitive information assets. An adversary may construct malware or modify a legitimate app to steal such information assets. 

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability AVERAGE**

Insecure data storage vulnerabilities occur when development teams assume that users or malware will not have access to a mobile device's filesystem and subsequent sensitive information in data-stores on the device. Filesystems are easily accessible. Organizations should expect a malicious user or malware to inspect sensitive data stores. Usage of poor encryption libraries is to be avoided. Rooting or jailbreaking a mobile device circumvents any encryption protections. When data is not protected properly, specialized tools are all that is needed to view application data.

# Technical Impacts	

**Impact SEVERE**

This can result in data loss, in the best case for one user, and in the worst case for many users. It may also result in the following technical impacts: extraction of the app's sensitive information via mobile malware, modified apps or forensic tools.
The nature of the business impact is highly dependent upon the nature of the information stolen. Insecure data may result in the following business impacts:

- Identity theft;
- Privacy violation;
- Fraud;
- Reputation damage;
- External policy violation (PCI); or
- Material loss.

# Business Impacts
	
**Application / Business Specific** 
		

Insecure data storage vulnerabilities typically lead to the following business risks for the organization that owns the risk app:

- Identity Theft
- Fraud
- Reputation Damage
- External Policy Violation (PCI); or
- Material Loss.

# Am I Vulnerable To 'Insecure Data Storage'?

This category insecure data storage and unintended data leakage. Data stored insecurely includes, but is not limited to, the following:

- SQL databases;
- Log files;
- XML data stores or manifest files;
- Binary data stores;
- Cookie stores;
- SD card;
- Cloud synced.

Unintended data leakage includes, but is not limited to, vulnerabilities from:

- The OS;
- Frameworks;
- Compiler environment;
- New hardware.
- Rooted or Jailbroken devices

This is obviously without a developer's knowledge. In mobile development specifically, this is most seen in undocumented, or under-documented, internal processes such as:

- The way the OS caches data, images, key-presses, logging, and buffers;
- The way the development framework caches data, images, key-presses, logging, and buffers;
- The way or amount of data ad, analytic, social, or enablement frameworks cache data, images, key-presses, logging, and buffers.

# How Do I Prevent 'Insecure Data Storage'?

It is important to threat model your mobile app, OS, platforms and frameworks to understand the information assets the app processes and how the APIs handle those assets. It is crucial to see how they handle the following types of features :

- URL caching (both request and response);
- Keyboard press caching;
- Copy/Paste buffer caching;
- Application backgrounding;
- Intermediate data
- Logging;
- HTML5 data storage;
- Browser cookie objects;
- Analytics data sent to 3rd parties.

# Example Attack Scenarios

**A Visual Example**

iGoat is a purposefully vulnerable mobile app for the security community to explore these types of vulnerabilities first hand. In the exercise below, we enter our credentials and log in to the fake bank app. Then, we navigate to the file system. Within the applications directory, we can see a database called “credentials.sqlite”. Exploring this database reveals that the application is storing our username and credentials (Jason:pleasedontstoremebro!) in plain text.

![Local Data Storage](https://wiki.owasp.org/images/6/6d/Screen_Shot_2012-12-19_at_6.34.23_AM.png)
![Goat Hills Financial](https://wiki.owasp.org/images/9/98/Screen_Shot_2012-12-19_at_6.44.51_AM.png)
![Terminal](https://wiki.owasp.org/images/5/5a/Screen_Shot_2012-12-19_at_10.11.15_AM.png)

# References

- OWASP
  - [OWASP iOS Developer Cheat Sheet](https://www.owasp.org/index.php/IOS_Developer_Cheat_Sheet)
- External
  - [Google Androids Developer Security Topics 1](http://source.android.com/tech/security/)
  - [Google Androids Developer Security Topics 2](http://developer.android.com/training/articles/security-tips.html)
  - [Apple's Introduction to Secure Coding](https://developer.apple.com/library/mac/)
  - [Fortify On Demand Blog - Exploring The OWASP Mobile Top 10: Insecure Data Storage](http://h30499.www3.hp.com/t5/Application-Security-Fortify-on/Exploring-The-OWASP-Mobile-Top-10-M1-Insecure-Data-Storage/ba-p/5904609)
