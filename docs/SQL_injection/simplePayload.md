---
layout: default
title: My way of testing SQL Injection - Part 1 - Simple Payload verification
parent: SQL Injection
nav_order: 1
has_children: false
---

### Use of comments

Every SQL server may contain its own type of comments. But mostly we can try `--` 

we can use comments to trigger the error by avoiding the completion of full query. 

If we observe any anomaly then we can try any other methods to confirm whether it is vulnerable to SQL injection. Most of the times these simple payloads will be blocked by firewall. 

### Use of single quote

we can use single quote `'` to break the query. If we observe any anomaly then we can try any other methods to confirm whether it is vulnerable to SQL injection. Most of the times these simple payloads will be blocked by firewall. 

### Usage of logic conditions 

we can use simple OR or AND logics to confirm the SQL injection. For eg:  `‘OR 1=1`  or  `’OR 1=2` 

If we want to move forward and would like to know more about the data present, then we can use case statement. Here it will be different for different SQL servers. 

Let us consider the backend server is using Microsoft DB . if we send the following query as a input 

`SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN 1/0 ELSE NULL END` 

then if our condition was met then it will throw an error saying divided by zero and if we can observe any anomaly then we can confirm that backend SQL server may be MS SQL and create payloads to extract the desired data.

Most of the cases the response we get will be default error set by the server. In that case we can not get the verify the vulnerability. 

### Time delay based queries 

This will be most effective way to know whether the endpoint is vulnerable to SQL injection. 

Here we introduce the time delay in the query, where the data will be sent after certain time specified. With that we can confirm the endpoint is vulnerable to SQL injection. 

Every SQL server has its own way of implementing time delays. For eg: 

Let us consider the backend server is using MySQL server. If we use the query  `Select sleep(10)`  then we will get the response from the backend after 10 sec. 

Unless the response is not depends on the input we gave, this method will be very effective in finding the Vulnerable endpoint.

We can combine conditional based and time delay methods for finding the data we need.

We can use the [cheat sheet given by the portswigger](https://portswigger.net/web-security/sql-injection/cheat-sheet) to test the vulnerability.