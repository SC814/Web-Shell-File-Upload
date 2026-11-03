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

<img width="763" height="232" alt="Initial image upload" src="https://github.com/user-attachments/assets/3da7a30b-d1c0-44fb-8ca6-5f6b42017a2e" />


### 2. Filter the Request in Burp Suite

I navigated to Burp Suite's HTTP history and filtered the captured traffic to identify the image-related request.

I located the request associated with the uploaded avatar and sent it to Repeater for further inspection.

📸 **Screenshot 2 — Image Request in Burp Suite**

<img width="672" height="540" alt="Image request in burpsuite" src="https://github.com/user-attachments/assets/af2bf3f3-4c1d-4e96-82ac-0c9f0e27b99e" />


### 3. Modify the Uploaded File

I changed the filename from the original image filename to:

`exploit.php`

I removed the existing text and replaced it with the following PHP code:

```php
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

This script reads the contents of the target file and returns them in the HTTP response.

📸 **Screenshot 3 — PHP Web Shell Preparation**

<img width="1287" height="650" alt="Shell preparation" src="https://github.com/user-attachments/assets/424aa3dc-f8c5-42e8-a740-e9165a6a39fd" />


### 4. Access the Uploaded PHP File

After uploading the modified file, I located the corresponding request in Burp Suite.

I sent the request to Repeater and modified the request path to access `exploit.php`.

📸 **Screenshot 4 — Request Sent to Repeater**

<img width="1028" height="757" alt="File sent to repeater" src="https://github.com/user-attachments/assets/dd751b8a-9ea1-437c-979c-2d46c57ddbb0" />


### 5. Retrieve the Secret

I sent the modified request and inspected the server's response.

The response revealed the contents of `/home/carlos/secret`.

📸 **Screenshot 5 — Secret Retrieved from Server**

<img width="1081" height="553" alt="code retrieved from server" src="https://github.com/user-attachments/assets/0c0bfa93-44e8-4159-990c-9e441fccaf5d" />


### 6. Submit the Secret and Complete the Lab

I copied the retrieved secret into the lab's submission field.

The lab confirmed that the challenge was successfully solved.

📸 **Screenshot 6 — Lab Successfully Completed**

<img width="757" height="381" alt="password found" src="https://github.com/user-attachments/assets/dd5838ed-2b6d-49d1-9770-f807cd270657" />
<img width="1600" height="852" alt="completed successfully" src="https://github.com/user-attachments/assets/855befb9-c190-443e-ba55-b5199c654976" />


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

