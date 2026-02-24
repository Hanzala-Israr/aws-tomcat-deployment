# Tomcat Web Application Deployment on AWS EC2

This project demonstrates how to deploy a Java web application on an Apache Tomcat server running on an AWS EC2 instance. It includes installing Tomcat, configuring users, and deploying applications using the Tomcat Manager.

This project was completed as part of a DevOps Bootcamp module focused on build tools and deployment.

---

## Project Overview

The goal of this project is to:

- Set up an EC2 instance
- Install and configure Apache Tomcat
- Enable Tomcat Manager access
- Deploy a Java web application
- Manage Tomcat using custom commands

---

## Prerequisites

- AWS Account
- EC2 Instance (Amazon Linux / Ubuntu)
- Java Installed
- Basic Linux Knowledge

### Required Open Ports

- 22 (SSH)
- 8080 (Tomcat)

---

## Connect to EC2

```bash
ssh ec2-user@your-ec2-public-ip
```

---

## Switch to Root User

```bash
sudo su
```

---

## Install Tomcat

### Move to /opt directory

```bash
cd /opt
```

### Download Tomcat

```bash
wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz
```

### Extract Tomcat

```bash
tar -xvf apache-tomcat-9.0.65.tar.gz
```

---

## Configure Tomcat Users

Navigate to configuration folder:

```bash
cd /opt/apache-tomcat-9.0.65/conf
```

Edit users file:

```bash
vi tomcat-users.xml
```

Add inside `<tomcat-users>`:

```xml
<user username="admin" password="admin1234" roles="admin-gui,manager-gui,manager-script"/>
```

---

## Enable Manager Access

Edit manager context file:

```bash
vi /opt/apache-tomcat-9.0.65/webapps/manager/META-INF/context.xml
```

Comment out this section:

```xml
<!--
<Valve className="org.apache.catalina.valves.RemoteAddrValve"
 allow="127\.\d+\.\d+\.\d+|::1" />
-->
```

Edit host-manager context file:

```bash
vi /opt/apache-tomcat-9.0.65/webapps/host-manager/META-INF/context.xml
```

Comment out the same section.

---

## Create Start/Stop Commands

```bash
ln -s /opt/apache-tomcat-9.0.65/bin/startup.sh /usr/bin/startTomcat
ln -s /opt/apache-tomcat-9.0.65/bin/shutdown.sh /usr/bin/stopTomcat
```

---

## Start Tomcat

```bash
startTomcat
```

---

## Stop Tomcat

```bash
stopTomcat
```

---

## Access Tomcat

Tomcat Home Page:

http://your-ec2-public-ip:8080

Tomcat Manager:

http://your-ec2-public-ip:8080/manager/html

---

## Deploy Application

1. Open Tomcat Manager
2. Login with credentials
3. Upload WAR file
4. Click Deploy

---

## Technologies Used

- Apache Tomcat
- AWS EC2
- Linux
- Java

---

## Author

Hanzala Israr  
BS Computer Science – 4th Semester  
DevOps Bootcamp Student
