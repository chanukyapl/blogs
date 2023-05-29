---
layout: default
title: My way of testing SQL Injection - Part 3 - Automation using SQLMAP
parent: SQL Injection
nav_order: 3
has_children: false
---

### What is SQLMAP?

sqlmap is an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers.

### Why SQLMAP?

 SQLMAP comes with a powerful detection engine, many niche features for the ultimate penetration tester, and a broad range of switches including database fingerprinting, over data fetching from the database, accessing the underlying file system, and executing commands on the operating system via out-of-band connections.

### Installation of SQLMAP

We can clone the repository by using the command

`git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap-dev`

### Help

we can change into sqlmap-dev directory and run the command `sqlmap.py -h` 

We can see the whole list of options

### Most useful options

*   \-p parameter → It is used to determine the parameter that we want to analyze 
*   \--current-user → We extract the username with which we interact with the database 
*   \--current-db → It extracts the name of the database in which we are 
*   \--dbs → It will give us the number of databases and will show us the name of each of them 
*   \-D name → It allows us to enter the selected database 
*   \--tables → It will show us the number of tables within a database and the names of each of the tables 
*   \-T name → It allows us to enter the selected table 
*   \--column → It will extract the number of the columns within a table and show us the name of each of them 
*   \-C name → It allows us to select the column 
*   \--dump → It allows us to extract content from the database 
*   \--dump-all → It extracts everything from the database |

### Most useful commands

Using the command `sqlmap.py -u <URL> --dbs` , we can test the GET method url that will fetch databases if the endpoint is vulnerable to SQL injection.

For POST method we can use the command `sqlmap.py -u "URL" --method POST --data " param1= 1 & param2 = 1" --dbs`  

### What is next?

*   After your reconnaissance, you will get the list of endpoints
*   You can use sqlmap to validate the endpoints