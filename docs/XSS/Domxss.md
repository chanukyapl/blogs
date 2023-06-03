---
layout: default
title: Types of Cross-Site Scripting - Part 2 - DOM based XSS
parent: Cross-site Scripting(XSS)
nav_order: 2
has_children: false
---

### DOM based Cross-site Scripting (DOM XSS)

DOM based Cross-site scripting is a web application vulnerability that occurs when an application receives malicious java-script payload in an HTTP request and sends back it and utilizes the payload in the later section of the HTML or javascript that can trigger the attack.

Let us take an example, The application with search functionality. Assume, The input we entered was processed in the client side and displayed in the form of link in an unsafe way. let us consider the link as 

 `<a href="/yourenteredinput?query=chanu"> Last Search </a>`

we can now format our query to execute the payload. So it can be done using the payload, 

`"></a><script>alert(1)</script>` Now observe the payload. Here we are closing the link tag `<a>` and executing the java-script payload using the `<script>` tag. With that our payload creation was completed 

Now let us understand how that actually works. After we enter the formatted payload, it will send to the server and send back the data. But here the client side java-script make a note of the input and process it to display the link to show last input we search for and writing it on the DOM. When the DOM renders the HTML, the `<a>` tag was closed and the script containing the malicious payload will be executed. 

### How dangerous is DOM based Cross-Site scripting

*   In short term we can call “user is compromised”
*   The attacker can perform any action within the application that the user can perform, view any information that the user is able to view and modify any information that the user is able to modify.
*   The attacker can  initiate interactions with other application users, including malicious attacks, that will appear to originate from the current user.

### Ways to find DOM based XSS

##### Testing HTML sinks

*   To test for DOM XSS in an HTML sink, place a random alphanumeric string into the source (such as `location.search`), then use developer tools to inspect the HTML and find where your string appears. 

> Note that the browser's "View source" option won't work for DOM XSS testing because it doesn't take account of changes that have been performed in the HTML by JavaScript. In Chrome's developer tools, you can use `Control+F` (or `Command+F` on MacOS) to search the DOM for your string.

*   For each location where the string appears within the DOM, we need to identify the context. Based on this context, we need to modify the input to see how it is processed. For example, if the string appears within a double-quoted attribute then try to inject double quotes in the string to see if we can break out of the attribute.

> Note that browsers behave differently with regards to URL-encoding, Chrome, Firefox, and Safari will URL-encode `location.search` and `location.hash`, while IE11 and Microsoft Edge (pre-Chromium) will not URL-encode these sources. If our data gets URL-encoded before being processed, then an XSS attack is unlikely to work.

##### Testing JavaScript execution sinks 

We'll need to use the JavaScript debugger to determine whether and how the input is sent to a sink.

For each potential source, such as `location`, we first need to find cases within the page's JavaScript code where the source is being referenced. 

Once we found where the source is being read, we can use the JavaScript debugger to add a break point and follow how the source's value is used. We might find that the source gets assigned to other variables. If this is the case, we'll need to use the search function again to track these variables and see if they're passed to a sink. When we find a sink that is being assigned data that originated from the source, we can use the debugger to inspect the value by hovering over the variable to show its value before it is sent to the sink. Then, as with HTML sinks, we need to refine the input to see if we can deliver a successful XSS attack.

### Sinks  that can lead to DOM-XSS vulnerabilities

The following are some of the main sinks that can lead to DOM-XSS vulnerabilities:

    document.write()
    document.writeln()
    document.domain
    element.innerHTML
    element.outerHTML
    element.insertAdjacentHTML
    element.onevent

### How to prevent XSS attacks

*   **Filter input on arrival.** At the point where user input is received, filter as strictly as possible based on what is expected or valid input.
*   **Encode data on output.** At the point where user-controllable data is output in HTTP responses, encode the output to prevent it from being interpreted as active content. Depending on the output context, this might require applying combinations of HTML, URL, JavaScript, and CSS encoding.
*   **Use appropriate response headers.** To prevent XSS in HTTP responses that aren't intended to contain any HTML or JavaScript, you can use the `Content-Type` and `X-Content-Type-Options` headers to ensure that browsers interpret the responses in the way you intend.
*   **Content Security Policy.** As a last line of defense, you can use Content Security Policy (CSP) to reduce the severity of any XSS vulnerabilities that still occur.