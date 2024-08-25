# XSS vulnerability from Sourcecodester Daily Calories Monitoring Tool 1.0 (add-calorie.php)
## CVE-2024-8141

**Affected Project**: Daily Calories Monitoring Tool 1.0

**Official Website**: https://www.sourcecodester.com/php/17445/daily-calories-monitoring-tool-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: add-calorie.php

**Injection parameter**: calorie_date, calorie_name

## Vulnerability Description

The **calorie_date**, **calorie_name** parameters are vulnerable to the tested XSS payload: `<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`
.

Application does not properly sanitize or validate the input, this script could be executed in the user's browser, leading to an XSS attack.

## Analysis

```
catch (PDOException $e) {
    echo "Error:" . $e->getMessage();
}
```

The code catches a PDOException and directly echoes the error message using $e->getMessage(). If an attacker can manipulate the database interaction to cause an error that includes malicious script content, that content would be output directly to the user's browser.


## Demonstration
Below is how Daily Calorie Monitoring Tool looks like:

![Screenshot from 2024-08-23 21-19-50](https://github.com/user-attachments/assets/8610e539-9638-4924-824e-b60a014671b4)

We can add calorie as such:

![Screenshot from 2024-08-23 21-24-07](https://github.com/user-attachments/assets/76e9b026-e501-4fe6-9a0a-d85dafd3a434)

Intercept the adding calorie traffic using Burp Suite:

![Screenshot from 2024-08-23 21-24-16](https://github.com/user-attachments/assets/18291d0a-8d9b-4420-91b4-751c9b2bad37)

Let's inject xss payloads to the vulnerable parameters. Following payload is used: <IMG """><SCRIPT>alert("XSS")</SCRIPT>">

![Screenshot from 2024-08-23 21-25-49](https://github.com/user-attachments/assets/f42bde8a-fc42-473c-94bc-d4df7de39626)

Upon sending the modified traffic, we can confirm XSS vulnerability:

![Screenshot from 2024-08-23 21-26-00](https://github.com/user-attachments/assets/4290a8c1-0daa-4992-a675-d5753b2b115a)
