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

# Stage 1: Installing Apache2 and Updating the firewall.

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

# Stage 2: Installing MYSQL
##    What is MYSQL
MySQL is an open-source relational database management system used to store, manage, and retrieve data for web applications. It is used to Store information like user accounts, product details, and content in an organized, easily queryable format.
## 1. Install the mysql-server
$ sudo apt install mysql-server
When prompted, confirm installation by typing Y, and then ENTER.
![image](https://github.com/user-attachments/assets/c2d07a5a-9e88-4b42-bb56-d2d902507572)


## 2. Log in to the MySQL console by typing:
$ sudo mysql
![image](https://github.com/user-attachments/assets/5270204a-aad8-41e1-96d5-eb6fac0e1f4a)

## 3. Set a password for the root user.
ALTERUSER'root' @'localhost' IDENTIFIED WITH mysql_native_password BY'PassWord.1';
## Error Message
![image](https://github.com/user-attachments/assets/eefc6da1-aa97-41f1-ae22-69a8ac190d6d)

## Troubleshooting:
The error in the MySQL query is caused by syntax mistakes. Specifically:
   1. There needs to be a space between ALTER and USER.
   2. You should ensure proper spacing around 'root' and the password string.
   3. It should be ALTER USER instead of ALTERUSER.
## Solution
ALTER USER is the correct command to modify a user's authentication method or password.
'root'@'localhost' refers to the root user connecting from localhost.
IDENTIFIED WITH mysql_native_password sets the authentication method to mysql_native_password.
BY 'PassWord.1' sets the new password to PassWord.1.
## Corrected Syntax
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
## Result
![image](https://github.com/user-attachments/assets/31967ca9-8558-45bd-9b89-4782130acea3)
## Exit mysql
exit
## Run the Interactive script command
      sudo mysql_secure_installation
The command "$ sudo mysql_secure_installation" is used to improve the security of your MySQL installation by performing a few essential security-related tasks.

a. Protect your MySQL server from unauthorized access.

b. Prevent remote root access (if not needed).

c. Ensure your installation is more resilient to attacks.

![image](https://github.com/user-attachments/assets/0b22530d-cdf0-4252-8f6b-fe0f33e772e2)

Press y to set-up VALIDATE PASSWORD component

![image](https://github.com/user-attachments/assets/d72ad011-403a-41bb-9769-0a8e3c39173b)

Enter 0,1 or 2 to choose which level of password validation policy you wish

![image](https://github.com/user-attachments/assets/4db9b999-8bce-46fd-aa20-1e50318ae7fc)

Enter y to continue

![image](https://github.com/user-attachments/assets/81406f49-12b3-4015-b912-12b50791a98a)

Enter the desired password

![image](https://github.com/user-attachments/assets/1b9dbf19-e788-4a5a-847c-b85e98d8cb51)

Press y to continue.

For the rest of the question press y and hit enter at each prompt.

![image](https://github.com/user-attachments/assets/4f348ce1-cd6b-4351-98d3-e6cc6dee1386)

## Log in to the MYSQL CONSOLE after changing the user root pasword by using

sudo mysql -p

Enter the new password when promped to

![image](https://github.com/user-attachments/assets/e4ccdb80-e9f6-48b0-8446-70e2cbcc4cef)

Exit the MYSQL console

exit
# Stage 3 Installing PHP, php-mysql, libapache2-mod-php
## What is PHP

PHP is used to develop the dynamic content of the website. These languages process user inputs, interact with the database, and generate dynamic HTML for the web server to serve to users.

## What is php-mysql

It is a PHP module that allows PHP to communicate with MySQL-based databases.

## What is libapache2-mod-php

to enable Apache to handle PHP files.















      












 
