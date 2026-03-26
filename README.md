# 📘 Linux Project — Deploy 3‑Tier PHP Application (WSL / Ubuntu)

# 🎯 Project Goal

Deploy a **3‑Tier PHP Application** on **Ubuntu / WSL** while learning:

* Linux Commands
* Apache Web Server
* PHP Configuration
* MariaDB Database
* Environment Variables
* Application Deployment
* Troubleshooting

This is **Step‑1 of End‑to‑End DevOps Project**

---

# 🏗️ 3‑Tier Architecture (Linux Local)

```
Browser
   ↓
Apache (Web Tier)
   ↓
PHP Application (App Tier)
   ↓
MariaDB (Database Tier)
```

---

# 🐧 Step 1 — Update System

Always update system before installation

```bash
sudo apt update -y
sudo apt upgrade -y
```

Useful Linux Commands

```bash
uname -a
whoami
pwd
ls -la
free -m
df -h
```

---

# 🗂️ Step 2 — Install Required Packages

```bash
sudo apt install apache2 php php-mysql mariadb-server git curl -y
```

Verify Installation

```bash
apache2 -v
php -v
mysql --version
```

---

# 🔧 Step 3 — Start Services

```bash
sudo systemctl start apache2
sudo systemctl enable apache2

sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Check Status

```bash
sudo systemctl status apache2
sudo systemctl status mariadb
```

---

# 🗄️ Step 4 — Create Database

Login to MariaDB

```bash
sudo mysql
```

Create Database

```sql
CREATE DATABASE ecomdb;

CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';

GRANT ALL PRIVILEGES ON ecomdb.* TO 'ecomuser'@'localhost';

FLUSH PRIVILEGES;

EXIT;
```

---

# 📦 Step 5 — Create Database Table

Create SQL file

```bash
nano db-load-script.sql
```

Paste

```sql
USE ecomdb;

CREATE TABLE products (
 id mediumint(8) unsigned NOT NULL auto_increment,
 Name varchar(255),
 Price varchar(255),
 ImageUrl varchar(255),
 PRIMARY KEY (id)
);

INSERT INTO products (Name,Price,ImageUrl) VALUES
("Laptop","100","c-1.png"),
("Drone","200","c-2.png"),
("VR","300","c-3.png"),
("Tablet","50","c-4.png");
```

Load Database

```bash
sudo mysql < db-load-script.sql
```

Verify

```bash
sudo mysql

use ecomdb;

show tables;

select * from products;
```

---

# 🌐 Step 6 — Configure Apache

Set index.php first

```bash
sudo nano /etc/apache2/mods-enabled/dir.conf
```

Make sure

```
DirectoryIndex index.php index.html
```

Restart Apache

```bash
sudo systemctl restart apache2
```

---

# 📂 Step 7 — Deploy Application

Move to web directory

```bash
cd /var/www/html
```

Remove default files

```bash
sudo rm -rf *
```

Clone Project

```bash
sudo git clone https://github.com/Saurabhtiwari0987/php_ecommerce_Website.git .
```

Check files

```bash
ls -la
```

---

# 🔐 Step 8 — Create Environment File

```bash
sudo nano .env
```

Add

```
DB_HOST=localhost
DB_USER=ecomuser
DB_PASSWORD=ecompassword
DB_NAME=ecomdb
```

---

# 🔑 Step 9 — Set Permissions

```bash
sudo chown -R www-data:www-data /var/www/html

sudo chmod -R 755 /var/www/html
```

---

# 🧪 Step 10 — Test Application

From Linux

```bash
curl localhost
```

From Browser

```
http://localhost
```

---

# 🔍 Troubleshooting Commands

Check Apache Logs

```bash
sudo tail -f /var/log/apache2/error.log
```

Check Port

```bash
sudo netstat -tulpn | grep 80
```

Check Service

```bash
sudo systemctl status apache2
```

Restart Services

```bash
sudo systemctl restart apache2
sudo systemctl restart mariadb
```

---

# 📚 Linux Commands Used in Project

File Commands

```bash
ls
cd
pwd
mkdir
rm
cp
mv
```

Service Commands

```bash
systemctl start
systemctl stop
systemctl restart
systemctl status
```

Permission Commands

```bash
chmod
chown
```

Networking Commands

```bash
curl
ping
netstat
ss
```

Process Commands

```bash
top
ps -ef
kill
```

---

# 🎯 Learning Outcome

After completing this lab student will learn:

✅ Linux Basics
✅ Apache Web Server
✅ PHP Configuration
✅ Database Setup
✅ Environment Variables
✅ Application Deployment
✅ Troubleshooting

---

# 🐚 Shell Scripting Automation (DevOps Practice)

This project also includes **Shell Scripting** to automate deployment.

---

# 📜 Script 1 — Full Deployment Script

Create file

```bash
nano deploy.sh
```

Paste

```bash
#!/bin/bash

