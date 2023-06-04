---
layout: default
title: Types of Cross-Site Scripting - Part 3 - Stored XSS
parent: Cross-site Scripting(XSS)
nav_order: 3
has_children: false
---


### What is Stored Cross-site Scripting (Stored XSS)

Stored Cross-site scripting is a web application vulnerability that occurs when an application stores malicious java-script payload, which comes from the HTTP request and make it persistent. When ever the data was requested, the payload will be fetched and the client java script loads the data in an unsafe way.

### How Stored Cross-site Scripting works?

Let us take an example, The application with search functionality. Assume, The input we entered will be stored in the server DB for analytics purpose and sends back the queries we made, when we request for the history of searches and the client side JavaScript displays in the form of link in an unsafe way. let us consider the link as 

 `<a href="/history?query=chanu"> chanu </a>`

we can now format our query to execute the payload. So it can be done using the payload, 

`"></a><script>alert(1)</script>` Now observe the payload. Here we are closing the link tag `<a>` and executing the java-script payload using the `<script>` tag. With that our payload creation was completed 

Now let us understand how that actually works. After we enter the formatted payload, it will send to the server and it will be stored in the DB for future reference. Now if we request for the history. the data along with the payload will be fetched and client side JavaScript will process in such a way that When the DOM renders the HTML, the `<a>` tag was closed and the script containing the malicious payload will be executed. 

### How dangerous is Stored Cross-Site scripting

*   This can very critical, if the stored payload will be accessed by other user as well.
*   If the data will be utilized by the admin, then this will be critical.
*   The attacker can perform any action within the application that the user can perform, view any information that the user is able to view and modify any information that the user is able to modify.
*   The attacker can  initiate interactions with other application users, including malicious attacks, that will appear to originate from the current user.

### Ways to find Stored XSS

*   Parameters or other data within the URL query string and message body.
*   The URL file path.
*   HTTP request headers that was stored for analytics, which can be accessed by admin.
*   Any out-of-band routes via which an attacker can deliver data into the application. The routes that exist depend entirely on the functionality implemented by the application: a webmail application will process data received in emails; an application displaying a Twitter feed might process data contained in third-party tweets; and a news aggregator will include data originating on other web sites.

### How to prevent XSS attacks

*   **Filter input on arrival.** At the point where user input is received, filter as strictly as possible based on what is expected or valid input.
*   **Encode data on output.** At the point where user-controllable data is output in HTTP responses, encode the output to prevent it from being interpreted as active content. Depending on the output context, this might require applying combinations of HTML, URL, JavaScript, and CSS encoding.
*   **Use appropriate response headers.** To prevent XSS in HTTP responses that aren't intended to contain any HTML or JavaScript, you can use the `Content-Type` and `X-Content-Type-Options` headers to ensure that browsers interpret the responses in the way you intend.
*   **Content Security Policy.** As a last line of defense, you can use Content Security Policy (CSP) to reduce the severity of any XSS vulnerabilities that still occur.