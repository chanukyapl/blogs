---
layout: default
title: Types of Cross-Site Scripting - Part 1 - Reflected XSS
parent: Cross-site Scripting(XSS)
nav_order: 1
has_children: false
---

### Reflected Cross-site Scripting (Reflected XSS)

Reflected Cross-site scripting is a web application vulnerability that occurs when an application receives malicious java-script payload in an HTTP request and sends back that malicious payload within the immediate response and utilizes that in an unsafe way.

For example, let us consider we are having an login form, where we have to pass username and password to the server to validate. The HTTP request will be like

    POST /login/user HTTP/1.1
    Host: target.com
    Content-Length: 100
    
    username=chanu&password=Chanu

The request will be processed and the server may sent the response which contains the error message and the username, we sent.

And consider, application is displaying the error message along with the username without validating it.

Now replace the username i.e chanu with <script>alert("Chanu")</script>. Now the browser will respond with the alert box. 

If that is the case, then we can consider that the endpoint it vulnerable to  Reflected Cross-site Scripting. There  by the application is vulnerable to Reflected Cross-site scripting.

### How dangerous is Reflected Cross-Site scripting

*   In short term we can call “user is compromised”
*   The attacker can perform any action within the application that the user can perform, view any information that the user is able to view and modify any information that the user is able to modify.
*   The attacker can  initiate interactions with other application users, including malicious attacks, that will appear to originate from the current user.