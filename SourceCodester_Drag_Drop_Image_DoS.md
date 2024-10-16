# DoS vulnerability was discovered from Sourcecodester Drag and Drop Image Upload without Refresh/Reload 1.0

**Affected Project**: Sourcecodester Drag and Drop Image Upload without Refresh/Reload 1.0

**Official Website**: https://www.sourcecodester.com/php/17656/drag-and-drop-image-upload-without-refreshreload-using-php-and-ajax-source-code.html

**Version**: 1.0

**Related Code file**: upload.php

## Vulnerability Description
### No Size Limit on File Upload
There’s no limit to the file size being uploaded. Large files could be uploaded, leading to a denial of service (DoS) attack by filling up disk space.

## Vulberable Code

The current implementation in your index.php file does not perform any file size validation on the uploaded files. Here's the section of the code that handles the file upload:

```php
uploadBtn.addEventListener('click', () => {
    if (selectedFile) {
        const formData = new FormData();
        formData.append('image', selectedFile);
        uploadImage(formData);
    }
});

function uploadImage(formData) {
    fetch('upload.php', {
        method: 'POST',
        body: formData
    })
    .then(response => response.json())
    .then(data => {
        if (data.status === 'success') {
            // Append the uploaded image to the gallery
            const img = document.createElement('img');
            img.src = 'uploads/' + data.file;  // Assuming the image is saved in 'uploads' directory
            gallery.appendChild(img);

            // Reset the preview and form
            previewContainer.style.display = 'none';
            previewImage.src = '';
            selectedFile = null;
            dropArea.style.display = 'block';
        } else {
            console.error(data.message);  // Log any error message from the server
        }
    })
    .catch(error => {
        console.error('Error uploading image:', error);
    });
}
```

In this code, the selectedFile is directly appended to the FormData object and then sent to the server (upload.php). No file size checks are done on the client or server side before uploading the file.

## Example Attack Scenario
1. The attacker uses a tool (such as Burp Suite) to upload a very large file (e.g., 10 GB or more), which the system accepts without any validation.
2. The server is forced to handle the large file, potentially exhausting its disk space or slowing down processing for other users.
3. If the attack is repeated multiple times, it can crash the server or degrade its performance, making it unavailable to legitimate users.

## Demonstration

Skipped. Just from reading the code it is very clear that this web application is vulnerable to DoS attack. 

I do not want to DoS my own Apache server so demonstation stage is skipped. 
