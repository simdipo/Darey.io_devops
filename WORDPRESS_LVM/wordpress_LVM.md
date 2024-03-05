# Implementing Wordpress websitewith LVM Storage management

Implementing WordPress Website with LVM Storage Management on AWS EC2 Ubuntu Course Description: Welcome
to the Implementing WordPress Website with LVM Storage Management on AWS EC2 Ubuntu Course. lf you're eager
to learn how to build and manage a scalable WordPress website using AWS EC2 and LVM (Logical Volume Management)
storage, this comprehensive course is tailored specifically for you. Gain the knowledge and skills needed to deploy and
maintain a robust WordPress site on the AWS cloud platform. Designed with beginners in mind, this course provides a
step-by-step introduction to implementing WordPress on AWS EC2 using Ubuntu as the operating system.

You'll learn how to set up an EC2 instance, configure security groups, and establish a reliable connection to your
website. Through practical demonstrations and hands-on exercises, you'll delve into the intricacies of LVM storage
management on Ubuntu. We'lguide you through the process of creatingl pgical volumes, managing disk space, and
dynamically resizing volumes to accommodate changing storage requirements. As part of the course, you'l gain
proficiency in installing and configuring WordPress, customizing themes, and adding essential plugins to enhance your
website's functionality. We'l cover performance optimization techniques and best practices for securing your
WordPress installation on the AWS cloud. Our experienced instructor will provide expert guidance and insights into
managing a WordPress website on AWS EC2 with LVM storage, You'llearn how to handle common challenges,
troubleshoot issues, and effectively manage your website's resources.

By the end of this course, you'll have the necessary knowledge and skills to successfully implement and manage a
WordPress website on AWS EC2 using LVM storage management. Whether you're a web developer, system
administrator, or aspiring AWS DevOps professional, this course will empower you to leverage the power of AWS cloud
infrastructure to build scalable and reliable WordPress sites. Join us on this transformative journey into the world of
WordPress and AWS EC2, and unlock the potential to create and manage dynamic websites with confidence. Enroll now
and take the first step towards mastering WordPress and AWS integration with LVM storage management.

# Understanding 3 Tier Architecture
## Web Solution With WordPress
You are progressing in practicing to implement web solutions using different technologies. As a DevOps engineer you
willmost probably encounter [PHP](https://www.php.net/)-based solutions since, even in 2021, it is the dominant web programming language
used by more websites than any other programming language.
In this project you will be tasked to prepare storage infrastructure on two Linux servers and implement a basic web
solution using [WordPress](https://en.wikipedia.org/wiki/WordPress). WordPress is a free and open-source content management system written in PHP and paired
with MySQL or MariaDB as its backend Relational Database Management System (RDBMS).
Project 6 consists of two parts:

1. Configure storage subsystem for Web and Database servers based on Linux OS. The focus of this part is to g
you practical experience of working with disks, partitions and volumes in Linux.

2. Install WordPress and connect it to a remote MySQL database server. This part of the project will solidify yo
skills of deploying Web and DB tiers of Web solution.

As a DevOps engineer, your deep understanding of core components of web solutions and ability to troubleshoot
will play essential role in your further progress and development.

### Three-tier Architecture
Generally, web, or mobile solutions are implemented based on what is called the Three-tier Architecture.
Three-tier Architecture is a client-server software architecture pattern that comprise of 3 separate layers.

![text](WORDPRESS_LVM_IMAGES/Three_Tier.png)

1. Presentation Layer (PL): This is the user interface such as the client server or browser on your laptop.
2. Business Layer (BL): This is the backend program that implements business logic. Application or Webserver
3. Data Access or Management Layer (DAL): This is the layer for computer data storage and data access. [Database
Server](https://www.computerhope.com/jargon/d/database-server.htm) or File System Server such as FTP server, or [NFS Server](https://www.techtarget.com/searchenterprisedesktop/definition/Network-File-System)

In this project, you will have the hands-on experience that showcases Three-tier Architecture while also ensuring that
the disks used to store files on the Linux servers are adequately partitioned and managed through programs such as
`gdisk` and `LVM` respectively.
You willbe working working with several storage and disk management concepts, to have a better understanding, watch
following video: Disk management in Linux
Note: We are gradually introducing new AWS elements into our solutions, but do not be worried if you dò not fully
understand AWS Cloud Services yet, there are Cloud focused projects ahead where we will get into deep details of
various Cloud concepts and technologies- not only AWS, but other Cloud Service Providers as well.
Your 3-Tier Setup
1. A Laptop or PC to serve as a client

2. An EC2 Linux Server as a web server (This is where you will install Wordpress)
3. An EC2 Linux server as a database (DB) server.

Use `RedHat` OS for this project.

By now you should know how to spin up an EC2 instanse on AWS, but if you forgot - refer to [Project1 Step 0](). In previous
projects we used 'Ubuntu', but it is better to be well-versed with various Linux distributions, thus, for this projects we willuse very popular distribution called [RedHat](https://www.redhat.com/en) (it also has a fully compatible derivative - [CentOS](https://www.centos.org/)

Note: for Ubuntu server, when connecting to it via SSH/Putty or any other tool, we used buntu user, but for RedHat
you will neèed to use c2-user user. Connection string will look like ec2-user@kPublic-IPs
Let us get started!
Instructions On How To Submit Your Work For Review And Feedback
To submit your work for review and feedback - follow this instruction.

# Implementing LVM on Linux servers (Web and Database servers)

#### Step 1- Prepare a Web Server

1. Launch an EC2 instance that will serve as "Web Server", Create 3 volumes in the same AZ as your Web Server
EC2,each of 10 GiB

Learn How to Add EBS Volume to an EC2 instance here

![](WORDPRESS_LVM_IMAGES/Create_Volumes.png)