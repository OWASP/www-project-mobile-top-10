---
layout: col-sidebar
title: "M4: Inadequate Privacy Controls"
---

# Threat Agents

**Application Specific**

Privacy controls are concerned with protecting Personally Identifiable Information (PII), e.g., names and addresses, credit card information, e-mail and IP addresses, information about health, religion, sexuality and political opinions. 

This information is valuable to attackers for various reasons. For example, an attacker could

- impersonate the victim to commit a fraud,
- misuse the victim's payment data,
- blackmail the victim with sensitive information or
- harm the victim by destroying or manipulating the victim's critical data.


# Attack Vectors	

**Exploitability MEDIUM**

Typical sources for PII are well protected, e.g., the sandbox of the app, the network communication with the server, the app's logs and backups. Some have less protection but are still hard to access, like URL query parameters and clipboard content.

Obtaining PII thus requires the attacker to first breach security on another level. Attackers could eavesdrop on the network communication, access file system, clipboard or logs with a trojan or get their hands on the mobile device and create a backup to analyze. Since PII is just data that can be stored, processed and transmitted by all means available on mobile devices, the possibilities to extract or manipulate it are manifold.


# Security Weakness	

**Prevalence COMMON** <br/>
**Detectability EASY**

Almost all apps process some kind of PII. Many even collect and process more than they actually need to fulfill their purpose, which makes them more attractive as a target without business needs.

Risks of privacy violations increase due to careless handling of PII by developers. PII should always be processed with the posibility in mind that an attacker could access communication and storage media. 

Hence, an app is vulnerable to privacy infringements if some personal data it collects motivates an attacker to manipulate or abuse that data through a storage or transmission medium that is insufficiently secured.


# Technical Impacts	

**Impact LOW**

Privacy violations usually have little technical impact on the system as a whole. Only if the PII includes information like authentication data, it can affect certain global security properties, e.g., traceability. 

If user data is manipulated it might render the system unusable for that user. Through ill-formed data, also the backend might be disturbed if it is missing proper sanitization and exception handling.


# Business Impacts

**Impact SEVERE** 

The business impact of privacy violations will typically result in the following at a minimum:

- Violation of legal regulations
- Financial damage due to victims' lawsuits
- Reputational damage
- Loss or theft of PII

Regulations are the biggest issue regarding privacy controls.  GDPR (Europe), CCPA (California, US), PDPA (Singapore), PIPEDA (Canada), LGPD (Brazil), Data Protection Act 2018 (UK), POPIA (South Africa), PDPL (China) are examples of relevant regulations with known sanctions against companies for not protecting their users' data.


# Am I Vulnerable To 'Inadequate Privacy Controls'?

Are you using PII?
Do you store and transfer them securely (cf. M2, M9)?
Are protected backups enabled?
Do they leak to externally accessible sinks, like clipboard, url-parameters, intents/broadcasts, logs/error messages?


# How Do I Prevent 'Inadequate Privacy Controls'?

The safest approach to prevent privacy violations is to minimize the amount and variety of PII that is processed.

PII should not be stored or transferred unless absolutely necessary. If it is to store or transfer, one should consider encrypting, anonymizing, or reducing it if feasible. Leakage of PII to uncontrollable sinks, e.g., logs, clipboard, URL-parameters, must be prevented.

Be aware of the most valuable PII assets you are processing in your app. Use threat modeling to assess the most likely ways that privacy violations may occur. Use static analyses to reveal common pitfalls, like logging of PII or leakage to URL query parameters. Consider platform or 3rd party tools to sanitize logs and error messages. -> Not sure how relevant. 3rd party SDK and analytics data leakage are not covered. I would also argue that Static Analysis is not efficient enough to detect leaks of PII.

data deletion mechanisms
user awareness and control
granular privacy settings


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
