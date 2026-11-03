# 🛡️ PortSwigger Lab: Remote Code Execution via Web Shell Upload

![PortSwigger](https://img.shields.io/badge/PortSwigger-Web%20Security%20Academy-orange?style=flat-square)
![Difficulty](https://img.shields.io/badge/Difficulty-Apprentice-green?style=flat-square)
![Category](https://img.shields.io/badge/Category-File%20Upload-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Solved-success?style=flat-square)

## 📌 Lab Overview

This lab demonstrates how an unrestricted file upload vulnerability can lead to Remote Code Execution (RCE).

The application allows users to upload files without properly validating them, making it possible to upload a PHP web shell and access sensitive information stored on the server.

- **Platform:** PortSwigger Web Security Academy
- **Lab:** Remote code execution via web shell upload
- **Category:** File Upload Vulnerabilities
- **Difficulty:** Apprentice
- **Tools:** Burp Suite, Firefox, Kali Linux

## 🎯 Objective

Upload a PHP web shell and retrieve the contents of:

`/home/carlos/secret`

Submit the retrieved secret through the lab's submission interface.

## ⚙️ Methodology

### 1. Access the Lab and Upload an Image

I accessed the lab and logged in using the provided credentials.

I uploaded a normal image as my profile avatar and captured the corresponding HTTP request using Burp Suite.

📸 **Screenshot 1 — Initial Image Upload**

<!-- Paste Screenshot Here -->

### 2. Filter the Request in Burp Suite

I navigated to Burp Suite's HTTP history and filtered the captured traffic to identify the image-related request.

I located the request associated with the uploaded avatar and sent it to Repeater for further inspection.

📸 **Screenshot 2 — Image Request in Burp Suite**

<!-- Paste Screenshot Here -->

### 3. Modify the Uploaded File

I changed the filename from the original image filename to:

`exploit.php`

I removed the existing text and replaced it with the following PHP code:

```php
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

This script reads the contents of the target file and returns them in the HTTP response.

📸 **Screenshot 3 — PHP Web Shell Preparation**

<!-- Paste Screenshot Here -->

### 4. Access the Uploaded PHP File

After uploading the modified file, I located the corresponding request in Burp Suite.

I sent the request to Repeater and modified the request path to access `exploit.php`.

📸 **Screenshot 4 — Request Sent to Repeater**

<!-- Paste Screenshot Here -->

### 5. Retrieve the Secret

I sent the modified request and inspected the server's response.

The response revealed the contents of `/home/carlos/secret`.

📸 **Screenshot 5 — Secret Retrieved from Server**

<!-- Paste Screenshot Here -->

### 6. Submit the Secret and Complete the Lab

I copied the retrieved secret into the lab's submission field.

The lab confirmed that the challenge was successfully solved.

📸 **Screenshot 6 — Lab Successfully Completed**

<!-- Paste Screenshot Here -->

## 🔍 Vulnerability Analysis

The vulnerability occurred because the application did not properly validate uploaded files.

By uploading a PHP script and accessing it through the application, I was able to retrieve sensitive information from the server.

**Potential Impact:**
- Unauthorized access to sensitive server files
- Exposure of confidential information
- Possible remote code execution, depending on server configuration

## 🛡️ Remediation

- Validate file extensions using an allowlist.
- Verify file content and MIME types on the server.
- Store uploaded files outside the web root.
- Prevent execution of uploaded files.
- Apply least-privilege permissions to the application.

## 📚 Key Takeaways

- File upload functionality can introduce serious security risks.
- Burp Suite helps analyze and modify HTTP requests.
- PHP web shells can expose sensitive server-side information.
- Proper file validation and storage controls are essential.

## ✅ Result

**Lab Status: Solved**

Successfully demonstrated how an unrestricted file upload vulnerability can expose sensitive server-side information.

🔗 [PortSwigger Lab — Remote Code Execution via Web Shell Upload](https://portswigger.net/web-security/file-upload/lab-file-upload-re)

