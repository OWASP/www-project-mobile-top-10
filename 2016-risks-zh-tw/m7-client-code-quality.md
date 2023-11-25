---

layout: col-sidebar
title: "M7: Poor Code Quality"
---

# Threat Agents

**Application Specific**

Threat Agents include entities that can pass untrusted inputs to method calls made within mobile code. These types of issues are not necessarily security issues in and of themselves but lead to security vulnerabilities. For example, buffer overflows within older versions of Safari (a poor code quality vulnerability) led to high risk drive-by Jailbreak attacks. Poor code-quality issues are typically exploited via malware or phishing scams.  

# Attack Vectors	

**Exploitability DIFFICULT**

An attacker will typically exploit vulnerabilities in this category by supplying carefully crafted inputs to the victim. These inputs are passed onto code that resides within the mobile device where exploitation takes place. Typical types of attacks will exploit memory leaks and buffer overflows. 

# Security Weakness	

**Prevalence COMMON** <br />
**Detectability DIFFICULT**

Code quality issues are fairly prevalent within most mobile code. The good news is that most code quality issues are fairly benign and result in bad programming practice. It is typically difficult to detect these types of issues through manual code review. Instead, attackers will use third-party tools that perform static analysis or perform fuzzing. These types of tools will typically identify memory leaks, buffer overflows, and other less severe issues that result in bad programming practice. Hackers with extreme low-level knowledge and expertise are able to effectively exploit these types of issues. The typical primary goal is to execute foreign code within the mobile code's address space.  

# Technical Impacts	

**Impact MODERATE**

Most exploitations that fall into this category result in foreign code execution or denial of service on remote server endpoints (and not the mobile device itself). However, in th event that buffer overflows/overruns do exist within the mobile device and the input can be derived from an external party, this could have a severely high technical impact and should be remediated.  

# Business Impacts
	
**Application / Business Specific** 
		

The business impact from this category of vulnerabilities varies greatly, depending upon the nature of the exploit. Poor code quality issues that result in remote code execution could lead to the following business impacts:
- Information Theft;
- Reputational Damage;
- Intellectual Property Theft

Other less severe technical issues that fall into this category may lead to degradations in performance, memory usage, or poor front-end architecture.

# Am I Vulnerable To 'Poor Code Quality'?

This is the catch-all for code-level implementation problems in the mobile client. That's distinct from server-side coding mistakes. This captures the risks that come from vulnerabilities like buffer overflows, format string vulnerabilities, and various other code-level mistakes where the solution is to rewrite some code that's running on the mobile device.

This is distinct from Improper Platform Usage because it usually refers to the programming language itself (e.g., Java, Swift, Objective C, JavaScript). A buffer overflow in C or a DOM-based XSS in a Webview mobile app would be code quality issues.

The key characteristic of this risk is that it's code executing on the mobile device and the code needs to be changed in a fairly localised way. Fixing most risks requires code changes, but in the code quality case the risk comes from using the wrong API, using an API insecurely, using insecure language constructs, or some other code-level issue. Importantly: this is not code running on the server. This is a risk that captures bad code that executes on the mobile device itself.

# How Do I Prevent 'Poor Code Quality'?

In general, code quality issues can be avoided by doing the following:

- Maintain consistent coding patterns that everyone in the organization agrees upon;
- Write code that is easy to read and well-documented;
- When using buffers, always validate that the the lengths of any incoming buffer data will not exceed the length of the target buffer;
- Via automation, identify buffer overflows and memory leaks through the use of third-party static analysis tools; and
- Prioritize solving buffer overflows and memory leaks over other 'code quality' issues.

# Example Attack Scenarios

**Scenario #1:** Buffer Overflow example:

```
include <stdio.h>

 int main(int argc, char **argv)
 {
    char buf[8]; // buffer for eight characters
    gets(buf); // read from stdio (sensitive function!)
    printf("%s\n", buf); // print out data stored in buf
    return 0; // 0 as return value
 }
```
 
In this example, taken from [this](https://www.owasp.org/index.php/Buffer_overflow_attack) page, we should avoid the use of the gets function to avoid a buffer overflow. This is an example of what most static analysis tools will report as a code quality issue.

# References

- OWASP
  - [Buffer Overflow Examples](https://www.owasp.org/index.php/Buffer_overflow_attack)
- External
  - [External References](http://cwe.mitre.org/)