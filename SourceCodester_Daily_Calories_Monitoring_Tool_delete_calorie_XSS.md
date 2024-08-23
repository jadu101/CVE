
# XSS vulnerability from Sourcecodester Daily Calories Monitoring Tool 1.0 (delete-calorie.php)

**Affected Project**: Daily Calories Monitoring Tool 1.0

**Official Website**: https://www.sourcecodester.com/php/17445/daily-calories-monitoring-tool-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: delete-calorie.php

**Injection parameter**: calorie
## Vulnerability Description

The **calorie** parameter is vulnerable to the tested XSS payload: `<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`
.

Application does not properly sanitize or validate the input, this script could be executed in the user's browser, leading to an XSS attack.




## Demonstration
Below is how Daily Calorie Monitoring Tool looks like:

![Screenshot from 2024-08-23 21-19-50](https://github.com/user-attachments/assets/8610e539-9638-4924-824e-b60a014671b4)

We can delete calorie as such:

![Screenshot from 2024-08-23 22-21-08](https://github.com/user-attachments/assets/449ce4b1-60fd-471b-a8c1-28fa1a328dbe)

Intercept the deleting calorie traffic using Burp Suite, `calorie` parameter is vulnerable to XSS:

![Screenshot from 2024-08-23 22-21-20](https://github.com/user-attachments/assets/0f54bc3b-4b07-457b-bd5a-63435a1ce6aa)

Let's inject xss payloads to the vulnerable parameters. Following payload is used: <IMG """><SCRIPT>alert("XSS")</SCRIPT>">

![Screenshot from 2024-08-23 22-21-50](https://github.com/user-attachments/assets/4214fca8-3681-492c-8e34-2aff16c31379)

Upon sending the modified traffic, we can confirm XSS vulnerability:

![Screenshot from 2024-08-23 21-26-00](https://github.com/user-attachments/assets/9686342f-222a-4547-b843-254b8026dc73)
