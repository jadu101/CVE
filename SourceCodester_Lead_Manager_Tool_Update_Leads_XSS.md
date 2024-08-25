# XSS vulnerability from Sourcecodester Lead Manager Tool 1.0 (update-leads.php)
## CVE-2024-7942

**Affected Project**: Lead Manager Tool 1.0

**Official Website**: https://www.sourcecodester.com/php/17510/leads-manager-tool-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: update-leads.php

**Injection parameter**: phone_number

## Vulnerability Description

The **phone_number** parameter is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage:
`<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the **phone_number** input, this script could be executed in the user's browser, leading to an XSS attack.

## Analysis

```
echo "
    <script>
        alert('Leads Update Successfully');
        window.location.href = 'http://localhost/leads-manager-tool/';
    </script>
";
```

In this block, user input is not directly used, but if there were any dynamic content being output within this <script> tag based on user input, it would be a point of XSS.



## Demonstration
Below is how Leads Manager Tool looks like:

![image](https://github.com/user-attachments/assets/7d5891c8-0e0d-478f-b8fc-c3e7bef760b9)

We can update leads as such:

![Screenshot from 2024-08-18 11-34-02](https://github.com/user-attachments/assets/a6dbf8d5-55a8-4670-bbca-fc32230efc00)

Intercept the update(leads-update.php) traffic using Burp Suite and inject the following payload:

`%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`

![Screenshot from 2024-08-18 11-35-15](https://github.com/user-attachments/assets/ba9c9af1-d917-461d-b950-56f26a48a3af)

Payload used above is HTML encoded and decodes as `<IMG """><SCRIPT>alert("XSS")</SCRIPT>">`

Upon sending the modifying traffic containing XSS payload, we can verify the vulnerability:

![Screenshot from 2024-08-18 11-23-21](https://github.com/user-attachments/assets/86746dcb-c840-4fb0-be31-6a1ff775ed86)


