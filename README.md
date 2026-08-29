# osTicket: Prerequisites and Installation

## Project Overview

In this lab, I installed and deployed **osTicket v1.15.8** on a Windows 10 virtual machine hosted in Microsoft Azure. I configured IIS as the web server, installed PHP and MySQL, created the osTicket database, completed the browser-based installation, and secured the configuration files.

## Technologies Used

- Microsoft Azure
- Windows 10 Virtual Machine
- Remote Desktop Protocol (RDP)
- osTicket v1.15.8
- Internet Information Services (IIS)
- Common Gateway Interface (CGI)
- PHP 7.3.8
- PHP Manager for IIS
- MySQL 5.5.62
- HeidiSQL
- IIS URL Rewrite Module
- Microsoft Visual C++ Redistributable

## Installation Process

### 1. Create and Connect to the Azure Virtual Machine

I created a Windows 10 virtual machine in Microsoft Azure with four virtual CPUs. After deployment, I connected to the virtual machine using Remote Desktop.

> **Security Note:** Login credentials and passwords are intentionally excluded from this documentation. Credentials should be stored securely in a password manager and never published in a GitHub repository.

### 2. Download the Installation Files

Inside the virtual machine, I downloaded and extracted the osTicket installation package. The package contained osTicket and the supporting software required to host the application.

### 3. Enable IIS and CGI

I enabled **Internet Information Services (IIS)** to host the osTicket website.

Under Windows Features, I enabled:

```text
World Wide Web Services
└── Application Development Features
    └── CGI
```

CGI allows IIS to communicate with the PHP interpreter and process PHP-based webpages.

### 4. Install the Required Dependencies

I installed the following supporting components:

- PHP Manager for IIS
- IIS URL Rewrite Module
- PHP 7.3.8
- Microsoft Visual C++ Redistributable
- MySQL 5.5.62
- HeidiSQL

<img width="3024" height="1885" alt="image" src="https://github.com/user-attachments/assets/36fae32a-8d57-4716-b7cf-a59e97ad8bdf" />


I created the following directory for PHP:

```text
C:\PHP
```

I then extracted the PHP files into that directory.


### 5. Configure MySQL

I installed MySQL using its standard configuration. MySQL provides the database used to store osTicket information, including:

- Users
- Agents
- Tickets
- Departments
- SLA plans
- Help topics
- Ticket history

The MySQL credentials used during the lab are not included in this documentation.

### 6. Register PHP with IIS

I opened IIS Manager with administrator privileges and registered PHP using the executable located at:

```text
C:\PHP\php-cgi.exe
```

I then stopped and restarted IIS so the configuration changes could take effect.

### 7. Deploy osTicket

I extracted the osTicket v1.15.8 package and copied its `upload` folder into:

```text
C:\inetpub\wwwroot
```

I renamed the folder from:

```text
upload
```

to:

```text
osTicket
```

The resulting installation directory was:

```text
C:\inetpub\wwwroot\osTicket
```

I restarted IIS and opened the osTicket website through the IIS **Browse** option on port 80.

### 8. Enable the Required PHP Extensions

The osTicket prerequisite check showed that some PHP extensions needed to be enabled. Using PHP Manager in IIS, I enabled:

- `php_imap.dll`
- `php_intl.dll`
- `php_opcache.dll`

I refreshed the osTicket installation page to confirm that the required and recommended dependencies were available.

![osTicket prerequisite verification]
<img width="2244" height="1401" alt="40EBAF69-6A33-488A-85E2-974ABC5B79BF_1_102_a" src="https://github.com/user-attachments/assets/be17e1d2-b5bf-4eb6-8e56-ced76f89871e" />

### 9. Create the osTicket Configuration File

I located the sample configuration file:

```text
C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
```

I renamed it to:

```text
ost-config.php
```

The completed file was located at:

```text
C:\inetpub\wwwroot\osTicket\include\ost-config.php
```

I temporarily adjusted the file permissions so the installer could write the required configuration settings.

### 10. Create the osTicket Database

I opened HeidiSQL and established a local connection to the MySQL server. I then created a database named:

```text
osTicket
```

This database was selected during the browser-based installation.

### 11. Complete the Browser Installation

In the osTicket installer, I configured:

- The help desk name
- The default support email address
- The administrator account
- The MySQL database name
- The MySQL username and password

I selected **Install Now** and verified that the installation completed successfully.

### 12. Verify the Installation

I confirmed access to both sides of the help desk system.

**Staff and administrator portal:**

```text
http://localhost/osTicket/scp/login.php
```

**End-user support portal:**

```text
http://localhost/osTicket/
```

![osTicket Agent Control Panel](<img width="2200" height="1429" alt="40EBAF69-6A33-488A-85E2-974ABC5B79BF_1_102_o" src="https://github.com/user-attachments/assets/e4cf7cfe-13f5-487e-bccf-9cac0ae2bcf5" />
)

## Post-Installation Security

After verifying the installation, I completed the recommended security cleanup:

- Deleted the osTicket `setup` directory.
- Removed unnecessary write permissions from `ost-config.php`.
- Changed `ost-config.php` to read-only.
- Kept usernames and passwords out of the public documentation.

Deleted directory:

```text
C:\inetpub\wwwroot\osTicket\setup
```

Secured configuration file:

```text
C:\inetpub\wwwroot\osTicket\include\ost-config.php
```

## Challenges and Troubleshooting

During installation, some PHP extensions were initially disabled. I resolved this by opening PHP Manager in IIS, enabling the required extensions, restarting IIS, and refreshing the osTicket prerequisite page.

I also temporarily changed the permissions for `ost-config.php` so the installer could write to it. Once the installation was complete, I removed the elevated permissions and returned the file to a read-only state.

## Skills Demonstrated

- Provisioning an Azure virtual machine
- Connecting to Windows through RDP
- Installing and configuring IIS
- Enabling Windows features
- Installing PHP and registering it with IIS
- Enabling PHP extensions
- Installing and configuring MySQL
- Creating and connecting to a database with HeidiSQL
- Deploying a PHP web application
- Managing Windows file permissions
- Verifying application prerequisites
- Applying post-installation security controls
- Troubleshooting web-server dependencies

## Outcome

I successfully installed and deployed a functional osTicket help desk environment on a Windows virtual machine. The completed system provided an administrator and agent portal for managing support tickets and an end-user portal for submitting and tracking incidents.
