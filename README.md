# WebAppPenetrationTesting
Running A Penetration Test on JuiceShop using BurpSuite 

# Web Application Penetration Test on OWASP Juice Shop

## Overview
This project documents a penetration test performed on the OWASP Juice Shop, a deliberately insecure web application designed for security training and testing. The aim of this assessment was to identify and exploit vulnerabilities within the application to demonstrate real-world penetration testing techniques.

## Table of Contents
- [Introduction](#introduction)
- [Methodology](#methodology)
- [Tools Used](#tools-used)
- [Findings](#findings)
- [Conclusion](#conclusion)

## Introduction
OWASP Juice Shop is a platform that simulates real-world vulnerabilities for educational purposes. It encompasses a wide range of security flaws, making it an ideal environment for practicing web application security assessments.

-
![Screenshot 2024-11-03 013302](https://github.com/user-attachments/assets/566c6f9c-0b4b-458f-be86-f4a95d1a2bad)

## Methodology
The penetration testing process was structured as follows:

1. **Reconnaissance**: Information gathering to understand the application’s architecture.
2. **Scanning**: Analyzing HTTP requests and responses to identify potential vulnerabilities.
3. **Exploitation**: Attempting to exploit identified vulnerabilities to gain unauthorized access.
4. **Reporting**: Documenting findings and providing recommendations for mitigation.

## Tools Used
-- **Burp Suite**: For intercepting and analyzing HTTP requests.

## Findings
### 1. Misconfigured CORS
- **Description**: The application allowed any origin due to the wildcard (`*`) in the CORS header.
- **Impact**: Low; can lead to potential Cross-Origin Resource Sharing issues.
  

  -![Screenshot 2024-11-03 014811](https://github.com/user-attachments/assets/30de98ee-9ff6-410e-9898-48cd7f6e6380)


### 2. SQL Injection
- **Description**: The login page was vulnerable to SQL injection, allowing access to the admin account.
- ![Screenshot 2024-11-03 013705](https://github.com/user-attachments/assets/fd0d72b2-5a5d-442c-85e2-a5d2760eb503)

- Attempted SQL injection brute force that failed using a common worslist from Github

- ![Screenshot 2024-11-03 013526](https://github.com/user-attachments/assets/edfa3451-2d71-4d80-9fd8-a03285fd4b85)


  
- **Exploit**: By using a payload like `' OR 1=1 --`, unauthorized access was achieved, the request was recorded in BurpSuite, and we were able to obtain the username and attempted the brute force again.

- ![Screenshot 2024-11-03 023954](https://github.com/user-attachments/assets/26ff2a85-6e55-437e-8fbe-98a4737ac066)

- ![Screenshot 2024-11-03 024003](https://github.com/user-attachments/assets/9935c664-4009-4221-b38e-39adb82af0e0)


- After using the SqL injection on the website, we retried the SQL injection brute force again inside Burpsuite and were able to get both the username and password

- ![Screenshot 2024-11-03 015642](https://github.com/user-attachments/assets/9799acd2-3bf5-4a4a-80b6-88a6477a308f)
 




- Eventually after brute force failed, attemepted the SQL injection on login page 
- **Impact**: High; potential for unauthorized access to sensitive data.

### 3. Sensitive Data Exposure
- **Description**: Credentials were transmitted over HTTP in plain text, compromising security.
- **Impact**: High; could lead to interception of sensitive information by attackers.

### 4. Reflected XSS
- **Description**: The search functionality was vulnerable to reflected XSS attacks.
- **Exploit**: Injecting a payload such as `<script>alert(1)</script>` executed JavaScript in the browser.

- ![Screenshot 2024-11-03 020322](https://github.com/user-attachments/assets/f4d9f51d-c81b-4f2b-9f6e-faa3d12fabf7)

- ![Screenshot 2024-11-03 020538](https://github.com/user-attachments/assets/5d950ac7-056f-4ee0-8ae4-136a41c4bb0a)

-

- ![Screenshot 2024-11-03 020026](https://github.com/user-attachments/assets/3bf491bc-3cdd-4123-8a31-9cc0ae5442ac)

- **Impact**: Medium; could lead to session hijacking.

## Conclusion
The OWASP Juice Shop contains multiple vulnerabilities that can be exploited. This penetration test provided valuable insights into the security weaknesses of web applications and underscored the importance of implementing robust security measures.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

