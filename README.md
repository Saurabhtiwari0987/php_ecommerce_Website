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
nano or vi deploy.sh
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
nano or Vi db-setup.sh
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
nano or Vi app-deploy.sh
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
nano or Vi health-check.sh
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


# 🐳 Git + Docker + Docker Compose — 3 Tier PHP Application

# 🎯 Project Goal

Deploy the same **3‑Tier PHP Application** using:

* Git Workflow
* Docker
* Docker Network
* Multi Container Architecture
* Docker Compose
* Apache + PHP Container
* MariaDB Container

This is **Step‑3 of End‑to‑End DevOps Project**

---

# 🏗️ Architecture

```
Browser
   |
Docker Container (Apache + PHP)
   |
Docker Network
   |
MariaDB Container
```

---

# 🪜 Step 1 — Install Docker

Ubuntu / WSL

```bash
sudo apt update
sudo apt install docker.io -y

sudo systemctl start docker
sudo systemctl enable docker
```

Verify

```bash
docker --version
```

---

# 🪜 Step 2 — Install Docker Compose

```bash
sudo apt install docker-compose -y
```

Verify

```bash
docker-compose --version
```

---

# 🪜 Step 3 — Git Project Setup

Clone Project

```bash
git clone https://github.com/Saurabhtiwari0987/php_ecommerce_Website.git

cd php_ecommerce_Website
```

---

# 🪜 Step 4 — Git Branch Workflow

Create Dev Branch

```bash
git checkout -b dev
```

Create Feature Branch

```bash
git checkout -b feature-docker
```

Commit Changes

```bash
git add .

git commit -m "Added Docker Support"
```

Merge Branch

```bash
git checkout dev

git merge feature-docker
```

Push to GitHub

```bash
git push origin dev
```

---

# 🪜 Step 5 — Create Dockerfile

Create file

```bash
nano Dockerfile
```

Paste

```dockerfile
FROM php:8.2-apache

RUN docker-php-ext-install mysqli

COPY . /var/www/html/

EXPOSE 80
```

---

# 🪜 Step 6 — Build Docker Image

```bash
docker build -t php-ecommerce .
```

Verify

```bash
docker images
```

---

# 🪜 Step 7 — Create Docker Network

```bash
docker network create ecommerce-network
```

Verify

```bash
docker network ls
```

---

# 🪜 Step 8 — Run Database Container

```bash
docker run -d \
--name mysql-db \
--network ecommerce-network \
-e MYSQL_ROOT_PASSWORD=root \
-e MYSQL_DATABASE=ecomdb \
-e MYSQL_USER=ecomuser \
-e MYSQL_PASSWORD=ecompassword \
mysql:5.7
```

Verify

```bash
docker ps
```

---

# 🪜 Step 9 — Run Application Container

```bash
docker run -d \
--name php-app \
--network ecommerce-network \
-p 8080:80 \
php-ecommerce
```

---

# 🪜 Step 10 — Test Application

Browser

```
http://localhost:8080
```

---

# 🪜 Step 11 — Docker Compose Setup

Create file

```bash
nano docker-compose.yml
```

---

# 🪜 Step 12 — Docker Compose File

```yaml
version: '3.8'

services:

  db:
    image: mysql:5.7
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: ecomdb
      MYSQL_USER: ecomuser
      MYSQL_PASSWORD: ecompassword
    networks:
      - ecommerce-network

  web:
    build: .
    container_name: php-app
    ports:
      - "8080:80"
    depends_on:
      - db
    networks:
      - ecommerce-network

networks:
  ecommerce-network:
```

---

# 🪜 Step 13 — Run Docker Compose

```bash
docker-compose up -d
```

Verify

```bash
docker-compose ps
```

---

# 🪜 Step 14 — Stop Containers

```bash
docker-compose down
```

---

# 🪜 Step 15 — Troubleshooting

Check Logs

```bash
docker logs php-app
```

Check Containers

```bash
docker ps
```

Check Network

```bash
docker network inspect ecommerce-network
```

---

# 📚 Docker Commands Used

```bash
docker build

docker run

docker ps

docker stop

docker rm

docker images

docker network create

docker-compose up

docker-compose down
```

---