# Update System
sudo apt update -y
sudo apt upgrade -y

# Install Packages
sudo apt install apache2 php php-mysql mariadb-server git curl -y

# Start Services
sudo systemctl start apache2
sudo systemctl enable apache2

sudo systemctl start mariadb
sudo systemctl enable mariadb

# Create Database
sudo mysql <<EOF
CREATE DATABASE ecomdb;
CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
GRANT ALL PRIVILEGES ON ecomdb.* TO 'ecomuser'@'localhost';
FLUSH PRIVILEGES;
EOF

# Deploy Application
cd /var/www/html
sudo rm -rf *

sudo git clone https://github.com/Saurabhtiwari0987/php_ecommerce_Website.git .

# Permission
sudo chown -R www-data:www-data /var/www/html

# Restart Apache
sudo systemctl restart apache2


echo "Deployment Completed Successfully"
```

Make Executable

```bash
chmod +x deploy.sh
```

Run Script

```bash
./deploy.sh
```

---

# 📜 Script 2 — Database Setup Script

```bash
nano db-setup.sh
```

```bash
#!/bin/bash

sudo mysql <<EOF
CREATE DATABASE ecomdb;
CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
GRANT ALL PRIVILEGES ON ecomdb.* TO 'ecomuser'@'localhost';
FLUSH PRIVILEGES;
EOF

echo "Database Created"
```

---

# 📜 Script 3 — Application Deployment Script

```bash
nano app-deploy.sh
```

```bash
#!/bin/bash

cd /var/www/html

sudo rm -rf *

sudo git clone https://github.com/Saurabhtiwari0987/php_ecommerce_Website.git .

sudo chown -R www-data:www-data /var/www/html

sudo systemctl restart apache2

echo "Application Deployed"
```

---

# 📜 Script 4 — Health Check Script

```bash
nano health-check.sh
```

```bash
#!/bin/bash

echo "Apache Status"

sudo systemctl status apache2

echo "Database Status"

sudo systemctl status mariadb

echo "Port Check"

sudo ss -tulpn | grep 80
```

---

# 📚 Shell Script Commands Used

```bash
#!/bin/bash
if
else
fi
EOF
chmod +x
./script.sh
```

---

# 🎯 Learning Outcome

Student will learn:

✅ Linux Commands
✅ Apache Deployment
✅ Database Setup
✅ Shell Scripting
✅ Automation
✅ Troubleshooting

---

# 🚀 Next Step

# ☁️ AWS 3‑Tier Architecture Project — PHP Application Deployment

# 🎯 Project Goal

Deploy the same **3‑Tier PHP Application** on **AWS Cloud** using:

* VPC
* Public & Private Subnets
* Internet Gateway
* NAT Gateway
* Route Tables
* EC2 Instances
* Application Load Balancer
* Auto Scaling Group
* RDS Database
* CloudWatch Monitoring

This is **Step‑2 of End‑to‑End DevOps Project**

---

# 🏗️ AWS 3‑Tier Architecture Diagram

```
                Internet
                   |
             Internet Gateway
                   |
         -------------------------
         |                       |
     Public Subnet 1        Public Subnet 2
     (Web Tier)             (Web Tier)
         |                       |
         -------- ALB -----------
                   |
        ---------------------------
        |                         |
   Private Subnet 1         Private Subnet 2
     (App Tier)               (App Tier)

        ---------------------------
        |                         |
   Private Subnet 3         Private Subnet 4
    (Database Tier)          (Database Tier)

              RDS Database
