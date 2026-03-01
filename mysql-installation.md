# MySQL Installation & Secure Setup Guide (Ubuntu 24.04)

This guide explains how to install MySQL on Ubuntu 24.04, secure it, create users, and connect safely from a local machine (Mac/Windows).

---

## 🚀 1. Install MySQL Server

### Update System
sudo apt update

### Install MySQL
sudo apt install mysql-server -y

### Start & Enable MySQL
sudo systemctl start mysql
sudo systemctl enable mysql

### Verify Status
sudo systemctl status mysql

You should see:
active (running)

---

## 🔐 2. Secure MySQL Installation

Run:
sudo mysql_secure_installation

Recommended:
- Validate password plugin → Yes
- Set root password → Yes
- Remove anonymous users → Yes
- Disallow root login remotely → Yes
- Remove test database → Yes
- Reload privilege tables → Yes

---

## 🔑 3. Configure Root Password

sudo mysql

ALTER USER 'root'@'localhost'
IDENTIFIED WITH mysql_native_password
BY 'YourStrongPassword123';

FLUSH PRIVILEGES;
EXIT;

Login using:
mysql -u root -p

---

## 👤 4. Create Application Database & User

mysql -u root -p

CREATE DATABASE myapp;

CREATE USER 'myappuser'@'localhost'
IDENTIFIED BY 'StrongPassword123';

GRANT ALL PRIVILEGES ON myapp.* TO 'myappuser'@'localhost';

FLUSH PRIVILEGES;
EXIT;

---

## 🌍 5. Secure Remote Access (SSH Tunnel)

ssh -L 3307:localhost:3306 root@YOUR_SERVER_IP

Use in client:
Host: 127.0.0.1
Port: 3307
Username: myappuser
Password: StrongPassword123

---

## 📦 Backup

mysqldump -u root -p myapp > myapp_backup.sql

Restore:
mysql -u root -p myapp < myapp_backup.sql
