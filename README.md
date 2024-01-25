# Ingryd SAMBA AND SERVER INSTALLATION PROJECT



# Linux Server Installation Documentation

Prepared By: Agbedeyi Segun Olatunde

## I. Introduction

### A. Purpose

The server installation serves various purposes depending on the intended use of an organization. Common scenarios include Web Hosting, File Hosting, Database Server, Application Server, and Development/Test Server. Each scenario influences the server's configuration, software installations, security measures, and maintenance tasks.

### B. Scope

For example, in the case of file hosting, the scope might include limitations on file types and sizes, access permissions, retention policies, and backup guidelines. Defining such scope helps maintain order, optimize storage resources, enhance security, and ensure efficient operation aligned with the server's intended purpose.

## II. Hardware and Software Requirements

### A. Hardware Specifications

- CPU: Intel Xeon E5-2690 v4 (14 cores, 2.60 GHz)
- RAM: 128GB DDR4 ECC RAM
- Storage: RAID-configured 1TB NVMe SSDs
- Network Interface: Dual Gigabit Ethernet ports (Intel I210)

### B. Software Requirements

- Linux Distribution: Ubuntu Server 20.04 LTS
- Additional Software: Apache HTTP Server, Samba File Transfer Server

## III. Installation Process

### A. Step-by-Step Installation

1. **Boot from ISO:** Insert the bootable installation media and restart the server.
2. **Language and Localization:** Select language and localization settings.
3. **Installation Type:** Choose the installation type, e.g., "Install Ubuntu Server."
4. **Network Configuration:** Connect to the network if required.
5. **Disk Partitioning:** Choose manual or guided partitioning.
6. **Installation Location and User Setup:** Specify installation destination and create initial user account.
7. **Software Selection:** Choose packages or server roles to install.
8. **Grub Boot Loader:** Install the boot loader to the appropriate disk.
9. **Finalization and Reboot:** Review settings, complete installation, and reboot.

### B. Configuration Options

1. **Disk Partitioning Choices:** Separate OS and data, allocate partitions accordingly.
2. **Network Settings:** Configure static IP address during installation.
3. **Additional Configuration:** Choose encryption options for heightened security.

## IV. Post-Installation Tasks

- **Update and Upgrade:** Run commands like `sudo apt update && sudo apt upgrade` for system updates.
- **User and Group Management:** Create and manage user accounts using commands like `sudo useradd` and `sudo groupadd`.
- **Security Measures:** Configure firewall rules (`sudo ufw enable`) and SSH access controls.

## V. System Monitoring and Maintenance

- **Logging and Monitoring:** Describe log rotation policies and use tools like `journalctl`.
- **Backup and Restore Procedures:** Detail backup strategies using tools like `rsync`.

## VI. Troubleshooting

- **Common Issues:** Address issues like dependency errors during software installation.
- **Logs and Diagnostics:** Explain how to access and interpret logs for troubleshooting.

# Samba Server Installation Documentation

## I. Introduction

### A. Purpose

Samba is a file-sharing platform across all OS (Windows, Linux/Unix, and MacOS), offering scalability, cross-platform compatibility, security, integration with Active Directory, performance, flexibility, and free configuration.

### B. Integration with Linux Server

Samba will integrate into the existing Linux server infrastructure for seamless file sharing capabilities.

## II. Installation and Configuration

### A. Samba Installation

```bash
sudo apt update
sudo apt install samba -y
sudo mkdir /share
sudo chmod 777 /share
sudo vim /etc/samba/smb.conf




Example Configuration:


[public-docs]
path = /share
public = yes
browseable = yes
guest ok = yes
read only = no
create mask = 0777
directory mask = 0777
comment = "Public file shared for Windows, Mac, and Linux users"


### testparm for permanent changes.

```bash
testparm 


### Start and enable services

```bash 
sudo systemctl start smbd.service
sudo systemctl start nmbd.service
sudo systemctl enable smbd.service
sudo systemctl enable nmbd.service


### User Authentication

User Accounts: Create Samba users with appropriate access privileges.

```bash
sudo useradd -s /sbin/nologin tech
sudo smbpasswd -a tech
sudo systemctl restart smbd.service

### Security and Access Controls

Firewall Configuration:

```bash
sudo ufw status
sudo ufw enable
sudo ufw allow 137/tcp
sudo ufw allow 138/tcp
sudo ufw allow 139/tcp
sudo ufw allow 445/tcp
sudo ufw allow 137/udp
sudo ufw allow 138/udp
sudo ufw status


### Testing and Verification

 Access Testing
Use smb://serveripaddress on Linux GUI.
Use `\\serverip for windows GUI


### Error Handling

Troubleshoot common issues like connection errors or permission mismatches.

### Maintenance and Upgrades

Software Updates: Update Samba through package managers for security and features.
Monitoring Samba: Use tools like sar or top for performance tracking.

### Troubleshooting

Logs and Diagnostics: Access and interpret Samba logs for troubleshooting.
Common Samba Issues: Provide solutions for common issues.

### Integration with Other Services

LDAP or Active Directory Integration: Document integration with LDAP or AD if applicable.

### Conclusion

In conclusion, the implementation of a Samba server offers a versatile solution for seamless file sharing. This guide covers key aspects, including installation, configuration, user management, security, testing, maintenance, and troubleshooting. A well-configured Samba server provides a stable foundation for file sharing in a small office environment, fostering collaboration and productivity.

Your suggestions and input are valuable to us! If you have any feedback, improvements, or additional insights to enhance this guide, please feel free to contribute. Open an issue, submit a pull request, or reach out to us. We appreciate the collaborative effort in making this documentation more comprehensive and user-friendly.

