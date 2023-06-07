---
layout: default
title: Information Disclosure
nav_order: 5
permalink: /cybersecurity/information_disclosure
has_children: false
---

### What is Information disclosure?

Information disclosure is disclosing the sensitive information about the users, architecture or business data which is unintentionally revealed to the users.

### What is the impact of Information disclosure?

The impact for information disclosure will be depending on the classified data and context of usage. If the attacker gets the information about technical architecture, then it will be easy for him to set up the payloads and eventually he can succeed in the attack. If the competitor get the details of business data, then they may take counter measure for the technology or information that was disclosed.

### Check points for information disclosure

*   Revealing the names of hidden directories, their structure, and their contents via a `robots.txt` file or directory listing
*   Providing access to source code files via temporary backups
*   Explicitly mentioning database table or column names in error messages
*   Unnecessarily exposing highly sensitive information, such as credit card details
*   Hard-coding API keys, IP addresses, database credentials, and so on in the source code
*   Hinting at the existence or absence of resources, usernames, and so on via subtle differences in application behavior
*   Developer comments will be sometimes very valuable.
*   Check whether debug information is disclosed in production environment
*   Flaws in validating the information or errors

How to prevent information disclosure 
--------------------------------------

We can not avoid the information disclosure to full extent, but we can follow the best practices given by Portswigger to minimize the risk.

*   Make sure that everyone involved in producing the website is fully aware of what information is considered sensitive. Sometimes seemingly harmless information can be much more useful to an attacker than people realize. Highlighting these dangers can help make sure that sensitive information is handled more securely in general by your organization.
*   Audit any code for potential information disclosure as part of your QA or build processes. It should be relatively easy to automate some of the associated tasks, such as stripping developer comments.
*   Use generic error messages as much as possible. Don't provide attackers with clues about application behavior unnecessarily.
*   Double-check that any debugging or diagnostic features are disabled in the production environment.
*   Make sure you fully understand the configuration settings, and security implications, of any third-party technology that you implement. Take the time to investigate and disable any features and settings that you don't actually need.