---
layout: col-sidebar
title: "M4: Inadequate Privacy Controls"
---

# Threat Agents

**Application Specific**

Privacy controls are concerned with protecting Personally Identifiable Information (PII). This information is valuable to attackers for various reasons, e.g., for

- impersonating the victims in cases of fraud,
- misusing the victims' payment data, or
- blackmailing the victims with sensitive information.

# Attack Vectors	

**Exploitability MEDIUM**

Typical sources for PII are either protected or hard to access, e.g., the sandbox of the app, the network communication with the server, the app's logs and backups. Some are easier to observe, like URL query parameters and clipboard content.

Obtaining PII thus requires the attacker to breach security on another level. He could eavesdrop on the network communication, access file system, clipboard or logs with a trojan or get his hands on the mobile device and create a backup to analyse.

# Security Weakness	

**Prevalence COMMON** <br/>
**Detectability EASY**

Risks of privacy violations increase due to careless handling of PII by developers. PII should always be processed with the posibility in mind that an attacker could access communication and storage media. Hence, PII should not be stored or transfered
unless absolutely necessary. If it is to store or transfer, one should consider encrypting or anonymizing it if feasible. Leakage of PII to uncontrollable sinks, e.g., logs, clipboard, url-parameters, must be prevented.


# Technical Impacts	

**Impact LOW**

Privacy violations usually have little technical impact on the system as a whole. Only if the PII includes information like authentication data, it can affect traceability. If user data is manipulated it might render the system unusable for that user.


# Business Impacts
	
**Impact SEVERE** 

The business impact of privacy violations will typically result in the following at a minimum:

- Loss or theft of personally identifiable informationInformation 
- Reputational damage
- Financial damage if jurisdiction mandates protection of PII, e.g., the European General Data Protection Regulation


# Am I Vulnerable To 'Inadequate Privacy Controls'?

Are you using PII?
Do you store and transfer them securely (cf. M2, M8)?
Are protected backups enabled?
Do they leak to externally accessible sinks, like clipboard, url-parameters, intents/broadcasts, logs/error messages?


# How Do I Prevent 'Inadequate Privacy Controls'?

Be aware of the most valuable PII assets you are using in your app. Use threat modeling to assess the most likely ways that privacy violations may occur for your app. Use static analyses to reveal common pitfalls, like logging of PII or leakage to URL query parameters. Consider platform or 3rd party tools to sanitize logs and error messages.


# Example Attack Scenarios

The following scenarios showcase inadequate privacy controls in mobile apps:

**Scenario #1:** inadequate sanitization of logs and error messages

**Scenario #2:** using PII in URL query parameters

**Scenario #3:** Exclusion of personal data in backups/not setting hasFragileUserData

# References

- OWASP
  - [OWASP](https://www.owasp.org/index.php/OWASP_Top_Ten)
- External
  - [External References](http://cwe.mitre.org/)
