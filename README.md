# ubuntu-security-review-lab
Security review of an intentionally misconfigured Ubuntu VM, including investigation, remediation, and verification of security findings.
## Overview
This project documents a security review of an intentionally misconfigured Ubuntu virtual machine. The lab was designed to practice interpreting Linux configurations, identifying security concerns, applying remediation, and verifying that corrective actions were successful.
The environment was intentionally configured using setup commands provided with assistance from ChatGPT. I then analyzed the configurations and performed the investigation, remediation, and verification using Linux commands.
## Environment
- Ubuntu 24.04.4 LTS
- Oracle VirtualBox
- Windows 11 host
- Linux command line

  ## Key Findings
  ### 1. Unnecessary Apache2 Web Service
  Apache2 was running and configured to start automatically despite the system having no intended web hosting role. The service was stopped and disabled to reduce unnecessary attack surface.
  ### 2. Overly Permissive Employee Records File
  `/opt/company/employee_records.txt` was configured with `777` permissions, granting read, write, and execute permissions to owner, group, and others. Permissions were changed to `640` to apply least privilege.
  ### 3. Insecure Backup Credential Storage
  `/etc/company/backup.conf` contained a plaintext backup password and was configured with `644` permissions, allowing group and other users to read the file. Permissions were restricted to `600` , and the plaintext credential was identified as requiring removal from the configuration file and storage through a secure credential-management mechanism.

  ## Skills Demonstrated
  - Linux command line navigation and system investigation
  - Linux file permissions and ownership analysis
  - Principle of least privilege
  - Service management using `systemctl`
  - Identification of unnecessary services and attack surface
  - Identification and remediation of insecure file permissions
  - Identification of insecure credential storage
  - Security finding documentation and risk analysis
  - Remediation and post-remediation verification
  - Virtual machine lab setup and snapshot management
 
  ## Evidence
  ### Finding 1 - Unnecessary Apache2 Web Service
  Apache2 was identified running and enabled despite the VM having no intended web hosting role.
  
  <img width="1755" height="1280" alt="01-apache2-discovery" src="https://github.com/user-attachments/assets/873cb883-3b47-4849-a2b5-640f272980dd" />
  
  After remediation, `systemctl status apache2` confirmed the service was inactive and disabled.
  
  <img width="1762" height="1380" alt="01-apache2-remediation" src="https://github.com/user-attachments/assets/e13cec86-a421-4284-862b-eaa9a37d9212" />
  
### Finding 2 - Overly Permissive Employee Records File
The employee records file was identified with `777` permissions. Permissions were changed to `640` to restrict access according to least privilege.

<img width="1792" height="1370" alt="02-employee-records-remediation" src="https://github.com/user-attachments/assets/8ede632b-af1f-42f5-ad42-e3f50d083863" />

### Finding 3 - Insecure Backup Credential Storage
`backup.conf` was identified with `644` permissions and contained a plaintext credential. File permissions were restricted to `600`. The credential has been redacted from the evidence image.

<img width="1750" height="1405" alt="03-backup-password-remediation" src="https://github.com/user-attachments/assets/bfdb3d80-eeb3-4b92-8ba5-04a57e1e9c93" />

## Full Report
A detailed report of the lab, including the investigation process, security impact of each finding, remediation steps, and verification, is available here:

[Ubuntu Security Lab Report.pdf](https://github.com/user-attachments/files/32446637/Ubuntu.Security.Lab.Report.pdf)

## Takeaways
This project strengthened my understanding of Linux file permissions, service management, least privilege, attack surface reduction, and secure credential handling. It also provided hands on experience investigating system configurations, documenting security findings, applying remediation, and verifying corrective actions from the Linux command line.
The lab reinforced the importance of understanding why a configuration creates a security risk rather than simply identifying that a configuration is incorrect.