```

---

# 📍 Architecture Requirements

| Resource          | Count |
| ----------------- | ----- |
| VPC               | 1     |
| Availability Zone | 2     |
| Public Subnet     | 2     |
| Private Subnet    | 4     |
| NAT Gateway       | 1     |
| Internet Gateway  | 1     |
| Route Table       | 3     |
| EC2 Instance      | 2     |
| RDS Database      | 1     |
| Load Balancer     | 1     |
| Auto Scaling      | 1     |

---

# 🪜 Step 1 — Create VPC

Go to AWS Console → VPC → Create VPC

```
Name: DevOps-3tier-VPC
CIDR: 10.0.0.0/16
```

Click Create

---

# 🪜 Step 2 — Create Subnets

Create 6 Subnets

### Public Subnets

Public Subnet 1

```
CIDR: 10.0.1.0/24
AZ: ap-south-1a
```

Public Subnet 2

```
CIDR: 10.0.2.0/24
AZ: ap-south-1b
```

---

### Private Subnets (App Tier)

Private Subnet 1

```
10.0.3.0/24
```

Private Subnet 2

```
10.0.4.0/24
```

---

### Private Subnets (Database Tier)

Private Subnet 3

```
10.0.5.0/24
```

Private Subnet 4

```
10.0.6.0/24
```

---

# 🪜 Step 3 — Create Internet Gateway

Create Internet Gateway

Attach to VPC

```
DevOps-IGW
```

---

# 🪜 Step 4 — Create NAT Gateway

Create NAT Gateway in

```
Public Subnet 1
```

Allocate Elastic IP

Create NAT Gateway

---

# 🪜 Step 5 — Create Route Tables

## Public Route Table

Add Route

```
0.0.0.0/0 → Internet Gateway
```

Attach to:

* Public Subnet 1
* Public Subnet 2

---

## Private Route Table

Add Route

```
0.0.0.0/0 → NAT Gateway
```

Attach to:

* Private Subnet 1
* Private Subnet 2
* Private Subnet 3
* Private Subnet 4

---

# 🪜 Step 6 — Create Security Groups

## Web Tier SG

Allow

```
HTTP 80
SSH 22
```

---

## App Tier SG

Allow

```
SSH
HTTP
```

---

## Database SG

Allow

```
MYSQL 3306
```

---

# 🪜 Step 7 — Launch EC2 Instances

Launch 2 Instances

Web Tier Instance

```
Public Subnet 1
```

App Tier Instance

```
Private Subnet 1
```

---

# 🪜 Step 8 — Install Application

SSH into Web Server

Install Packages

```bash
sudo apt update
sudo apt install apache2 php php-mysql git -y
```

Clone Application

```bash
cd /var/www/html
sudo rm -rf *

sudo git clone https://github.com/Saurabhtiwari0987/php_ecommerce_Website.git .
```

---

# 🪜 Step 9 — Create RDS Database

Create Database

```
Engine: MySQL
```

Choose

```
Private Subnet
```

Security Group

```
Database SG
```

---

# 🪜 Step 10 — Connect Application to RDS

Update .env

```
DB_HOST=RDS-ENDPOINT
DB_USER=admin
DB_PASSWORD=password
DB_NAME=ecomdb
```

---

# 🪜 Step 11 — Create Load Balancer

Create Application Load Balancer

Attach

* Public Subnet 1
* Public Subnet 2

Add Target Group

Attach EC2 Instances

---

# 🪜 Step 12 — Create Auto Scaling Group

Create Launch Template

Create Auto Scaling

Attach Load Balancer

Select Private Subnets

---

# 🪜 Step 13 — Enable CloudWatch

Enable Monitoring

Create Alarm

CPU Utilization

---

# 🎯 Final Architecture

```
Internet
   |
Load Balancer
   |
Web Tier EC2
   |
App Tier EC2
   |
RDS Database
```

---

# 🎯 Learning Outcome

Student will learn:

✅ AWS VPC
✅ Subnets
✅ NAT Gateway
✅ Route Tables
✅ EC2
✅ RDS
✅ Load Balancer
✅ Auto Scaling
✅ CloudWatch

---

# 🚀 Next Step





