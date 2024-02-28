# Implementing Loadblancers with Nginx

Discover the art of load balancing with Nginx in this project. Learn how to distribute traffic efficiently across multiple
servers, optimize.performance, and ensure high availability for your web applications

## Introduction to Load Balancing and Nginx
Introduction to Load Balancing and Nginx

![Images](Load_balancer_Images/LB_Diagram.png)


Load balancing is like having a team of helpers working together to make sure a big job gets done smoothly and
efficiently. Imagine you have a lot of heavy boxes to carry, but you can't carry them all by yourself because they are too
heavy.
Load balancing is when you call your friends to help you carry the boxes. Each friend takes some of the boxes and carries
them to the right place. This way, the work gets done much faster because everyone is working together.
In computer terms, load balancing means distributing the work or tasks among several computers or servers so that no
one computer gets overloaded with too much work. This helps to keep everything running smoothly and ensures that
websites and apps work quickly and don't get too slow. It's like teamwork for computers!
Lets say you have a set of webservers serving a serving your website. In other to distribute the traffic evenly between
the webservers, a load balancer is deployed. The load balancer stands in front of the webservers, all traffic gets to it first,
it then distributes the traffic across the set of webservers. his is to ensure no webserver get over worked, consequently
improving system performance.
ec.
To..
rse
Nginx is aversatile software, it can act like a webserver, reverse proxy, and a load balancer etc. All that is needed is to
confgure it properly to server your use case.
In this project we will be wor king you through how to configure Nginx as a load balancer.


