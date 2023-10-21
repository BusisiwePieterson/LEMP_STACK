# LEMP_STACK


![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/lemp.jpg)  

### What is LEMP?

The LEMP software stack is a group of software that can be used to serve dynamic web pages and web applications written in PHP. This is an acronym that describes a Linux operating system, with an Nginx web server. The backend data is stored in the MySQL database and the dynamic processing is handled by PHP.

This guide demonstrates how to install a LEMP stack on an Ubuntu 22.04 server. The Ubuntu operating system takes care of the Linux portion of the stack. We will describe how to get the rest of the components up and running.

**LEMP Stands For:**

- **L**- Linux Operating System
- **E**- Nginx Server(pronounced Engine-X)
- **M**- MySQL Database
- **P**- PHP


## Web Stack Implementation

In order to complete the project you will need an AWS account and a virtual server with Ubuntu.

1. Register a new AWS account https://repost.aws/knowledge-center/create-and-activate-aws-account
2. Select the preferred region and launch a new EC2 instance, then connect to the instance via ssh.


### Installing the Nginx Web Server

In order to display web pages to our visitors, we are going to employ Nginx. We'll use the `apt` package manager for the installation. Since it's the first time using the `apt` for the session, we will start by updating the server's package index. Following that, we will check if the server(nginx) is running

`sudo apt update`
`sudo apt install nginx`
`sudo systemctl status nginx`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_1.png)  

Our Web Server is now running!! But, before we can receive traffic from our Web Server, we need to open **TCP Port 80** which is the port web browsers use to access web pages.
So, let's add a rule to the EC2 configuration to open an inbound connection through port 80.

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_2.png)  

Now that the Web Server is running, let's try accessing it locally and from the Internet.

`curl http://localhost:80`
`http://<Public-IP-Address>:80`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_3.png)  

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_4.png)  

## **Installing MySQL**

We need to store and manage data for our site and we will be using MySQL a popular DBMS to do so.

 - Run `sudo apt install mysql-server`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_5.png)  

To connect to the MySQL server as root user

 - Run `sudo mysql`

We will set a password for the root user and exit.

 - ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';


![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_6.png)  

To start the interactive script

 - Run `sudo mysql_secure_installation`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_7.png) 

## **Installing PHP**

We have installed Nginx to serve the content and MySQL to store and manage our data, we need PHP to generate dynamic content for the web server.

 - Run `sudo apt install php-fpm php-mysql`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_8.png)  

## **Configuring Nginx to use PHP**

We first create the root web directory for our domain, then assign ownership of the directory with the $USER environment variable, and lastly, open a new config file using vim.

 - Run `sudo mkdir /var/www/projectLEMP`
 - Run `sudo chown -R $USER:$USER /var/www/projectLEMP`
 - Run `sudo vim /etc/nginx/sites-available/projectLEMP`



![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_9.png)  

Here is what each of these directives and location blocks do:
> 1. **listen** : Defines what port NginX will listen on. In this case, it will listen on port 80 ,the default port for HTTP
> 2. **root** : Defines the document root where the files served by this website ar stored.
> 3. **index** : Defines in which order Nginx will prioritize `index files` for this website. It is a commnon practice to list `index.html` files with a higher precedence than index.php files to allow for quickly setting up a maintenance landing page in PHP applications. You can adjust these settings to better suit your application needs.
> 4. **server_name** : Defines which domain names and/or IP addresses this server block should respond for. Point this directive to your server's domain name or public IP address.
> 5. **location /** : The first location block includes a try files directive, which checks for the existence of files or directories matching a URl request. If Nginx cannot find the appropriate resource, it will return a 404 error.
> 6. **location ~ \.php$** : This location block handles the actual PHP processing by pointing Nginx to the fastcgi-php.conf configuration file and the `php7.4-fpm.sock file` , which declares what socket is associated with `php-fpm`.
> 7. **location ~ /\.ht : The last location block deals with `.htaccess` files, which Nginx does not process. By adding the deny all directive, if `.htaccess` files happen to find their way into the document root ,they will not be served to visitors.



To activate the configuration by linking the config file from Nginx's directory.

 - Run `sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`


![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_10.png) 

To disable the default Nginx host that is currently configured on port 80.

 - Run `sudo unlink /etc/nginx/sites-enabled/default`

Now reload Nginx to apply the changes

 - Run ` sudo systemctl reload nginx` 


![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_11.png)  

The website is active but the web root /var/www/projectLEMP is empty, let's create a file in that location to test our web server.

 - Run `sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

Now let's go to our URL using our IP address

 - Run `http://<Public-IP-Address>:80`


![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_12.png) 

## **Testing PHP with Nginx**

The stack is now fully operational. Now, let's validate that Nginx can correctly handle `.php` files.

 - Open `vim /var/www/projectLEMP/info.php`

Type the following lines of code.

  ```
   <?php
   phpinfo();
  ```

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_13.png) 

Now access the page in the web browser.

 - Go to `http://server_domain_or_IP/info.php`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_14.png) 

After checking the relevant information about our PHP server, let's remove the file as it contains sensitive info about the PHP environment.

 - Run `$ sudo rm /var/www/your_domain/info.php`

## **Retrieving data from MySQL with PHP**

We will now create a test database with a `To-do list` and configure access to it. The Nginx website would be able to query data from the DB and display it. We will then create a database named **example_database** and a user named **example_user**

First, connect to the DB console using the **root** account

 - Run `sudo mysql`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_15.png) 

To create a new database run the following command from the MySQL console

 - Run `mysql> CREATE DATABASE example_database`;

Next, let's create a new user `example_user` and give the user a password `PassWord.123`
 - Run `mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.123';`

Now we need to give the user permission over the `example_database` database

 - Run `mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';`
 - Run `mysql> exit`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_17.png) 

To test if the new user has proper permissions, we will log into the MySQL console again. The `-p` flag will prompt for a password.

 - Run `$ mysql -u example_user -p`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_18.png) 

Confirm that you have access to the database.

 - Run `mysql> SHOW DATABASES;`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_19.png) 

Next, we will create a table named **todo_list**. We will also insert a row of content in the table.

 - Run `CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));`

 - Run `mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");`
 - Run `mysql> exit`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_20.png)

Let's insert a few more rows and change the values. We will also confirm that the data was saved in the table.

- Run `mysql> INSERT INTO example_database.todo_list (content) VALUES ("<chang_value _and_repeat>")`
- Run `mysql>  SELECT * FROM example_database.todo_list;`
- Run `mysql> exit`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_21.png) 

Now we will create a PHP script that connects to the database and queries the content of our table.

 - `$ vim /var/www/projectLEMP/todo_list.php`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_22.png) 

Finally, access the page in your web browser.

 - `http://<Public_domain_or_IP>/todo_list.php`

![Images](https://github.com/BusisiwePieterson/LEMP_STACK/blob/main/Images/Screenshot_23.png) 
