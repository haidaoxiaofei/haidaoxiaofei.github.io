---
layout: post
category: "linux"
title:  "Configure Apache Http Server"
tags: [linux]
---

Long time no see! In this article, I want to summarise some experience about configuring Apache Http Server and Firewall on Linux.

### 1. NameVirtualHost

Here I first give the configuration of my server. On the server I deployed some PHP projects under "/var/www/html/", and yesterday I deployed one docker shipped project to another place. In docker, it maps a service in a virtual machine to some port of you host OS (e.g., I map it to port 9092). Then, I need to do proxying. Here, we can see the configure file proxy the port 9092 to subdomain "/gmission".

When we use "NameVirtualHost *:80", the corresponding "<VirtualHost *:80>" block will handle the traffic of port 80. Then, we need to maintain the traffic of the PHP projects and configure the traffic for the new docker project. Here we need to leave "DocumentRoot" as "/var/www/html/", which indicates that apache will do name based access for the projects under "/var/www/html/".

	
	Listen 80

    NameVirtualHost *:80
    
    <VirtualHost *:80>
    
        ServerAdmin pchengaa@ust.hk
        DocumentRoot /var/www/html/
        ServerName http://lccpu4.cse.ust.hk
        ErrorLog logs/all-error.log
        CustomLog logs/all-access.log common
        RewriteEngine On
 
        #gmission_hkust proxy
        ProxyPass         /gmission  http://localhost:9092/ nocanon
        ProxyPassReverse  /gmission  http://localhost:9092/
        ProxyRequests     Off
        AllowEncodedSlashes Off


        <Directory /home/bigstone/www/>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride None
                Order allow,deny
                allow from all
        </Directory>
        Alias /static/ /home/bigstone/www/gmission/hkust-gmission/gmission/static/
    </VirtualHost>
	

### 2. Open port 80

After configuring the proxy for the projects, I find I cannot access them from other machine but only can do it on the server through command line browser "w3m". Then I recognise that the problem may be caused by firewall. 

I notice a command to add a policy to open port 80:
	
	
	iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
	service iptables save
	service iptables restart
	
	
However, the result is not as I expected. 
	
After a long time of searching, I find the order of the policies in iptables will make a huge difference. In my iptables policy list, it is
	
	sudo iptables -L
	
	Chain INPUT (policy ACCEPT)
	target     prot opt source               destination
	ACCEPT     all  --  anywhere             anywhere            state RELATED,ESTABLISHED
	ACCEPT     all  --  anywhere             anywhere
	ACCEPT     tcp  --  anywhere             anywhere            state NEW tcp dpt:ssh
	DROP       all  --  anywhere             anywhere
	ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:http
	
	
which means, the fifth rule to open port 80 will be blocked by the fourth rule, then I need to give rule 5 a little bit higher priority.
	
Here is the method:
	
	
	iptables -D INPUT 5 #delete rule 5 in INPUT
	iptables -I INPUT 4 -p tcp -m tcp --dport 80 -j ACCEPT #insert this as rule 4
	
	
Then, everything looks good now!
	