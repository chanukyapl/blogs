---
layout: default
title: Authorization Vulnerabilities
nav_order: 7
has_children: true
permalink: /cybersecurity/authorization_vulnerabilities
---

### What are Authorization Vulnerabilities?

Authorization vulnerabilities are the vulnerabilities which will arise when the implementation of access control having the flaws. From security point of view these Authorization vulnerabilities can be most critical.

### What is the impact of Authorization vulnerabilities?

Authorization vulnerabilities potentially allows attackers to have direct access to sensitive data and functionality, they also expose additional attack surface for further exploits. They can eventually leads to account take over or if the account belongs to administrator, then system take over is also possible. From there, the attacker can target dependent infrastructure which can contain sensitive data.

### Types of Authorization vulnerabilities

**Vertical Access Control Vulnerabilities**

Vertical Access Control Vulnerabilities are the vulnerabilities arises from the flaw induced by the validation of process to check the type of user  
With vertical access controls, different types of users have access to different application functions.   
For example, an administrator might be able to modify or delete any user's account, while an ordinary user has no access to these actions. Vertical access controls can be more fine-grained implementations of security models designed to enforce business policies such as separation of duties and least privilege.

**Horizontal Access Control**

Horizontal Access Control Vulnerabilities are the vulnerabilities arises from the flaw induced by the validation of the user session only for whom the resource must be available.  
With horizontal access controls, different users have access to a subset of resources of the same type. For example, a banking application will allow a user to view transactions and make payments from their own accounts, but not the accounts of any other user.

  
**Context-dependent Access Control**  
Context-dependent access controls restrict access to functionality and resources based upon the state of the application or the user's interaction with it.

Context-dependent access controls prevent a user performing actions in the wrong order. For example, a retail website might prevent users from modifying the contents of their shopping cart after they have made payment.

>   
> Note: The detailed explanation will be provided in the new write up.

### How to prevent access control vulnerabilities

  
Access control vulnerabilities can generally be prevented by taking a defense-in-depth approach and applying the following principles:

*   Never rely on obfuscation alone for access control.
*   Unless a resource is intended to be publicly accessible, deny access by default.
*   Wherever possible, use a single application-wide mechanism for enforcing access controls.
*   At the code level, make it mandatory for developers to declare the access that is allowed for each resource, and deny access by default.
*   Thoroughly audit and test access controls to ensure they are working as designed.