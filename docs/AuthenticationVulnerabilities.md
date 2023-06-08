---
layout: default
title: Authentication Vulnerabilities
nav_order: 6
has_children: true
permalink: /cybersecurity/authentication_vulnerabilities
---

### What are Authentication Vulnerabilities?

Authentication vulnerabilities arises when the application having the flaws in process of verifying the identity of the users. Authentication vulnerabilities are easy to understand and there is more scope to verify these vulnerabilities. From security point of view these Authentication vulnerabilities can be most critical.

### What is the impact of Authentication vulnerabilities?

Authentication vulnerabilities potentially allows attackers to have direct access to sensitive data and functionality, they also expose additional attack surface for further exploits. They can eventually leads to account take over or if the account belongs to administrator, then system take over is also a possible. From there attacker can target dependent infrastructure which can contain sensitive data.

### Check list for Authentication flaws

*   Brute-forcing usernames
*   Enumerating usernames
*   Brute-forcing password
*   Flawed brute-force protection
*   Flaws in user rate limiting
*   Flawed two-factor verification logic
*   Brute-forcing 2FA verification codes
*   Resetting user password
*   Changing user password

> Note: detailed explanation will be posted in another write up. And please let me know if you want me to add anything for the checklist. 

### How to secure Authentication mechanism?

*   Don't count on users for security
*   Prevent User enumeration
*   Implement robust brute force protection
*   Thoroughly check verification logic
*   Implement proper multi-factor authentication