# Web Stack Implementation (LempStack)

 This comprehensive course/project takes us through a hands-on
adventure, guiding us step-by-step in harnessing the power of Linux, Nginx, MySQL, and PHP to create dynamic and
high-performing websites. We will dive into the architecture of the LEMP stack, understanding how Linux provides a
solid foundation, Nginx serves as a powerful web: server, MySQL handles the databases, and PHP empowers: server- side
functionality.
Throughout the course/project, we will set up a Linux environment, configure Nginx for optimal performance, manage
MySQL databases, and develop PHP code to bring applications tolife. Through the practical and hands-on exercises, you
willgain proficiency in building dynamic websites with the LEMP stack. We will explore techniques for handling user
requests,interacting with databases, processing forms, and implementing robust security measures. Furthermore,
introduce us to popular development frameworks and tools that can elevate our productivity and simplify the web
application development process.

Lunch Gitbash and run the following command.

 `ssh -i "devops.pem" ubuntu@ec2-16-171-168-230.eu-north-1.compute.amazonaws.com`

 ![lunch ubuntu from AWS](LEMPSTACK_IMAGES/1stack.png)

 # Installing the Nginx Web Server
### Step 1- Installing the Nginx Web Server
In order to display web pages to our site visitors, we are going to employ Nginx, a high-performance web server. Well
use the apt package manager to install this package.

Since this is our first time using `apt` for this session, start off by updating your server's package index. Following that,
you can use apt install to get Nginx installed:

`sudo apt update`
 ![application update](LEMPSTACK_IMAGES/2update.png)

`sudo apt install nginx`

 ![NGINX INSTALLATION](LEMPSTACK_IMAGES/2install.png)

When prompted, enter
to confirm that you want to install Nginx. Once the installation is finished, the Nginx web
server will be active and running on your Ubuntu 20.04 server.
To verify that nginx was successfully installed and is running as a service in Ubuntu, run:

`sudo systemctl status nginx`

 ![NGINX INSTALLATION](LEMPSTACK_IMAGES/3status.png)

If it is green and running, then you did everything correctly -you have just launched your first Web Server in the Clouds!

Let us check how we can access it from Ubuntu shell.

`curl http://localhost:80`

![localhost](LEMPSTACK_IMAGES/4local.png)

or

`curl http://127.0.0.1:80`

![Loopback address](LEMPSTACK_IMAGES/4loopback.png)

These 2 commands above actually do pretty much the same - they use `curl` command to request our Nginx on port 80
(actually you can even try to not specify any port - it will work anyway). The difference is that: in the first case we try to
access our server via DNS name and in the second one - by IP address (in this case IP address 127.0.0.1 corresponds to
DNS name'localhost' and the process of converting a DNS name to lP address is called "resolution"). We will touch DNS
in further lectures and projects.

As an output you can see some strangely formatted test, do not worry, we just made sure that our Nginx web service
responds to `curl` command with some payload.
Now it is time for us to test how our Nginx server can respond to requests from the Internet. Open a web browser of
your choice and try to access following url

`http://<16.171.168.230>:80`

![Loopback address](LEMPSTACK_IMAGES/5awsip.png)

Another way to retrieve your Public IP address, other than to check it in AWS Web console, is to use following
command:

`curl http://169.254.169.254/latest/meta-data/public-ipV4`

![Loopback address](LEMPSTACK_IMAGES/5webnginx.png)

# Installing MySQL
### Step 2-Installing MySQL
Now that you have a web server up and running, you need to install a Database Management System (DBMS) to be able
to store and manage data for your site in a relational database. MySQL is a popular relational database management
system used within PHP environments, so we will use it in our project.
Again,use 'apt' to acquire and install this software:

`sudo apt install mysql-server`

![Loopback address](LEMPSTACK_IMAGES/6installsql.png)

When prompted,confirm installation by typing
and then ENTER
When the installation is finished, log in to the MySQL console by typing:

`sudo mysql`
![Loopback address](LEMPSTACK_IMAGES/6loginsql.png)

This will connect to the MySQL server as the administrative database user root, which is inferred by the use of `sudo` when running this command. You should see output like this:

![Loopback address](LEMPSTACK_IMAGES/6loginsql.png)

It's recommended that you run a security script that comes pre-installed with MySQL. This script will remove some
insecure default settings and lock down access to your database system. Before running the script you willset a
password for the root user, using mysql_native_password as default authentication method. We're defining this user's
password as PassWord.1

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1";`

