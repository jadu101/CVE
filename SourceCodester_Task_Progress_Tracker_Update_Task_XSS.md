
# XSS vulnerability from Sourcecodester Task Progress Manager 1.0 (update-task.php)

**Affected Project**: Task Progress Manager 1.0

**Official Website**: https://www.sourcecodester.com/php/17479/task-progress-tracker-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: update-task.php

**Injection parameter**: task_name

## Vulnerability Description

The **task_name** parameter is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage:
`<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the **task_name** input, this script could be executed in the user's browser, leading to an XSS attack.

## Analysis

```
echo "
                <script>
                    alert('Task Updated Successfully');
                    window.location.href = 'http://localhost/task-progress-tracker/';
                </script>
            ";
```

In this block, user input is not directly used, but if there were any dynamic content being output within this <script> tag based on user input, it would be a point of XSS.



## Demonstration
Below is how Task Progress Tracker looks like:

![Screenshot from 2024-08-23 21-11-21](https://github.com/user-attachments/assets/3304462d-e531-4924-9ac1-70471b4b1685)

We can add task as such:

![Screenshot from 2024-08-23 21-02-59](https://github.com/user-attachments/assets/4f16b8d4-a714-48ac-a784-634d09ebe419)

Now let's try updating the task.

Inject the following payload to task_name form:

`<IMG """><SCRIPT>alert("XSS")</SCRIPT>">`

![Screenshot from 2024-08-23 21-07-30](https://github.com/user-attachments/assets/2e4bf3c1-ec0a-4ad9-a8ed-612b142b2b76)

Upon sending the traffic containing XSS payload, we can verify the vulnerability:

![Screenshot from 2024-08-23 21-07-47](https://github.com/user-attachments/assets/98afb289-e8ee-411c-ad8f-c154cf9f0f40)

