# osTicket Installation Guide

## Overview

This document outlines the installation and configuration process used to deploy the osTicket help desk environment within a Hyper-V virtual lab using Ubuntu Server, Apache2, MariaDB, PHP, and osTicket.

---

# Environment Details

| Component      | Version / Platform |
| -------------- | ------------------ |
| Host OS        | Windows 11         |
| Virtualization | Hyper-V            |
| Guest OS       | Ubuntu Server      |
| Web Server     | Apache2            |
| Database       | MariaDB            |
| Backend        | PHP                |
| Application    | osTicket           |

---

# Step 1 — Update Ubuntu Server

```bash
sudo apt update && sudo apt upgrade -y
```

Updated Ubuntu packages and system dependencies before beginning application installation.

---

# Step 2 — Install Apache Web Server

```bash
sudo apt install apache2 -y
```

Verified Apache installation and enabled web services.

Check Apache service status:

```bash
sudo systemctl status apache2
```

Restart Apache service:

```bash
sudo systemctl restart apache2
```

---

# Step 3 — Install MariaDB Database Server

```bash
sudo apt install mariadb-server -y
```

Verified MariaDB service status:

```bash
sudo systemctl status mariadb
```

Secured MariaDB installation:

```bash
sudo mysql_secure_installation
```

---

# Step 4 — Install PHP and Required Extensions

```bash
sudo apt install php php-mysql php-gd php-imap php-mbstring php-xml php-curl php-zip php-intl -y
```

Verified PHP installation:

```bash
php -v
```

---

# Step 5 — Create osTicket Database

Enter MariaDB:

```bash
sudo mysql
```

Create database and user:

```sql
CREATE DATABASE helpdesk;
CREATE USER 'osticketuser'@'localhost' IDENTIFIED BY 'StrongPassword';
GRANT ALL PRIVILEGES ON helpdesk.* TO 'osticketuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

---

# Step 6 — Download and Configure osTicket

Download osTicket:

```bash
wget https://github.com/osTicket/osTicket/releases/download/v1.18.1/osTicket-v1.18.1.zip
```

Extract installation files:

```bash
unzip osTicket-v1.18.1.zip
```

Move upload files to Apache web directory:

```bash
sudo cp -r upload /var/www/html/helpdesk
```

---

# Step 7 — Configure File Permissions

Set ownership permissions:

```bash
sudo chown -R www-data:www-data /var/www/html/helpdesk
```

Set directory permissions:

```bash
sudo chmod -R 755 /var/www/html/helpdesk
```

Rename sample configuration file:

```bash
sudo cp /var/www/html/helpdesk/include/ost-sampleconfig.php /var/www/html/helpdesk/include/ost-config.php
```

---

# Step 8 — Restart Apache and MariaDB

Restart services:

```bash
sudo systemctl restart apache2
sudo systemctl restart mariadb
```

Verify both services are running properly:

```bash
sudo systemctl status apache2
sudo systemctl status mariadb
```

---

# Step 9 — Complete Web-Based Installation

Access osTicket from browser:

```text
http://SERVER-IP/helpdesk
```

Completed:

* Admin account setup
* Database configuration
* Initial osTicket environment configuration

---

# Step 10 — Secure Installation

Remove setup directory after installation:

```bash
sudo rm -rf /var/www/html/helpdesk/setup
```

Set osTicket configuration file to read-only:

```bash
sudo chmod 644 /var/www/html/helpdesk/include/ost-config.php
```

---

# Validation and Testing

Verified:

* Apache web services
* MariaDB database connectivity
* osTicket login portal accessibility
* Ticket creation and routing
* Department and agent functionality
* SLA plan functionality
* Ticket lifecycle workflows

---

# Skills Demonstrated

* Linux server administration
* Apache web server configuration
* MariaDB database management
* PHP dependency configuration
* Linux file permission management
* Hyper-V virtualization
* Help desk system deployment
* Technical troubleshooting
* IT infrastructure documentation
