
# Arbitrary File Upload vulnerability from Sourcecodester Zipped Folder Manager App 1.0 (add-folder.php)

**Affected Project**: Zipped Folder Manager App 1.0

**Official Website**: https://www.sourcecodester.com/php/17291/zipped-folder-manager-app-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: add-folder.php

## Vulnerability Description

The Zipped Folder Manager App 1.0 has an Arbitrary File Upload vulnerability in its add-folder.php file. 

This vulnerability arises because the application does not thoroughly validate the contents of uploaded files, even though it checks that the file extension is .zip. Attackers can exploit this vulnerability to upload malicious files disguised as .zip files, leading to potential execution of arbitrary code on the server.

## Vulnerability Details and Analysis

1. **File Extension Check Only**:

- The add-folder.php script checks the file type based only on the file extension using the pathinfo() function:

```php
$fileType = strtolower(pathinfo($zipFile, PATHINFO_EXTENSION));
if ($fileType != 'zip') {
    echo "Only zip files are allowed.";
    exit;
}
```

- This check only verifies that the file has a .zip extension. It does not verify the actual contents or structure of the file. As a result, a .zip file could be crafted that contains malicious PHP code or scripts.

2. **Lack of Content Inspection**:

- There is no inspection or validation of the contents of the uploaded .zip file. Attackers can upload a .zip archive containing files like malicious.php. Once extracted or executed on the server, these files can run arbitrary PHP code.

3. **File Upload Location**:

- The file is directly moved to the target directory using the move_uploaded_file() function:

```php
if (move_uploaded_file($_FILES['folder']['tmp_name'], $zipFile)) {
    // Insert the folder information into the database
}
```

- This step implies that the file is accessible from the web server if the folders/ directory is within the web root. If the server is configured to execute PHP files in this directory, the attacker can access their malicious code directly via HTTP, resulting in Remote Code Execution (RCE).

4. **Database Interaction**:

- Once the file is uploaded, the script stores information about the file in the database:

```php
$stmt = $conn->prepare("INSERT INTO tbl_folder (zip_file, date_uploaded) VALUES (:zipFile, :dateUploaded)");
```

- While this part does not directly contribute to the vulnerability, it facilitates managing and organizing uploaded files, making it easier for attackers to track and access their malicious uploads.


## Demonstration

Belowis how Zipped Folder Manager App looks like:

![Screenshot from 2024-08-25 20-58-51](https://github.com/user-attachments/assets/c35a8333-714b-4a19-8055-b1a8c243251e)

User can add a zipped folder as such:

![Screenshot from 2024-08-25 20-57-27](https://github.com/user-attachments/assets/b9cb9c07-23ba-4d82-8b73-22faed872039)

Let's intercept the traffic when adding a zipped folder using Burp Suite:

![Screenshot from 2024-08-25 20-57-41](https://github.com/user-attachments/assets/2eda9bb9-101d-4474-b1bc-23f7ca235125)

Traffic could be modifed to contain any kind of codes since the app doesn't validate the zipped folder content. Here, I have a php code inserted as an example:

![Screenshot from 2024-08-25 20-58-26](https://github.com/user-attachments/assets/7de670a2-4f00-49b7-aea2-f4d756f53c63)

After sending the modified traffic, we can confirm the modified zipped folder is uploaded with no issue:

![Screenshot from 2024-08-25 20-58-51](https://github.com/user-attachments/assets/abaf9aa9-1ecf-4711-b30a-f1fb716f60d0)

When we download the zipped folder, we can see that zip file has an `.zip` extension but the content include the modified code untouched:

![Screenshot from 2024-08-25 22-35-22](https://github.com/user-attachments/assets/905506b6-1aaa-4f16-8dc0-097d9a29b474)