![Loopback address](LEMPSTACK_IMAGES/6altersql.png)

Exit the MySQL shell with:

`mysql> exit`

![Loopback address](LEMPSTACK_IMAGES/6exitsql.png)

Start the interactive script by running:

`sudo mysql secure _installation`

![Loopback address](LEMPSTACK_IMAGES/6sqlpassword.png)

This will ask if you want to confgure the VALIDATE PASSWORD PLUGIN'

Note: Enabling this feature is something of a judgment call If enabled, passwords which don't match the specified
criteria will be rejected by MySOL with an error. It is safe to leave validation disabled, but you-should always use strong,
unique passwords for database credentials.
Answer foryes, or anything else to continue without enabling.

*VALIDATE PASSWORD PLUGIN can be used to test passwords and improve security. It checks the strength of password
and allows the users to set only those passwords which are secure enough. Would you like to setup VALIDATE PASSWORD plugin?*

`Press y|Y for Yes, any other key for No:`

If you answer "yes", you'll be asked to select a level of password validation. Keep in mind that if you enter
2 for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words e.g PassWord.1

*There are three levels of password validation policy:
LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file
Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1*

Regardless of whether you chose to set up the V ALIDATE PASSMORD PLUGIn , your server will next ask you to select and
confirm a password for the MySQL root user. This is not to be confused with the system root. The database root user is
an administrative user with fullprivileges over the database system. Even though the default authentication method for
the MySQL root user dispenses the use of a password, even when one is set, you should define a strong password here
as an additional safety measure. We'll talk about this in a moment.
If you enabled password validation. you'll be shown the password strength for the root password you just entered and
your server will ask if you want to continue with that password. If you are happy with your current password, enter
for "yes" at the prompt:

*Estimated strength of the password: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No)*

For the rest of the questions, press
and hit the ENTER key at each prompt. This will prompt you to change the root
password. remove some anonymous users and the test database, disable remote root logins, and load these new rules so
that MySOL immediately respects the changes you have made.
When you'refnished. test if you're able to log in to the MXSQL console by typing:

`sudo mysql -p`

![Loopback address](LEMPSTACK_IMAGES/6sqlpromptpassword.png)

Notice the `-p` flag in this command, which will prompt you for the password used after changing the root user
password.

To exit the MySQL console, type exit in the mysql prompt:

mysgl> `exit` 

![Loopback address](LEMPSTACK_IMAGES/6exitsql.png)


Notice that you need to provide a password to connect as the root user.
For increased security, it's best to have dedicated user accounts with less expansive privileges set up for every database, especially if you plan on having multiple databases hosted on your server.

`Note: At the time of this writing, the native MySQL PHP library mysqlnd doesn't support caching sha2_aut`

Your MySOL server is now installed and secured., Next, we willinstall PHP, the final component in the LEMP stack.

# Installing PHP
### Step 3- Installing PHP

You have Nginx installed to serve your content and MySQL installed to store and manage your data. Now you can install PHP to process code and generate dynamic content for the web server.

While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP
processing and act as a bridge between the PHP interpreter itself and the web server. This allows for a better overall
performance in most PHP-based websites, but it requires additional configuration. You'll need to install php-fpm
which stands for **PHP fastCGI process manager**  and tell Nginx to pass PHP requests to this software for processing.
Additionally. you'll need_php-mysql ,a PHP module that allows PHP to communicate with MySQL-based databases.
Core PHP packages will automatically be installed as dependencies.
To install these 2 packages at once, run:

`sudo apt install php-fpm php-mysql`

![Loopback address](LEMPSTACK_IMAGES/7phpinstall.png)

When prompted. type **Y**
and press **ENTER** to confirm installation.

You now have.your PHP components installed. Next, you will configure Nginx to use them.
# Configuring Nginx to Use PHP Processor

### Step 4 - Configuring Nginx.to Use PHP Processor

When using the Nginx web server, we can create server blocks (similar to virtual hosts in Apache) to encapsulate
configuration details and host more than one domain on a single server. In this guide, we will use **projectLEMP** as an example domain name.

On Ubuntu 20.04, Nginx has one server block enabled by default and is confgured to serve documents out of a directory at */var /www/html* .

While this works well for a single site, it can become difficult to manage if you are hosting multiple
sites. Insteadof modifying */var/www/html* we will create a directorystructure within */var/www* for the *your_domain*
website, leaving */var/www/html* in place as the default directory to be served if a client request does not match any
other sites.

