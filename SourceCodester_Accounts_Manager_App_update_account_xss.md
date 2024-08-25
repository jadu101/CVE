# XSS vulnerability from Sourcecodester Accounts Manager App 1.0 (update-account.php)
## CVE-2024-7948

**Affected Project**: Accounts Manager App 1.0

**Official Website**: [https://www.sourcecodester.com/php/17510/leads-manager-tool-using-php-and-mysql-source-code.html](https://www.sourcecodester.com/php/17482/accounts-manager-app-using-php-and-mysql-source-code.html)

**Version**: 1.0

**Related Code file**: update-account.php

**Injection parameter**: account_name, tbl_account_id, username, password, link

## Vulnerability Description

All parameters at update-account.php are vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage:
`<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the input, this script could be executed in the user's browser, leading to an XSS attack.

## Analysis

```php
echo "
<script>
    alert('Account Updated Successfully');
    window.location.href = 'http://localhost/account-manager-app/index.php';
</script>
";
```

If any of the values being displayed in the alert() function or used in the URL were derived from user input, and those inputs were not properly sanitized, a malicious user could inject JavaScript code into these fields.

## Demonstration
Below is how Account Manager App looks like:

![Screenshot from 2024-08-19 15-06-32](https://github.com/user-attachments/assets/37606ebb-3a9f-4d18-a310-7622d868593c)

We can update account as such:

![Screenshot from 2024-08-19 15-06-36](https://github.com/user-attachments/assets/c438d100-cb38-4fec-ae32-438a60066e94)

Fill in the forms with the following payload:

`<IMG """><SCRIPT>alert("XSS")</SCRIPT>">`

![Screenshot from 2024-08-19 15-19-51](https://github.com/user-attachments/assets/2d88c913-49c1-45e5-bb09-2e84b8e37085)

After saving changes, we can verify XSS vulnerability:

![Screenshot from 2024-08-19 15-12-29](https://github.com/user-attachments/assets/37585057-2799-487e-8ad8-e2b1cf9094fb)

