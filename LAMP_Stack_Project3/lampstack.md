# LAMP STACK IMPLEMENTATION
The Project(LAMP Stack) is a comprehensive program designed for individuals seeking to build and deploy web
applications using the LAMP stack. This course offers a hands-on learning experience, guiding participants through the
process of creating dynamic websites by combining Linux, Apache, MySQL, and PHP. Throughout the course and project
implementation, I have gained a solid understanding of the LAMP stack components and their roles in web
application development. Starting with an introduction to the LAMP stack architecture.

## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
I have realised that everything will be doing as a DevOps engineer is
around software, websites, applications etc. And, there are different stack of technologies that make different solutions
possible. These stack of technologies are regarded as WEB STACKS. Examples of Web Stacks include LAMP, LEMP
MEAN, and MERN stacks.

### What is a Technology stack?
A technology stack is a set of frameworks and tools used to develop a software product. This set of frameworks and
tools are very specifically chosen to work together in creating a well-functioning software. They are acronymns for
individual technologies used together for a specific technology product. some examples are..

1. LAMP (Linux, Apache, MySQL, PHP or Python, or Perl)

2. LEMP (Linux, Nginx, MySQL, PHP or Python, or Perl)

3. MERN (MongoDB, ExpressJS, ReactJS, NodeJS)

4. MEAN (MongoDB, ExpressJS, AngularJS, NodeJS

Connecting to the EC2 instance using the terminal.
![Change directory](LAMPSTACK_IMAGES/cd.png)

Connect to the instance by running

ssh -i "devops.pem" ubuntu@ec2-16-171-133-147.eu-north-1.compute.amazonaws.com
![Change directory](LAMPSTACK_IMAGES/instanceconnection.png)

## Installing Apache and Updating the Firewall
Step 1- Installing Apache and Updating the Firewall
What exactly is Apache?
Apache HTTP Server is the most widely used web server software. Developed and maintained by Apache Software
Foundation, Apache is an open source software available for free. It runs on 67% of all webservers in the world. It is fast.
reliable, and secure. It can be highly customized to meet the needs of many different environments by using extensions
and modules. Most WordPress hosting providers use Apache as their web server software. However, websites and
other applications can run on other web server software as well. Such as Nginx, Micrelmft's l1S, etc.
The Apache web server is among the most popular web servers in the world. It's well documented, has an active
community of users, and has been in wide use for much of the history of the web, which makes it a great default choice
for hosting a website
## Install Apache using Ubuntu's package manager.
### Step 1 - Install Apache using Ubuntu's package manager.
update a list of packages in package manager
sudo apt update

run apache2 package installation

sudo apt install apache2

![Apache installation](LAMPSTACK_IMAGES/apacheinstall.png)

To verify that apache2 is running as a service

sudo systemctl status apache2

![Apache status](LAMPSTACK_IMAGES/apachestatus.png)

To verify if we can access it locally in our Ubuntu shell
$ curl http://localhost:80
or
$ curl http://127.0.0.1:80

![Apache status](LAMPSTACK_IMAGES/curl1.png)
or
![Apache status](LAMPSTACK_IMAGES/curl2.png)

Another way to retrieve the Pubic address

![Apache status](LAMPSTACK_IMAGES/apache2works.png)

## Installing Mysql
### Step 2 - Installing Mysql

Now that I have a web server up and running, I need to install a Database Management System (DBMS) to be able
to store and manage data for my site in a relational database. 

MySQL is a popular relational database management
system used within PHP environments, so we will use it in our project.

sudo apt install mysql-server
![Apache status](LAMPSTACK_IMAGES/sqlinstall.png)

When prompted, confirm installation by typing and then ENTER
When the installation is finished, log in to the MysQL console by typing,

sudo mysql

![Apache status](LAMPSTACK_IMAGES/sudomysql.png)

This will connect to the MySOL server as the administrative database user root, which is inferred by the use of sudo
when running this command. You should see output like this:

