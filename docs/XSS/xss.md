---
layout: default
title: Cross-site Scripting(XSS)
nav_order: 4
has_children: true
permalink: /cybersecurity/xss
---

### What is cross-site scripting (XSS)?

Cross-site scripting (also known as XSS) is a web security vulnerability that allows an attacker to compromise the interactions that users have with the application. It allows an attacker to circumvent the same origin policy, which is designed to segregate different websites from each other. Cross-site scripting vulnerabilities normally allow an attacker to masquerade as a victim user, to carry out any actions that the user is able to perform, and to access any of the user's data. If the victim user has privileged access within the application, then the attacker might be able to gain full control over all of the application's functionality and data.

### How does XSS work?

Cross-site scripting works by manipulating a vulnerable web site so that it returns malicious JavaScript to users. When the malicious code executes inside a victim's browser, the attacker can fully compromise their interaction with the application.

### How dangerous is XSS?

*   Impersonate or masquerade as the victim user.
*   Carry out any action that the user is able to perform.
*   Read any data that the user is able to access.
*   Capture the user's login credentials.
*   Perform virtual defacement of the web site.
*   Inject trojan functionality into the web site.

### Types of XSS attacks

##### Stored XSS

Stored XSS, data with the payload sent by the attacker will be stored in the database of the server and the payload will be executed when ever the data was fetched and  improperly loaded by the client.

##### DOM-based XSS

The HTTP request with the malicious payload sent to the server and that malicious payload will be utilized by the vulnerable code in the client-side.

##### Reflected XSS

The HTTP request will be sent from the user which contains malicious payload that will not be processed in the back-end but it will be sent back and improperly loaded by the client.

##### Self XSS

Self XSS, we can not consider it as a serious vulnerability as this type of vulnerability requires user interaction. Here user has to paste the code and run the script sent by the attacker

> Note: Detailed explanation will be posted in another article

### How to prevent XSS attacks

*   **Filter input on arrival.** At the point where user input is received, filter as strictly as possible based on what is expected or valid input.
*   **Encode data on output.** At the point where user-controllable data is output in HTTP responses, encode the output to prevent it from being interpreted as active content. Depending on the output context, this might require applying combinations of HTML, URL, JavaScript, and CSS encoding.
*   **Use appropriate response headers.** To prevent XSS in HTTP responses that aren't intended to contain any HTML or JavaScript, you can use the `Content-Type` and `X-Content-Type-Options` headers to ensure that browsers interpret the responses in the way you intend.
*   **Content Security Policy.** As a last line of defense, you can use Content Security Policy (CSP) to reduce the severity of any XSS vulnerabilities that still occur.