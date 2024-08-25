
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
