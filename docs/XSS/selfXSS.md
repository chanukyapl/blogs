---
layout: default
title: Types of Cross-Site Scripting - Part 4 - Self-XSS
parent: XSS
nav_order: 4
has_children: false
---


### Self- Cross-site Scripting (Self-XSS)

DOM based Cross-site scripting is a web application vulnerability that occurs when the user himself runs the payload. Only possible way to achieve this is through Social engineering. 

### Why is it not so important? 

It requires the user interaction with the attacker. So it is not an important vulnerability. But it will work through social engineering.

### How Self-XSS works?

Let us take an example, The application with search functionality. Assume, The input we entered was processed in the client side and displays the input in an unsafe way. 

Now we enter the input `chan`, the site processes the input and display the results along with the name `search results for chan`. In place of chan we use the payload `<script>alert(1)</script>` and the payload was executed and browser raises the alert box. 

We achieved XSS. But it is not severe because, the input we entered was handled by the client side java-script in such a way that the input sent to the different endpoint or different site to just fetch the results. those results will be processed and rendered back on the DOM. So the payload will not be present on the current endpoint or any endpoint that displays the page. 

So, here the attacker has to send this payload to the user and make the user to paste it in the input box and runs it. In that case, this Self-XSS will be effective and the attacker gains the control over the user account.