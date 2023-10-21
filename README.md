# LEMP_STACK
Web Stack Implemantation(LEMP)

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/lemp.jpg)  

### What is LEMP?

The LEMP software stack is a group of software that can be used to serve dynamic web pages and web applications written in PHP. This is an acronym that describes a Linux operating system, with an Nginx web server. The backend data is stored in the MySQL database and the dynamic processing is handled by PHP.

This guide demonstrates how to install a LEMP stack on an Ubuntu 22.04 server. The Ubuntu operating system takes care of the Linux portion of the stack. We will describe how to get the rest of the components up and running.

**LEMP Stands For:**

- **L**- Linux Operating System
- **E**- Nginx Server(pronounced Engine-X)
- **M**- MySQL Database
- **P**- PHP


## Web Stack Implemantation

Inorder to complete the project you will need an AWS account and virtual server with Ubuntu.

1. Register a new AWS account https://repost.aws/knowledge-center/create-and-activate-aws-account
2. Select the preffered region and launch a new EC2 instance, then connect to the instance via ssh.


### Installing the Nginx Web Server

In order to display web pages to our vistors, we are going to emply Nginx. We'll use the `apt` package manager for the install. Since its the first time using the `apt` for the session, we will start by updating the server's package index. Following that, we will check if the server(nginx) is running

`sudo apt update`
`sudo apt install nginx`
`sudo systemctl status nginx`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_1.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_2.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_3.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_4.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_5.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_6.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_7.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_8.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_9.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_10.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_11.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_12.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_13.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_14.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_15.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_16.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_17.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_18.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_19.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_20.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_21.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_22.png) 

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_23.png) 