Create the root web directory for your_domain as follows:

`sudo-mkdir /var/www/projectLEMP`

![Loopback address](LEMPSTACK_IMAGES/8mkdir.png)


Next, assign ownership of the directory with the $USER environment variable, which will reference your current system
user:

`sudo chown $USER:$USER /yar/www/projectLEMP`

![Loopback address](LEMPSTACK_IMAGES/8chown.png)

Then, open a new configuration file in Nginx's *sites- available* directory using your preferred command-line editor.
Here,w will use `nano`

`sudo nano /etc/nginx/sites-available/projectLEMP` 

![Loopback address](LEMPSTACK_IMAGES/9edit%20projectLEMP.png)

This will create a new blank file. Paste in the following bare-bone configuration.

`#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
`


![Loopback address](LEMPSTACK_IMAGES/9nano.png)

Here's what each of these directives and location blocks do:

**listen** -Defines what port Nginx will listen on. In this case, it will listen on port `80`; the default port for HTTP.

**root**  Defines the document root where the files served by this website are stored.

**index** - Defines in which order Nginx will prioritize index files for this website. Iit is a common practice to list.

**index.html** files with ahigher precedence than *index.php* files to allow for quickly setting up a maintenance landing page in PHP applications. You can adjust these settings to better suit your application needs.

**server_name** - Defines which domain names and/or IP addresses this server block should respond for. Point
this directive to your server's domain name or public IP address.

**location /** -The first location block includes a *try_files* directive, which checks for the existence of files or directories matching a URl request. If Nginx cannot find the appropriate resource, it will return a 404 error.

**location . phps** - This location block handles the actual PHP processing by pointing Nginx to the fastcgi-
php.conf configuration file and the *php7.4 fpm-sock file*, which declares what socket is associated with *php-
fpm*.

**`location ~ /\.ht`** The last location block deals with *htaccess* files, which Nginx does not process. By
adding the deny all directive, if any *htaccess* files happen to find their way into the document root.,they will
not be served to visitors.

When you're done editing, save and close the file. If you're using `nano` you can do so by typing `CTRL+X` and then `y`
and `ENTER`to confirm.
Activate your configuration by linking to the config file from Nginx's tes-enabled directory:

`sudo ln -s /etc/nginx/sites-available/projectLEMP./etc/nginx/sites-enabled/`

![Link NGINX sites](LEMPSTACK_IMAGES/9linkfile.png)

This will tell NGINX to use the configuration nct time it is reloaded, you can test your configuration for syntax errors by

` sudo nginx -t`

![Syntax checks](LEMPSTACK_IMAGES/9test.png)

To Unlink

`sudo unlink /etc/nginx/sites-enabled/default`

![Syntax checks](LEMPSTACK_IMAGES/9unlink.png)

To reload again to confirm changes

`sudo systemctl reload nginx` 

![Syntax checks](LEMPSTACK_IMAGES/9reload.png)

Your new website is now active, but the web root */var/www/projectLEMP* is still empty. Create an index.html file in that
location so that we can test that your new server block works as expected:

`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname`

Now go to your browser and try tom open your website URL using IP address.

`http://<16.171.168.230>:80`



If you see the text from 'echo' command you wrote to index.h![Syntax checks](LEMPSTACK_IMAGES/9workingnginx.png)
tml file, then it means your Nginx site is working as
expected. In the output you will see your server' 's public hostname(DNS name) and public IP address. You can also
access your website in your browser by public DNS name, not only by IP - try it out, the result must be the same (portis
optional)

`nttp:// <Public=DNS-Name>;80`

![Syntax checks](LEMPSTACK_IMAGES/9dns.png)

You can leave this file in place as a temporary landing page for your. application until you set up an *index.php* file to
replace it. Once you do that, remember to remove or rename the index.html fle from your document root, as it would
take precedence over an index. php file by default.

# Testing PHP with Nginx
### Step 5 - Testing PHP with Nginx

Your LEMP stack should now be completely set up
At this point, your LAMP stack is completely installed and fully operational.

You can test it to validate that Nginx can correctly hand
php files off to your PHP processor.

You can do this by creating a test PHP file in your document root. Open a new file called nfolphe within your
document root in your text editor:

`nano /var/www/projectLEMP/info.php`

![Syntax checks](LEMPSTACK_IMAGES/10infophp.png)

