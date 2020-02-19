---

layout: col-sidebar
title: "M9: Improper Session Handling"
---

# Threat Agents

**Application Specific**

Anyone or any mobile app with access to HTTP/S traffic, cookie data, etc. 

# Attack Vectors	

**Exploitability EASY**

Attack vectors include physical access to the device, and network traffic capture, or malware on the mobile device. 

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability EASY**

In order to facilitate a stateful transaction between a user and a mobile app's backend servers, mobile apps use session tokens to maintain state over stateless protocols like HTTP or SOAP. To maintain state, the mobile app must first authenticate the user through the backend. In response to successful authentication, the server issues a session cookie to the mobile app. The mobile app adds this cookie to all future service transactions between the mobile app and the server. This allows the server to conveniently enforce authentication and authorization for any service requests issued by the mobile app. Improper session handling occurs when the session token is unintentionally shared with the adversary during a subsequent transaction between the mobile app and the backend servers. 

# Technical Impacts	

**Impact SEVERE**

An adversary that has access to the session tokens is able to impersonate the user by submitting the token to the backend server for any sensitive transactions. Hence, the technical impact is dependent upon who is being impersonated and what service is being requested.
In the worst-case scenario,the adversary is impersonating an administrative user and issuing a request for administrative functionality that is dangerous in nature.

In the average-case scenario, users lose control of their accounts and who is performing authorized functionality on their behalf.

# Business Impacts
	
**Application / Business Specific** 
		
Improper session handling results in an adversary that can impersonate another user and perform business functionality on their behalf. This may result in:

- Fraud;
- Information Theft; or
- Business Interruption

# Am I Vulnerable To 'Improper Session Handling'?

This category deals with session handling and the various ways it can be done insecurely.

Improper Session Handling typically results in the same outcomes as poor authentication. Once you are authenticated and given a session, that session allows one access to the mobile application. Mobile app code must protect user sessions just as carefully as its authentication mechanism.

Here are some examples of how it is often done improperly:

**Failure to Invalidate Sessions on the Backend**

Many developers invalidate sessions on the mobile app and not on the server side, leaving a major window of opportunity for attackers who are using HTTP manipulation tools. Ensure that all session invalidation events are executed on the server side and not just on the mobile app.

Lack of Adequate Timeout Protection
Any mobile app you create must have adequate timeout protection on the backend components. This helps prevent malicious potential for an unauthorized user to gain access to an existing session and assume the role of that user.

Good timeout periods vary widely according to the sensitivity of the app, one's own risk profile, etc., but some good guidelines are:

- 15 minutes for high security applications
- 30 minutes for medium security applications
- 1 hour for low security applications

There is an increasing trend towards allowing long timeout values on mobile app sessions due to the nature of user interaction with mobile apps. Often, users are doing many things at once when using their mobile apps. Interactions tend to be sporatic, unpredictable, and drawn out over a longer timeframe than with traditional web apps. In some ways, it makes sense that longer timeout sessions are required because the interval between interactions might be longer. However, this increased session timeout window will increase the risk of session stealing if session handling is not done properly. It is important to raise this risk with the powers-that-be to ensure that session handling is handled properly.

**Failure to Properly Rotate Cookies**

Another major problem with session management implementations is the failure to properly reset cookies during authentication state changes. Authentication state changes include events like:

- Switching from an anonymous user to a logged in user
- Switching from any logged in user to another logged in user
- Switching from a regular user to a privileged user
- Timeouts

For each of these event types, it is critical that sessions are destroyed on the server side and that the cookies presented as part of the previous sessions are no longer accepted. Ideally, your application would even detect any use of said cookies and would report that to the appropriate security team.

**Insecure Token Creation**

In addition to properly invalidating tokens (on the server side) during key application events, it's also crucial that the tokens themselves are generated properly. Just as with encryption algorithms, developers should use well-established and industry-standard methods of created tokens. They should be sufficiently long, complex, and pseudo-random so as to be resistant to guessing/anticipation attacks.

# How Do I Prevent 'Improper Session Handling'?

To handle sessions properly, ensure that mobile app code creates, maintains, and destroys session tokens properly over the life-cycle of a user's mobile app session. Follow the advice above.

# Example Attack Scenarios

None

# References

- OWASP
  - [OWASP](https://www.owasp.org/)
- External
  - [External References](http://cwe.mitre.org/)