# 🎯 Learning Outcome

Student will learn:

✅ Git Workflow
✅ Dockerfile
✅ Docker Image
✅ Docker Network
✅ Multi Container
✅ Docker Compose

---

# 🚀 Next Step


# ☸️ Kubernetes Deployment — 3 Tier PHP Application

# 🎯 Project Goal

Deploy the same **PHP 3‑Tier Application** on Kubernetes using:

* Kubeadm Cluster
* Kind Cluster (Local Testing)
* Deployment
* Service
* ConfigMap
* Secret
* Ingress
* Persistent Volume
* Prometheus Monitoring
* Grafana Dashboard

This is **Step‑4 of End‑to‑End DevOps Project**

---

# 🏗️ Kubernetes Architecture

```
Internet
   |
Ingress Controller
   |
Service (ClusterIP)
   |
PHP App Pods
   |
Service
   |
MySQL Pod
   |
Persistent Volume
```

---

# 🪜 Step 1 — Install Kubernetes (Kubeadm)

## Install Dependencies

```
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl
```

## Install Docker

```
sudo apt install docker.io -y
```

---

# Install Kubernetes Packages

```
curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"

sudo apt install kubeadm kubelet kubectl -y
```

---

# Initialize Cluster

```
sudo kubeadm init
```

---

# Configure kubectl

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

---

# Install Network Plugin

```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

---

# 🪜 Step 2 — KIND Cluster (Alternative)

Install Kind

```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

Create Cluster

```
kind create cluster --name devops-cluster
```

Verify

```
kubectl get nodes
```

---

# 🪜 Step 3 — Namespace

namespace.yaml

```
apiVersion: v1
kind: Namespace
metadata:
  name: ecommerce
```

Apply

```
kubectl apply -f namespace.yaml
```

---

# 🪜 Step 4 — MySQL Deployment

mysql-deployment.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  namespace: ecommerce
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: root
        - name: MYSQL_DATABASE
          value: ecomdb
        ports:
        - containerPort: 3306
```

---

# MySQL Service

mysql-service.yaml

```
apiVersion: v1
kind: Service
metadata:
  name: mysql
  namespace: ecommerce
spec:
  ports:
  - port: 3306
  selector:
    app: mysql
  clusterIP: None
```

---

# 🪜 Step 5 — PHP Application Deployment

php-deployment.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php-app
  namespace: ecommerce
spec:
  replicas: 2
  selector:
    matchLabels:
      app: php
  template:
    metadata:
      labels:
        app: php
    spec:
      containers:
      - name: php
        image: php-ecommerce:latest
        ports:
        - containerPort: 80
```

---

# PHP Service

```
apiVersion: v1
kind: Service
metadata:
  name: php-service
  namespace: ecommerce
spec:
  type: NodePort
  selector:
    app: php
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30007
```

---

# Apply Resources

```
kubectl apply -f .
```

---

# 🪜 Step 6 — Ingress Controller

Install nginx ingress

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

---

# 🪜 Step 7 — Prometheus Monitoring

Install Helm

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

Add Repo

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update
```

Install Prometheus

```
helm install prometheus prometheus-community/kube-prometheus-stack
```

---

# 🪜 Step 8 — Access Grafana

Get Password

```
kubectl get secret prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 --decode
```

Port Forward

```
kubectl port-forward svc/prometheus-grafana 3000:80
```

Access

```
http://localhost:3000
```

Login

```
admin
password
```

---

# 🪜 Step 9 — Check Pods

```
kubectl get pods -n ecommerce
```

---

# 🪜 Step 10 — Troubleshooting

```
kubectl describe pod

kubectl logs podname

kubectl get svc
```

---

# 📚 Kubernetes Commands

```
kubectl get pods

kubectl get svc

kubectl get deploy

kubectl apply -f

kubectl delete -f
```

---

# 🎯 Learning Outcome

Student will learn

✅ Kubernetes Cluster
✅ Deployment
✅ Service
✅ Ingress
✅ Monitoring
✅ Prometheus
✅ Grafana

---

# 🚀 Next Step

# 🚀 Jenkins CI/CD Pipeline — Git → Docker → DockerHub → Kubernetes

# 🎯 Project Goal

Create Full Automated CI/CD Pipeline:

```
Developer Push Code → GitHub
        ↓
      Jenkins
        ↓
 Build Docker Image
        ↓
 Push to DockerHub
        ↓
 Deploy to Kubernetes
