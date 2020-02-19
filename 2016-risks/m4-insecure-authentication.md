---

layout: col-sidebar
title: "M4: Insecure Authentication"
---

# Threat Agents

**Application Specific**

Threat agents that exploit authentication vulnerabilities typically do so through automated attacks that use available or custom-built tools. 

# Attack Vectors	

**Exploitability EASY**

Once the adversary understands how the authentication scheme is vulnerable, they fake or bypass authentication by submitting service requests to the mobile app's backend server and bypass any direct interaction with the mobile app. This submission process is typically done via mobile malware within the device or botnets owned by the attacker.  

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability AVERAGE**

Poor or missing authentication schemes allow an adversary to anonymously execute functionality within the mobile app or backend server used by the mobile app. Weaker authentication for mobile apps is fairly prevalent due to a mobile device's input form factor. The form factor highly encourages short passwords that are often purely based on 4-digit PINs.
Authentication requirements for mobile apps can be quite different from traditional web authentication schemes due to availability requirements.

In traditional web apps, users are expected to be online and authenticate in real-time with a backend server. Throughout their session, there is a reasonable expectation that they will have continuous access to the Internet.

In mobile apps, users are not expected to be online at all times during their session. Mobile internet connections are much less reliable or predictable than traditional web connections. Hence, mobile apps may have uptime requirements that require offline authentication. This offline requirement can have profound ramifications on things that developers must consider when implementing mobile authentication.

To detect poor authentication schemes, testers can perform binary attacks against the mobile app while it is in 'offline' mode. Through the attack, the tester will force the app to bypass offline authentication and then execute functionality that should require offline authentication (for more information on binary attacks, see M10). As well, testers should try to execute any backend server functionality anonymously by removing any session tokens from any POST/GET requests for the mobile app functionality.

# Technical Impacts	

**Impact SEVERE**

The technical impact of poor authentication is that the solution is unable to identify the user performing an action request. Immediately, the solution will be unable to log or audit user activity because the identity of the user cannot be established. This will contribute to an inability to detect the source of an attack, the nature of any underlying exploits, or how to prevent future attacks.

Authentication failures may expose underlying authorization failures as well. When authentication controls fail, the solution is unable to verify the user's identity. This identity is linked to a user's role and associated permissions. If an attacker is able to anonymously execute sensitive functionality, it highlights that the underlying code is not verifying the permissions of the user issuing the request for the action. Hence, anonymous execution of code highlights failures in both authentication and authorization controls.

# Business Impacts
	
**Application / Business Specific** 
		

The business impact of poor authentication will typically result in the following at a minimum:

- Reputational Damage
- Information Theft; or
- Unauthorized Access to Data.

# Am I Vulnerable To 'Insecure Authentication'?

There are many different ways that a mobile app may suffer from insecure authentication:

- If the mobile app is able to anonymously execute a backend API service request without providing an access token, this application suffers from insecure authentication;
- If the mobile app stores any passwords or shared secrets locally on the device, it most likely suffers from insecure authentication;
- If the mobile app uses a weak password policy to simplify entering a password, it suffers from insecure authentication; or
- If the mobile app uses a feature like TouchID, it suffers from insecure authentication.

# How Do I Prevent 'Insecure Authentication'?

**Avoid Weak Patterns**

Avoid the following Insecure Mobile Application Authentication Design Patterns:

- If you are porting a web application to its mobile equivalent, authentication requirements of mobile applications should match that of the web application component. Therefore, it should not be possible to authenticate with less authentication factors than the web browser;
- Authenticating a user locally can lead to client-side bypass vulnerabilities. If the application stores data locally, the authentication routine can be bypassed on jailbroken devices through run-time manipulation or modification of the binary. If there is a compelling business requirement for offline authentication, see M10 for additional guidance on preventing binary attacks against the mobile app;
- Where possible, ensure that all authentication requests are performed server-side. Upon successful authentication, application data will be loaded onto the mobile device. This will ensure that application data will only be available after successful authentication;
- If client-side storage of data is required, the data will need to be encrypted using an encryption key that is securely derived from the user’s login credentials. This will ensure that the stored application data will only be accessible upon successfully entering the correct credentials. There are additional risks that the data will be decrypted via binary attacks. See M9 for additional guidance on preventing binary attacks that lead to local data theft;
- Persistent authentication (Remember Me) functionality implemented within mobile applications should never store a user’s password on the device;
- Ideally, mobile applications should utilize a device-specific authentication token that can be revoked within the mobile application by the user. This will ensure that the app can mitigate unauthorized access from a stolen/lost device;
- Do not use any spoof-able values for authenticating a user. This includes device identifiers or geo-location;
- Persistent authentication within mobile applications should be implemented as opt-in and not be enabled by default;
- If possible, do not allow users to provide 4-digit PIN numbers for authentication passwords.

**Reinforce Authentication**

- Developers should assume all client-side authorization and authentication controls can be bypassed by malicious users. Authorization and authentication controls must be re-enforced on the server-side whenever possible.
- Due to offline usage requirements, mobile apps may be required to perform local authentication or authorization checks within the mobile app's code. If this is the case, developers should instrument local integrity checks within their code to detect any unauthorized code changes. See M9 for more information about detecting and reacting to binary attacks.

# Example Attack Scenarios

The following scenarios showcase weak authentication or authorization controls in mobile apps:

**Scenario #1:** Hidden Service Requests: Developers assume that only authenticated users will be able to generate a service request that the mobile app submits to its backend for processing. During the processing of the request, the server code does not verify that the incoming request is associated with a known user. Hence, adversaries submit service requests to the back-end service and anonymously execute functionality that affects legitimate users of the solution.

**Scenario #2:** Interface Reliance: Developers assume that only authorized users will be able to see the existence of a particular function on their mobile app. Hence, they expect that only legitimately authorized users will be able to issue the request for the service from their mobile device. Back-end code that processes the request does not bother to verify that the identity associated with the request is entitled to execute the service. Hence, adversaries are able to perform remote administrative functionality using fairly low-privilege user accounts.

**Scenario #3:** Usability Requirements: Due to usability requirements, mobile apps allow for passwords that are 4 digits long. Server code correctly stores a hashed version of the password. However, due to the severely short length of the password, an adversary will be able to quickly deduce the original passwords using rainbow hash tables. If the password file (or data store) on the server is compromised, an adversary will be able to quickly deduce users' passwords.

# References

- OWASP
  - [OWASP](https://www.owasp.org/index.php/OWASP_Top_Ten)
- External
  - [External References](http://cwe.mitre.org/)