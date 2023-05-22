### LAMP Implementation

![Instance Created](/Images/lamp.png)

[] Install APache

#update a list of packages in package manager

`sudo apt update`

#run apache2 package installation

`sudo apt install apache2`

[] To verify

`sudo systemctl status apache2`

[] To check 

``

curl http://localhost:80

or

curl http://127.0.0.1:80 

``

[]Open on Browser

http://3.14.130.129:80

[]Open

![Site confirmed](/Images/site.png)

## Installing MYSQL

[]Install MYSQL

`sudo apt install mysql-server`

![Mysql done](/Images/mysql.png)

[]login

`sudo mysql`

![Mysql environment](/Images/env.png)

## Instal PHP

`sudo apt install php libapache2-mod-php php-mysql`

![PHP Installed](/Images/php.png)

[]Confirm all three packages

`php -v`

![PHP done](/Images/php-done.png)

## Create a virtaul Host for your website on APache

[]Create directory Projectlamp

`sudo mkdir /var/www/projectlamp`

[]Assign ownership to current user

`sudo chown -R $USER:$USER /var/www/projectlamp`

[]Create and Open a new configuration file in Apache's sites-available using vi line editor

`sudo vi /etc/apache2/sites-available/projectlamp.conf`

[]Insert

``
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

``
-Save File with Ese,:wq and enter

[]Confirm new file

`sudo ls /etc/apache2/sites-available`

![sites-available](/Images/sites-avail.png)

[]Reload systemctl

`sudo systemctl reload apache2`

[]use a2ensite command to enable the new virtual host:

`sudo a2ensite projectlamp`

[]Disable default site that comes with apache2

`sudo a2dissite 000-default`

[]Run

`sudo apache2ctl configtest`

[]Reload apache2

`sudo systemctl reload apache2`

[]Create an index file

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

[]Open Browser

http://3.14.130.129:80

![Reloaded](/Images/reloaded.png)

[]Rename index.html file to index.php

`sudo mv /var/www/projectlamp/index.html /var/www/projectlam/index.php`

[]Confirm index.html removed

`sudo ls /var/www/projectlamp`

## Enable PHP on the Website

[]edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

`sudo vim /etc/apache2/mods-enabled/dir.conf`

[]Change the order

`` 
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
``

[]Reload apache2

`sudo systemctl reload apache2`

[]CReate index.php inside your web root folder

`sudo vim /var/www/projectlamp/index.php`

[]Type this

``

<?php
phpinfo();

``
[]View site

![Site viewed](/Images/index.png)

[]Remove file

`sudo rm /var/www/projectlamp/index.php`
