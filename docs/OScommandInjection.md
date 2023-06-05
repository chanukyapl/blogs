---
layout: default
title: OS command injection
nav_order: 5
permalink: /cybersecurity/os_command_injection
has_children: false
---

### What is OS command injection?

OS Command injection is a web application vulnerability, which allows the attacker to send a malicious OS command to take full control of the server or the infrastructure. 

### Why is OS Command injection is dangerous?

Using OS command injection, the attacker may not only controls the server or the underlying infrastructure but there are highly likely chances that the attacker may attack the other systems within the organization. 

### Example of using OS Command injection

Let us take the scenario, where the application sends us the details of restaurants near by, when we send the country and Pin/Zip code. Here these parameters will be passed into the another program and gives us the results based on the input. Let us assume the application is not handling these parameters in a safe way. 

Our example URL will be like `https://www.target.com/getrestaurantdeals?country=IN&postal=111111`

Now these parameters will be passed into the another program. Let us take it as `getrestaurantdeals.sh`. This program will take these inputs and sends back the details to the server. The command will be like `getrestaurantdeals.sh IN 111111`.

Now attacker can format the URL like `https://www.target.com/getrestaurantdeals?country=IN&postal=1111%20&%20echo%20hi` . The command that will run is `getrestaurantdeals.sh IN 111111 & echo hi`. Now along with the details of restaurants, we will get the hi text. With this the attacker can confirm that the application is vulnerable to the OS command injection on the endpoint `getrestaurantdeals`.

### Ways to find OS command injection

We can not find the OS command injection vulnerabilities directly, because we can not directly identify the endpoints that is vulnerable to the attack. So we can only blindly test our payloads to find whether the endpoint is vulnerable or not.

**Detecting using time delays**

We can introduce the time delays to find the OS Command injection. If we get the response from the server after the time delay we mentioned, then we can confirm that the endpoint is vulnerable. one such an command is `& ping -c 10 127.0.0.1 &`. Here the `-c` option will be used for introducing the time delay. If we get the response from the server after 10 sec, then we can try with other numbers and confirm the vulnerability.

**Redirecting the output to the static folder**

We can redirect the output to a file and place it in the static files serving folder. If we are able to access the file, then we can confirm that application is vulnerable to OS command injection. Example command will be like `& echo hi > /var/www/static/hi.txt &`.

**Out-of-band Application Testing (OAST ) techniques**

We can use a command that will trigger an out-of-band network interaction with a system that we control, using OAST techniques. For example:

`& nslookup <subdomain>.<ourhost>.com &`

This payload uses the `nslookup` command to cause a DNS lookup for the specified domain. The attacker can monitor for the specified lookup occurring, and thereby detect that the command was successfully injected.

### How to prevent OS command injection attacks?

*   Validating against a whitelist of permitted values.
*   Validating that the input contains only alphanumeric characters, no other syntax or white-space.
*   Never permit the shell meta-characters.