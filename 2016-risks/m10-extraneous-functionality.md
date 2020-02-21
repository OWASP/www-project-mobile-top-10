---

layout: col-sidebar
title: "M10: Extraneous Functionality"
---

# Threat Agents

**Application Specific**

Typically, an attacker seeks to understand extraneous functionality within a mobile app in order to discover hidden functionality in in backend systems. The attacker will typically exploit extraneous functionality directly from their own systems without any involvement by end-users. 
# Attack Vectors	

**Exploitability EASY**

An attacker will download and examine the mobile app within their own local environment. They will examine log files, configuration files, and perhaps the binary itself to discover any hidden switches or test code that was left behind by the developers. They will exploit these switches and hidden functionality in the backend system to perform an attack. 

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability AVERAGE**

There is a high likelihood that any given mobile app contains extraneous functionality that is not directly exposed to the user via the interface. Most of this additional code is benign in nature and will not give an attacker any additional insight into backend capabilities. However, some extraneous functionality can be very useful to an attacker. Functionality that exposes information related to back-end test, demo, staging, or UAT environments should not be included in a production build. Additionally, administrative API endpoints, or unofficial endpoints should not be included in final production builds. Detecting extraneous functionality can be tricky. Automated static and dynamic analysis tools can pick up low hanging fruit (log statements). However, some backdoors are difficult to detect in an automated means. As such, it is always best to prevent these things using a manual code review.  

# Technical Impacts	

**Impact SEVERE**

The technical impact from extraneous functionality includes the following:
- Exposure of how backend systems work; or
- Unauthorized high-privileged actions executed.


# Business Impacts
	
**Application / Business Specific** 
		

The business impact from extraneous functionality includes the following:
- Unauthorized Access to Sensitive Functionality;
- Reputational Damage; or
- Intellectual Property Theft.

# Am I Vulnerable To 'Extraneous Functionality'?

Often, developers include hidden backdoor functionality or other internal development security controls that are not intended to be released into a production environment. For example, a developer may accidentally include a password as a comment in a hybrid app. Another example includes disabling of 2-factor authentication during testing.

The defining characteristic of this risk is leaving functionality enabled in the app that was not intended to be released.

# How Do I Prevent 'Extraneous Functionality'?

The best way to prevent this vulnerability is to perform a manual secure code review using security champs or subject matter experts most knowledgable with this code. They should do the following:

1. Examine the app's configuration settings to discover any hidden switches;
2. Verify that all test code is not included in the final production build of the app;
3. Examine all API endpoints accessed by the mobile app to verify that these endpoints are well documented and publicly available;
4. Examine all log statements to ensure nothing overly descriptive about the backend is being written to the logs;

# Example Attack Scenarios

**Scenario #1**: Administrative Endpoint Exposed:

As part of mobile endpoint testing, developers included a hidden interface within the mobile app that would display an administrative dashboard. This dashboard accessed admin information via the back-end API server. In the production version of the code, the developers did not include code that displayed the dashboard at any time. However, they did include the underlying code that could access the back-end admin API. An attacker performed a string table analysis of the binary and discovered the hardcoded URL to an administrative REST endpoint. The attacker subsequently used 'curl' to execute back-end administrative functionality.

The developers should have removed all extraneous code, including code that is not directly reachable by the native interface.

**Scenario #2**: Debug Flag in Configuration File:

An attacker tries manually added "debug=true" to a .properties file in a local app. Upon startup, the application is outputting log files that are overly descriptive and helpful to the attacker in understanding the backend systems. The attacker subsequently discovers vulnerabilities within the backend system as a result of the log.

The developers should have prevented the activation of 'debug mode' within a production build of the mobile app.

# References

- OWASP
  - [OWASP](https://www.owasp.org/)
- External
  - [External References](http://cwe.mitre.org/)