```

This is **Step‑5 of End‑to‑End DevOps Project**

---

# 🏗️ Architecture

```
GitHub
   |
Webhook
   |
Jenkins
   |
Docker Build
   |
DockerHub
   |
Kubernetes Deployment
```

---

# 🪜 Step 1 — Install Jenkins

Ubuntu

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

 echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
```

Start Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Access Jenkins

```
http://SERVER-IP:8080
```

---

# 🪜 Step 2 — Install Required Jenkins Plugins

Go to:

Manage Jenkins → Plugins

Install:

* Git Plugin
* Docker Plugin
* Docker Pipeline
* Kubernetes CLI Plugin
* Pipeline Plugin
* GitHub Integration Plugin

---

# 🪜 Step 3 — Install Docker on Jenkins Server

```bash
sudo apt install docker.io -y

sudo usermod -aG docker jenkins

sudo systemctl restart jenkins
```

Verify

```bash
docker ps
```

---

# 🪜 Step 4 — Add DockerHub Credentials

Manage Jenkins → Credentials

Add:

```
Username : DockerHub Username
Password : DockerHub Password
ID : dockerhub
```

---

# 🪜 Step 5 — Add Kubernetes Credentials

```bash
kubectl config view --raw
```

Add kubeconfig in Jenkins Credentials

ID:

```
kubeconfig
```

---

# 🪜 Step 6 — Create Jenkins Pipeline Job

New Item → Pipeline

Name:

```
php-ecommerce-pipeline
```

---

# 🪜 Step 7 — Jenkinsfile

Create Jenkinsfile in GitHub Repo

```groovy
pipeline {

agent any

stages {

stage('Clone Repository') {
steps {
 git 'https://github.com/Saurabhtiwari0987/php_ecommerce_Website.git'
}
}

stage('Build Docker Image') {
steps {
 script {
 docker.build("saurabhtiwari/php-ecommerce:latest")
 }
}
}

stage('Push Docker Image') {
steps {
 script {
 docker.withRegistry('', 'dockerhub') {
 docker.image('saurabhtiwari/php-ecommerce:latest').push()
 }
 }
}
}

stage('Deploy to Kubernetes') {
steps {
sh 'kubectl apply -f k8s/'
}
}

}
}
```

---

# 🪜 Step 8 — Kubernetes Deployment YAML

k8s/deployment.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: php
  template:
    metadata:
      labels:
        app: php
    spec:
      containers:
      - name: php
        image: saurabhtiwari/php-ecommerce:latest
        ports:
        - containerPort: 80
```

---

# Service YAML

```yaml
apiVersion: v1
kind: Service
metadata:
  name: php-service
spec:
  type: NodePort
  selector:
    app: php
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30007
```

---

# 🪜 Step 9 — GitHub Webhook

GitHub Repo → Settings → Webhooks

Add:

```
http://jenkins-ip:8080/github-webhook/
```

Now pipeline triggers automatically

---

# 🪜 Step 10 — Test Pipeline

Push Code

```bash
git add .

git commit -m "updated code"

git push
```

Pipeline Automatically:

✅ Build Image
✅ Push DockerHub
✅ Deploy Kubernetes

---

# 🎯 Pipeline Flow

```
GitHub Push
     ↓
Jenkins Trigger
     ↓
Docker Build
     ↓
DockerHub Push
     ↓
Kubernetes Deploy
```

---

# 🎯 Learning Outcome

Student will learn:

✅ Jenkins Pipeline
✅ Docker Automation
✅ Kubernetes Deploy
✅ CI/CD Pipeline

---

# 🚀 Next Step

# 🚀 End‑to‑End DevOps Project using Terraform

# 🎯 Project Overview

We will build Full Production DevOps Architecture using Terraform:

```
Terraform → AWS Infrastructure
        ↓
EC2 Instances
        ↓
Jenkins Setup
        ↓
Docker Build
        ↓
Push to DockerHub
        ↓
