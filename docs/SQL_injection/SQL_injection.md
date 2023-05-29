---
layout: default
title: sql_injection
nav_order: 3
has_children: true
permalink: /cybersecurity/sql_injection
---

# SQL Injection

### What is SQL Injection

SQL injection is a web security vulnerability that allows a person to post the query that in turn use the database without proper validation and retrieves the data that can be sensitive. 

### Why is SQL Injection dangerous?

In most of the cases, a person can modify or delete the data, causing persistent changes to the application's content or behavior. In some cases, we can escalate this SQL injection attack to compromise the underlying SQL server or other back-end infrastructure, which were dependent or perform a denial-of-service attack.

### Ways to exploit the SQL injection

*   [Retrieving hidden data](https://portswigger.net/web-security/sql-injection#retrieving-hidden-data), where you can modify a SQL query to return additional results.
*   [Subverting application logic](https://portswigger.net/web-security/sql-injection#subverting-application-logic), where you can change a query to interfere with the application's logic.
*   [UNION attacks](https://portswigger.net/web-security/sql-injection/union-attacks), where you can retrieve data from different database tables.
    *   ' UNION SELECT username, password FROM users--
    *   To know the number of columns
        *   ' UNION SELECT NULL,NULL,NULL--
        *   ' ORDER BY 3--
    *   For a `UNION` query to work, two key requirements must be met:
        *   The individual queries must return the same number of columns.
        *   The data types in each column must be compatible between the individual queries.
*   [Examining the database](https://portswigger.net/web-security/sql-injection/examining-the-database), where you can extract information about the version and structure of the database.
    *   SELECT \* FROM information\_schema.tables
*   [Blind SQL injection](https://portswigger.net/web-security/sql-injection/blind), where the results of a query you control are not returned in the application's responses.
    *   You can change the logic of the query to trigger a detectable difference in the application's response depending on the truth of a single condition. This might involve injecting a new condition into some Boolean logic, or conditionally triggering an error such as a divide-by-zero.
    *   You can conditionally trigger a time delay in the processing of the query, allowing you to infer the truth of the condition based on the time that the application takes to respond.
    *   You can trigger an out-of-band network interaction, using [OAST](https://portswigger.net/burp/application-security-testing/oast) techniques. This technique is extremely powerful and works in situations where the other techniques do not. Often, you can directly exfiltrate data via the out-of-band channel, for example by placing the data into a DNS lookup for a domain that you control.

### My way of testing an SQL injection

*   Simple payloads
*   OAST testing
*   Automation

Best effective way of exploiting SQL injection is OAST testing(Out of band Application Security Testing)

OAST testing

*   Gather the Generate set of payloads as per the requirement to check as OAST Testing
*   Test them 
*   check if there is any kind of WAF that is blocking our payload
    *   Create a set of payloads to check, what kind of payloads getting blocked as per the database 
    *   If possible create a set of payloads to bypass the WAF
*   Get the database information 
*   Extract the data and look for the sensitive information

### How to prevent SQL injection?

First important thing is to sanitize the input sent by user. Yet we can not be sure that SQL Injection can not happen.

So we have to use parameterized queries. Parameterized queries helps to pass the input sent by the user into the query as a string while executing the query.