Type or paste the following lines into the new file. This is valid PHP code that will return information about your server:

'<?php 

phpinfo();

'
![php tags](LEMPSTACK_IMAGES/10phptags.png) 

You can now access this page in your web browser by visiting the domain name.or public IP address you 've setup in your nginx configuration file followed by `/info.php`

`http://server_domain_or_IP/info.php`

![php info page](LEMPSTACK_IMAGES/10phpserverpage.png)


It is a best practice to remove the file created since it hs a sensitive information. So to remoe it simply run the commnd below:

`sudo rm /var/www/your_domain/info.php`

![remove info.php](LEMPSTACK_IMAGES/10rmphp.png)

# Retrieving data from MySQL database with PHP
### Step 6 - Retrieving data from MySQL database with PHP
In this step you will create a test database (DB) with simple "To do list" and configure access to it, so the Nginx website
would be able to query data from the DB and display it.

At the time of this writing, the native MySQL PHP library mysqlnd doesn't support caching_ sha2_authentication
the default authentication method for MySQL 8. We'll need to create a new user with the mysql native_password
authentication method in order to be able to connect to the MySQL database from PHP.

We will create a database named example_database and auser named example_user,but you can replace these names
with different values.

First, connect to the MySQL console using the root account:

`sudo mysql`

![Sql login](LEMPSTACK_IMAGES/6loginsql.png)

To create a new database, run the following command from your MySQL console:

`mysql> CREATE DATABASE`

![sql database creation](LEMPSTACK_IMAGES/11createdb.png)

Now you can create a new user and grant him full privileges on the database you have just created.

The following command creates a new.user named example user , using mysql_native_password as default
authentication method. We're defining this user's password as *PassWord. 1* , but you should replace this value with a
secure password of your own choosing.

`mysql> CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1'`

![Sql user creation](LEMPSTACK_IMAGES/11createuser.png)


Now we need to give this user permission over the example database database:

`mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';`

![grant acces in sql database](LEMPSTACK_IMAGES/11grant.png)


This will give the example_user user full privileges over the example_database database, while preventing this user
from creating or modifying other databases on your server.
Now exit the MySQL shell with:

`mysql> exit`

![Sql exit](LEMPSTACK_IMAGES/11exit.png)

You can test if the new user has the proper permissions by logging in to the MySQL console again, this time using the custom user credentials.

`mysql -u example_user -p`

This is simply used when you -p to prompt you for password used when creating the example_user user.

![login sql with password](LEMPSTACK_IMAGES/11rootswitch.png)


To display the database created.

`show databases;`

![show databases in sql](LEMPSTACK_IMAGES/11showdb.png)

Next, we'll create a test table named todo list. From the MySQL console, run the following statement:

`CREATE TABLE example_ database.todo_list (item id INT AUTO_INCREMENT, content VARCHAR(255),PRIMARY KEY(item_id));`

![create tables in sql](LEMPSTACK_IMAGES/11createtable.png)


Insert a few rows of content in the test table. You might want to repeat the next command S few times, using different
VALUES:


`mysql> INSERT INTO example database.todo list (content) VALUES ("My first important item");`

![Sql insert](LEMPSTACK_IMAGES/11insert.png)



To confirm that the data was successfully saved to your table, run:

`mysql> SELECT FROM example database.todo list`

![Select from syntax](LEMPSTACK_IMAGES/11select.png)


You will see the following output:

![SQL SELECT](LEMPSTACK_IMAGES/11select2.png)

After confirming that you have valid data in your test table, you can exit the MySQL console:

`mysql> exit`

![exit](LEMPSTACK_IMAGES/11exit2.png)

Now you can create a PHP script that will connect to MySQL and query for your content. Create a new PHP file in your
custom web root directory using your preferred editor. We'll use vi for that:

`nano /var/www/projectLEMP/todo_list.php`

The following PHP script connects to the MySQL database and quelyes for the content of the todo_list table, displays
the results in a list. If there is a problem with the database connection, it will throw an exception.
Copy this content into your todo list.php script:

![nano pages edited](LEMPSTACK_IMAGES/11phpeditnano.png)

Save and close the file when you are done editing.

You can now access this page in your web browser by visiting the domain name or public IP address configured for your website, followed by `/todo_list.php`

`http://<Public_domain_or_IP>/todo_list.php`

![todo list implemented](LEMPSTACK_IMAGES/11browsetodolist.png)




















