# Linux Users, Groups & Permissions Lab

## Objective

Build practical Linux administration skills by creating users and groups, configuring directory ownership and permissions, and testing access controls in an Ubuntu Server environment.

This lab focuses on concepts that are foundational to Linux system administration, cloud infrastructure, and security.

## Environment

- OS: Ubuntu Server 24.04 LTS
- Hostname: tech-cloud
- Shell: Bash
- Access: SSH from Windows PowerShell
- Virtualization: VirtualBox
- Repository: Court-Cloud/linux-lab-notes

## Environment

- OS: Ubuntu Server 24.04 LTS
- Hostname: tech-cloud
- Shell: Bash
- Access: SSH from Windows PowerShell
- Virtualization: VirtualBox
- Repository: Court-Cloud/linux-lab-notes

## Skills Demonstrated

- Linux user identification and account management
- User and group administration
- UID and GID concepts
- File and directory ownership
- Linux permission management
- Shared group directories
- SGID directory inheritance
- Least-privilege access control
- Permission testing and verification

## Lab Tasks

### 1. Verify Current User

Used whoami and id to identify the current Linux account and its associated UID, GID, and groups.

Current administrative user: courtttt

### 2. Verify Administrative Privileges

Checked the commands available through sudo.

The account has administrative privileges on the lab server.

### 3. Create a Test User

Created a dedicated test account for permission testing.

Command used: sudo
### 4. Create a Shared Group

Created a group representing a shared application team.

Command used: sudo
### 5. Add the User to the Shared Group

Added labuser to the cloudteam group.

Commands used: `sudo usermod -aG cloudteam labuser` and `groups labuser`
### 6. Create a Shared Application Directory

Created '/opt/cloud-app' for resources shared by the application team. 

Commands used: 
- 'sudo mkdir /opt/cloud-app'
- 'sudo chgrp cloudteam /opt/cloud-app'
- 'sudo chmod 775 /opt/cloud-app' 

The directory is owned by 'root' and assigned to the 'cloudteam' group. 
### 7. Enable SGID Directory Inheritance

Enabled the SGID bit on the shared application directory so that new files inherit the 'cloudteam' group ownership. 

Command used: 'sudo chmod 2775 /opt/cloud-app'

Verified the directory permissions with 'ls -ld /opt/cloud-app', which showed 'drwxrwsr-x'.
### 8. Verify Group Inheritance

Created a test file as 'labuser' inside '/opt/cloud-app' and confirmed that it inherited the 'cloudteam' group. 

Command used: 'sudo -u labuser touch /opt/cloud-app/shared-test.txt'
### 9. Test Authorized Write Access

Tested that 'labuser' could write to the shared file. 

Command used: 'sudo -u labuser bash -c 'echo "Cloud team access test" > /opt/cloud-app/shared-test.txt'

Verified the contents with 'cat /opt/cloud-app/shared-test.txt'. 
### 10. Restrict File Permissions

Set the shared file permissions to allow read and write access for the owner and group, while denying access to others. 

Command used: 'sudo chmod 660 /opt/cloud-app/shared-test.txt' 

Verified permissions: '-rw-rw----'. 
### 11. Test Unauthorized Access 

Tested access as the 'nobody' user. 

Command used: 'sudo -u nobody cat /opt/cloud-app/shared-test.txt'

Result: 'Permission denied'.
## Security Concepts Demonstrated

### Least Privilege

Access was restricted to the users who required it rather than allowing unrestricted access. 

### Group-Based Access Control

The 'cloudteam' group provides a scalable way to manage access for multiple users without assigning permissions individually. 

### SGID Directory

The SGID bit ensures that files created inside the shared directory inherit the intended group ownership, supporting consistend collaboration between authorized users. 

### Permission Verification

Access controls were tested directly rather than assumed to be working based only on configuration commands. 
## Practical Cloud Engineering Application

These Linux administration concepts are directly applicable to cloud environments where engineers manage:

- Linux virtual machines
- Application directories
- Service accounts
- Shared resources
- File permissions
- Team-based access
- Security boundaries
- Least-privilege configurations

Understanding Linux permissions provides a foundation for later cloud security topics such as identity and access management (IAM), secure server configuration, and access control. 
## Lab Status

**Completed**

This lab was performed on a self-managed Ubuntu Server virtual machine and documented as part of a cloud engineering home lab portfolio.  
