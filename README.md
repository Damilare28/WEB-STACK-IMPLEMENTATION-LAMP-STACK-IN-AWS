# WEB-STACK-IMPLEMENTATION-LAMP-STACK-IN-AWS

# Purpose of this Project: 
This project helps to develop deep understanding on the following
•	Linux Terminal
•	Understanding on web technology stack such as LAMP
•	Components of LAMP Stack: LINUX, APACHE, MYSQL, PHP
•	How the Lamp stack works
# What is LAMP Stack: 
LAMP stack is a popular open-source software stack used for web development. It stands for Linux, Apache, MySQL, and PHP (or Perl/Python). Each component in the LAMP stack represents a layer of the software that supports the deployment of dynamic websites and web applications.
# Stages Involved:
•	Stage 0: Preparing Prerequisite. Creating an AWS account and a virtual server with Ubuntu Server OS.

•	Stage 1: Install Apache and Updating the Firewall.

•	Stage 2: Install MySQL.

•	Stage 3: Install PHP.

•	Stage 4: Create a Virtual Host for your Website using Apache.

# Stage 0: Preparing Prerequisite. 

## 1.	Create an AWS account and a virtual server with Ubuntu Server OS. 
The EC2 instance of t3.micro family with Ubuntu Server 24.04 LTS (HVM) was launched with the available zone eu-north-1b
![image](https://github.com/user-attachments/assets/afd1054c-0fba-410f-9529-c0432c3d087a)

## 2.	Selection of Instance Type and Creation of new key pair
a.	Select the preferred Instance type of your choice. For this project we’ll be using the free tier eligible.
b.	Create a new key pair for your choice.
![image](https://github.com/user-attachments/assets/91bfe714-d55d-4c9a-b8f8-5c4e5a5983fc)

## 3.	SECURITY GROUP:
Create a security group to set the firewall rules that control the traffic on your instance.
![image](https://github.com/user-attachments/assets/024e9e30-4078-471a-91a9-d4728a2c31c6)

## 4.	Connecting to Virtual Instance:
Connect to the virtual server using the SSH protocol using TCP port 22
![image](https://github.com/user-attachments/assets/c377a53e-43c8-4270-b41e-9cf7dff3d565)

![image](https://github.com/user-attachments/assets/a1e4f5d6-4cc8-470a-bb7e-e75f28938787)

![image](https://github.com/user-attachments/assets/3ea3a25e-b94c-4d03-81ab-54ce3843db85)

a.	Locate where the key is saved on the computer. 

b.	If properly set up, the link under the example should work perfectly.  
![image](https://github.com/user-attachments/assets/30d3d3a0-fdb4-4d78-b145-aba4956dba5d)

# Step 1: Installing Apache2 and Updating the firewall.

## What is Apache: 
Apache HTTP Server is a widely used open-source web server software. It handles incoming web requests, serves web pages to users, and supports a variety of modules for added functionality
## 1.	Update and upgrade all packages in the package manager.
   sudo apt update
   sudo apt upgrade
![image](https://github.com/user-attachments/assets/e9dd4156-6b88-48c0-8fa6-303e58c83bb7)

## 2. Run Apache2 command installation package
      sudo apt install apache2
  ![image](https://github.com/user-attachments/assets/1686673e-c66d-45cf-af73-8a01f0263a34)

## 3. Verify that apache is running as a service on the OS.
      sudo systemctl status apapche2
      Note: If it is green and running, then apache2 is running perfectly.
![image](https://github.com/user-attachments/assets/3202a97e-e07d-43c3-9bae-4dbdf80e8b38)

## The server can be accessed locally by using the commands below
   $ curl http://localhost:80   
            or            
   $ curl http://127.0.0.1:80
![image](https://github.com/user-attachments/assets/9cd375c7-cb6f-49bd-8567-92ca684dca2f)

## Test how our Apache HTTP server can respond to requests from the Internet. 
   Open a web browser of your choice and try to access following url
   
   http://<"Public ip address">:80-- "In place of the <Public-IP-Address> Use the public ip address on the instance page"
   
   Note: If the page is displayed, then the web server is now correctly installed and accessible through your firewall.
![image](https://github.com/user-attachments/assets/bc7869aa-0241-4231-94d9-fcf678d5866e)

Another way to retrieve your Public IP address, other than to check it in AWS Web console, is to use following command:

TOKEN='curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl- seconds: 21600"' && curl -H "X-aws-ec2-metadata-token: $TOKEN" -s http://169.254.169.254/latest/meta-data/public-ipv4

## Error Message:
![image](https://github.com/user-attachments/assets/74957a1e-d037-40fb-bf4b-d320f414baf8)

## Troubleshooting:
The issue lies in how the TOKEN is being assigned. It is not correctly capturing the result of the curl command in the TOKEN variable. It is being set to a string ('curl -X PUT ...') instead of executing the command and capturing its output.

## Solution: 
There is need to properly execute the curl command and assign its output to the TOKEN variable.
## Corrected syntax:
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
curl -H "X-aws-ec2-metadata-token: $TOKEN" -s http://169.254.169.254/latest/meta-data/public-ipv4
## Result:
![image](https://github.com/user-attachments/assets/4b65c956-c6d6-4ecc-9f10-602cbddcf850)

# Step 2: Installing MYSQL
##    What is MYSQL
MySQL is an open-source relational database management system used to store, manage, and retrieve data for web applications. It is used to Store information like user accounts, product details, and content in an organized, easily queryable format.







      












 
