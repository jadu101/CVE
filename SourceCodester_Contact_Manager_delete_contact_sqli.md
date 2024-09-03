# SQL Injection vulnerability was discovered from Sourcecodester Contact Manager with Export to VCF (delete-contact.php)
## CVE-2024-8380

> A vulnerability was found in SourceCodester Contact Manager with Export to VCF 1.0. It has been rated as critical. This issue affects some unknown processing of the file /endpoint/delete-account.php of the component Delete Contact Handler. The manipulation of the argument contact leads to sql injection. The attack may be initiated remotely. The exploit has been disclosed to the public and may be used.

**Affected Project**: Sourcecodester Contact Manager with Export to VCF 1.0

**Official Website**: https://www.sourcecodester.com/php/17556/contact-manager-export-vcf-using-php-and-mysql-source-code.html

**Version**: `1.0`

**Related Code file**: `delete-contact.php`

**Injection parameter**: `contact`

## Analysis

```sql
$query = "DELETE FROM tbl_contact WHERE tbl_contact_id = '$contact'";
```

The `contact` parameter from the GET request is directly used in the SQL query without any validation or escaping, making the code susceptible to SQL injection attacks.

## Demonstration

Below is Contact Manager with Export to VCF app:

![image](https://github.com/user-attachments/assets/104310c0-3db5-4119-a77b-d7dd98e15372)

We can delete contact as such:

![Screenshot from 2024-09-02 14-16-28](https://github.com/user-attachments/assets/703f8f55-5ad2-45a0-bdcf-4ad706843825)

Let's intercept the delete contact traffic using Burp Suite:

![Screenshot from 2024-09-02 14-17-12](https://github.com/user-attachments/assets/7dca2c6d-6bf9-4f60-b2c9-e6aa69a12327)

Save the traffic to a file and run sqlmap against it:

![image](https://github.com/user-attachments/assets/c1b91dad-7232-4bcb-8cc0-6ddc73bd186d)

We can see that parameter `contact` is vulnerable:

![Screenshot from 2024-09-02 14-17-38](https://github.com/user-attachments/assets/00f486ff-fe18-45f9-8807-6dcb104136f0)




