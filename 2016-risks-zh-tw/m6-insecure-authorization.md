---

layout: col-sidebar
title: "M6: Insecure Authorization"
---

# Threat Agents

**Application Specific**

Threat agents that exploit authorization vulnerabilities typically do so through automated attacks that use available or custom-built tools.  

# Attack Vectors	

**Exploitability EASY**

Once the adversary understands how the authorization scheme is vulnerable, they login to the application as a legitimate user. They successfully pass the authentication control. Once past authentication, they typically force-browse to a vulnerable endpoint to execute administrative functionality. This submission process is typically done via mobile malware within the device or botnets owned by the attacker.  

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability AVERAGE**

To test for poor authorization schemes, testers can perform binary attacks against the mobile app and try to execute privileged functionality that should only be executable with a user of higher privilege while the mobile app is in 'offline' mode (for more information on binary attacks, see M9 and M10). As well, testers should try to execute any privileged functionality using a low-privilege session token within the corresponding POST/GET requests for the sensitive functionality to the backend server.Poor or missing authorization schemes allow an adversary to execute functionality they should not be entitled to using an authenticated but lower-privilege user of the mobile app. Authorization requirements are more vulnerable when making authorization decisions within the mobile device instead of through a remote server. This may be a requirement due to mobile requirements of offline usability.  

# Technical Impacts	

**Impact SEVERE**

The technical impact of poor authorization is similar in nature to the technical impact of poor authentication. The technical impact can be wide ranging in nature and dependent upon the nature of the over-privileged functionality that is executed. For example, over-privileged execution of remote or local administration functionality may result in destruction of systems or access to sensitive information. 

# Business Impacts
	
**Application / Business Specific** 
		

In the event that a user (anonymous or verified) is able to execute over-privileged functionality, the business may experience the following impacts:
- Reputational Damage;
- Fraud; or
- Information Theft.

# Am I Vulnerable To 'Insecure Authorization'?

It is important to recognize the difference between authentication and authorization. Authentication is the act of identifying an individual. Authorization is the act of checking that the identified individual has the permissions necessary to perform the act. The two are closely related as authorization checks should always immediately follow authentication of the an incoming request from a mobile device.

If an organization fails to authenticate and individual before executing an API endpoint requested from a mobile device, then the code automatically suffers from insecure authorization as well. It is essentially impossible for authorization checks to occur on an incoming request when the caller's identity is not established.

There are a few easy rules to follow when trying to determine if a mobile endpoint is suffering from insecure authorization:

- **Presence of Insecure Direct Object Reference (IDOR) vulnerabilities** - If you are seeing an Insecure Direct Object Reference Vulnerability (IDOR), the code is most likely not performing a valid authorization check; and
- **Hidden Endpoints** - Typically, developers do not perform authorization checks on backend hidden functionality as they assume the hidden functionality will only be seen by someone in the right role;
- **User Role or Permission Transmissions** - If the mobile app is transmitting the user's roles or permissions to a backend system as part of a request, it is suffering from insecure authorization.

# How Do I Prevent 'Insecure Authorization'?

In order to avoid insecure authorization checks, do the following:

- Verify the roles and permissions of the authenticated user using only information contained in backend systems. Avoid relying on any roles or permission information that comes from the mobile device itself;
- Backend code should independently verify that any incoming identifiers associated with a request (operands of a requested operation) that come along with the identify match up and belong to the incoming identity;

# Example Attack Scenarios

**Scenario #1:** Insecure Direct Object Reference:

A user makes an API endpoint request to a backend REST API that includes an actor ID and an oAuth bearer token. The user includes their actor ID as part of the incoming URL and includes the access token as a standard header in the request. The backend verifies the presence of the bearer token but fails to validate the actor ID associated with the bearer token. As a result, the user can tweak the actor ID and attain account information of other users as part of the REST API request.

**Scenario #2:** Transmission of LDAP roles:

A user makes an API endpoint request to a backend REST API that includes a standard oAuth bearer token along with a header that includes a list of LDAP groups that the user belongs to. The backend request validates the bearer token and then inspects the incoming LDAP groups for the right group membership before continuing on to the sensitive functionality. However, the backend system does not perform an independent validation of LDAP group membership and instead relies upon the incoming LDAP information coming from the user. The user can tweak the incoming header and report to be a member of any LDAP group arbitrarily and perform administrative functionality.

# References

- OWASP
  - [OWASP](https://www.owasp.org/)
- External
  - [External References](http://cwe.mitre.org/)