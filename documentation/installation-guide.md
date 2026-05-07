# osTicket Installation Guide

## Overview

This document outlines the installation and configuration process used to deploy the osTicket help desk environment on Ubuntu Server using Apache, MariaDB, and PHP.

---

# Environment Details

| Component | Version / Platform |
|---|---|
| Host OS | Windows 11 |
| Virtualization | Hyper-V |
| Guest OS | Ubuntu Server |
| Web Server | Apache2 |
| Database | MariaDB |
| Backend | PHP |
| Application | osTicket |

---

# Step 1 — Update Ubuntu Server

```bash
sudo apt update && sudo apt upgrade -y

sudo apt install apache2 -y