Deploy to Kubernetes
        ↓
Monitoring (Prometheus + Grafana)
```

---

# 🏗️ Final Architecture

```
AWS Cloud
 ├── VPC
 │   ├── Public Subnet
 │   │    ├── Jenkins Server
 │   │    ├── Bastion Host
 │   │
 │   ├── Private Subnet
 │        ├── Kubernetes Master
 │        ├── Kubernetes Worker 1
 │        ├── Kubernetes Worker 2
```

---

# 🪜 Step 1 — Install Terraform

Ubuntu

```bash
sudo apt update
sudo apt install unzip -y

wget https://releases.hashicorp.com/terraform/1.6.6/terraform_1.6.6_linux_amd64.zip

unzip terraform_1.6.6_linux_amd64.zip

sudo mv terraform /usr/local/bin/

terraform -version
```

---

# 🪜 Step 2 — Install AWS CLI

```bash
sudo apt install awscli -y

aws configure
```

Enter:

```
Access Key
Secret Key
Region
```

---

# 🪜 Step 3 — Terraform Project Structure

```
terraform-project
 ├── provider.tf
 ├── vpc.tf
 ├── subnet.tf
 ├── ec2.tf
 ├── security.tf
 ├── variables.tf
 ├── outputs.tf
```

---

# 🪜 Step 4 — provider.tf

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

---

# 🪜 Step 5 — VPC Creation

vpc.tf

```hcl
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "DevOps-VPC"
  }
}
```

---

# 🪜 Step 6 — Subnet Creation

subnet.tf

```hcl
resource "aws_subnet" "public" {
  vpc_id = aws_vpc.main.id
  cidr_block = "10.0.1.0/24"
  availability_zone = "ap-south-1a"

  tags = {
    Name = "Public Subnet"
  }
}

resource "aws_subnet" "private" {
  vpc_id = aws_vpc.main.id
  cidr_block = "10.0.2.0/24"
  availability_zone = "ap-south-1a"

  tags = {
    Name = "Private Subnet"
  }
}
```

---

# 🪜 Step 7 — Internet Gateway

```hcl
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main.id
}
```

---

# 🪜 Step 8 — Route Table

```hcl
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.gw.id
  }
}
```

---

# 🪜 Step 9 — Security Group

security.tf

```hcl
resource "aws_security_group" "devops" {
  vpc_id = aws_vpc.main.id

  ingress {
    from_port = 22
    to_port = 22
    protocol = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port = 8080
    to_port = 8080
    protocol = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port = 80
    to_port = 80
    protocol = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

---

# 🪜 Step 10 — EC2 Instance

```hcl
resource "aws_instance" "jenkins" {
  ami = "ami-0f5ee92e2d63afc18"
  instance_type = "t2.medium"
  subnet_id = aws_subnet.public.id

  vpc_security_group_ids = [aws_security_group.devops.id]

  tags = {
    Name = "Jenkins Server"
  }
}
```

---

# 🪜 Step 11 — Terraform Commands

```bash
terraform init

terraform plan

terraform apply
```

---

# 🪜 Step 12 — Install Jenkins using Terraform UserData

```hcl
user_data = <<-EOF
#!/bin/bash
sudo apt update
sudo apt install docker.io -y
sudo apt install openjdk-17-jdk -y
sudo apt install jenkins -y
EOF
```

---

# 🪜 Step 13 — Kubernetes Setup

After EC2 creation:

Install Kubernetes using kubeadm

Master Node

Worker Nodes

---

# 🪜 Step 14 — Jenkins Pipeline Flow

```
GitHub Push
      ↓
Jenkins Build
      ↓
Docker Image
      ↓
DockerHub
      ↓
Kubernetes Deploy
```

---

# 🪜 Step 15 — Monitoring Setup

Install:

Prometheus

Grafana

---

# 🎯 Final Project Flow

```
Terraform
    ↓
AWS Infrastructure
    ↓
Jenkins
    ↓
Docker
    ↓
DockerHub
    ↓
Kubernetes
    ↓
Monitoring
```

---

# 🎯 Resume Project Title

End to End DevOps Automation using:

Terraform
AWS
Jenkins
Docker
Kubernetes
Prometheus
Grafana

---