Setting Up a Basic Load Balancer
Setting Up a Basic Load Balancer
We are going to be provisioning two EC2 instances running ubuntu 22.04 and install apache webserver in them. We will
open port 8000 to allow traffic from anywhere, and finaly update the default page of the webservers to display their
public IP address.
sec.
Next we will provision another 'EC2 instance running ubuntu, 22.04, this time we will install Nginx and configure it to act
as a load balancer distributing traffic across the webservers.
sec..
sec..
Step 1: Provisioning EC2 instance
Open your AWS Management Console, click on EC2. Sdpll down the page and click on Launch instance:
sec..
-console
(To..
Under Name, Provide a unique name for each of your webservers




Under Applications and OS Images, click on quick start and click on ubuntu:




Under Key Pair,click on create new key pair if you do not have one. You can use the same key pair for all the
instances


And finally click on Launch Instance




Step 2:Open Port 8000 We willbe running our webservers on port 8000 while the load balancers runs on port 80. We
need to open port 8000 to allow traffic from anywhere. To do this we need to add a rule to the security group of each of
our webservers
ec..
sec..
Click on the instance ID to get the details of your EC2 instance



On that same page, click on scrol down and click on securiy




Click on security group




On the top of the page click on Action andlselect Edit inbound rules:


Add your rule




Click on save rules.

Step 3: Install Apache Webserver
After provisioning both of our servers and have opened the necessary ports, Its time to install apache software on both
servers. To do so we must first connect to each of the webserver via ssh. Then we can now run commands on the
terminal of our webservers.
Connecting to the webserver: To connect to the webserver, click on your instance Id, at the top of the page click
on connect.





Next copy the ssh command below:

copy-ssh-command

Open a terminal in your local machine, cd into your Downloads folder. Paste the ssh command you copied in the
previous step



Click on enter and type yes when prompted. You should be connected to a terminal on your instance.



Next install Apache with the command below:

sudo apt update -y &&  sudo apt install apache2 -y




Verify that apache is running with the command below:

sudo systemctl status apache2


Step 4: Configure Apache to server a page showing its public IP:
We will start by configuring Apache webserver to serve content on port 8000 instead of its default which is port 80.
Then we will create a new index.html file. The file will contain code to display the public IP of the EC2 instance. We will
then override apache webserver's default html file with our new file.
Configuring Apache to Serve content on port 8000:

1. Using your text editor(eg vi, nano) open the file /etc/apache2/ports.conf
Copy Below Code
sudo vi /etc/apache2 ports.conf

2. Add a new Listen directive for port 8000: First type i to switch the editor to insert mode. Then add the
listen directive. Then save your file




3. Next open the file /etc/apache 2/sites-available/000-default.conf and change port 80 on the virtualhost to
8000 like the screenshot below:
Copy Below Code
sudo vi /etc/apache2/sites-available/000-default.conf



4. Close the file by first pressing the esc key on your keyboard then the command below:
Copy Below Code
:wqal
5. Restart apache to load the new configuration using the command below:
Copy Below Code
sudo systemctl restart apache2
Creating our new html file:
1. Open a newindex.html file with the commandlelow:
Copy Below Code
sudo vi index.html
2. Switch vi editor to insert mode and paste the html file below. Before pasting the html file, get the public IP
of your EC2 instance from AWS Management Console and replace the placeholder text for IP address in
the html file
Copy Below Code

        <!DOCTYPE html>
        <html>
        <head>
            <title>My EC2 Instance</title>
        </head>
        <body>
            <h1>Welcome to my EC2 instance</h1>
            <p>Public IP: YOUR_PUBLIC_IP</p>
        </body>
        </html>



3. Change file ownership of the index.html file with the command below:
Copy Below Code

`sudo chown www-data:www-data ./index.html`

Overriding the Default html file of Apache Webserver:

1. Replace the default html file with our new html file using the command below:

Copy Below Code

`sudo cp -f ./index.html /var/www/html/index.html`

2. Restart the webserver to load the new configuration using the command below:

Copy Below Code

`sudo systemctl restart apache2` 

3,You should find a page on the browser like so:



Step 5: Configuring Nginx as a Load Balancer
Provision a new EC2instance running ubuntu 22.04. Make sure port 80 is opened to accept traffic from
anywhere. Your can refer to step 1 through step 2 to refresh your memory.
Next SSH into the instance. Again refer to step 3 for a refresher if needed.
Install Nginx into the instance using the command below:

Copy Below Code

`sudo apt update -y && sudo apt install nginx -y`
Verify that Nginx is installed with the command below:

Copy Below Code

`sudo systemctl status nginx`




Goen Nginx configuration file with the command below:
Copy Below Code
sudo vi /etc/nginx/conf.d/loadbalancer.cont
Paste the configuration file below to configure nginx to act like a load balancer. A screenshot of an example config
file is shown below: Make sure you edit.the file and provide necessary information like your server IP address etc.

Copy Below Code

        
        upstream backend_servers {

            # your are to replace the public IP and Port to that of your webservers
            server 127.0.0.1:8000; # public IP and port for webserser 1
            server 127.0.0.1:8000; # public IP and port for webserver 2

        }

        server {
            listen 80;
            server_name <your load balancer's public IP addres>; # provide your load balancers public IP address

            location / {
                proxy_pass http://backend_servers;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            }
        }
    


addresses and ports of your backend servers. proxy. pass inside the location block: sets up the load balancing.
passing the requests to the backend servers. The proxy_ set header lines pass necessary headers to the backend
servers to correctly handle the requests
Test your configuration with the command below:

Copy Below Code

`sudo nginx -t`



If there are no errors, restart Nginx to laod the new configuration with the command below:

Copy Below Code

`sudo systemctl restart nginx`

Paste the public IP address of Nginx load balancer, you should see the same webpages served by the webservers.




# Load Balancing Algorithms
## Load Balancing Algorithms
Load balancer algorithms are techniques used to distribute incoming network traffic or workload across multiple
servers, ensuring efficient utilization of resources and improving overall system performance, reliability, and availability.
Here are some common load balancer algorithms:

1. Round Robin: This algorithm distributes requests sequentially to each server in the pool. It is simple to implement
and ensures an even distribution of traffic. It works well when all servers have similar capabilities and resources.

2. Least Connections: This algorithm routes new requests to the server with the least number of active connections.
It is effective when servers have varying capacities or workloads, as it helps distribute traffic to the least busy
server.

3. Weighted Round Robin: Similar to the Round Robin algorithm, but servers are assigned different weights based
on their capabilities. Servers with higher capacities receive more requests. This approach is useful when servers
have varying capacities or perfamance I levels.

4. Weighted Least Connections: Similar to the Least Connections algorithm, but servers are assigned different
weights based on their capabilities. Servers with higher capacities receive more connections. This approach
balances traffic based on server capacities.

5. IP Hash: This algorithm uses a hash function based on the client's IP address to consistently map the client to a specific server. This ensures that the same client always reaches the same server, which can be helpful for
maintaining session data or stateful connections.

# SSL Termination and HTTPS Load Balancing
## SSL Termination and HTTPS Load Balancing
In this module we will be conniguring TLS/ SSL on our deployed website. But before doing so, let us take a brief r moment
to understand the purF pose of TLS certificate, how they work a and the technology behinde  it.

## Encryption
Encryption is at the heart of TLS/SSL. Encryption is the process of converting plain, readable data (referred to as
plaintext) into an unreadable format called ciphertext. The purpose of encryption is to ensure data confdentiality and.
protect sensitive information from unauthorized access or interception.
on.
In encryption, an algorithm (known as a cryptographic algorithm) and a secret key are used to transform the plaintext
into ciphertext. Only those who possess the correct key. can decrypt the ciphertext and convert it back into its original
plaintext form.

## Types of Encryption

Encryption can be classifed into several types based on various criteria, such as the encryption process, the key used.



