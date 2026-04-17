# Public-Architecture-Configuration-Installation-and-Security-of-OpenEMR

This Project was focused on installing, configuring, and protecting the Open EMR in terms of security through the virtual machines created for the different hospitals

OpenEMR is a widely used, open-source EHR and medical practice management software system designed to streamline and digitize the workflows of healthcare providers. Its comprehensive feature set includes patient scheduling, billing, clinical decision support, reporting, and a customizable patient portal.

# Code used for configuration and Installation of OpenEMR on Linux
-------- used to install and upgrade package list first
sudo apt-get update
sudo apt-get upgrade

------- Install the LAMP stack (Linux, Apache, MySQL, PHP) 
sudo apt-get install apache2 mysql-server php libapache2-mod-php php-mysql php-gd php-xml
php-mbstring php-json php-zip php-soap php-curl

--------- Secure your MySQL installation
sudo mysql_secure_installation

-----------Create a MySQL database and user for OpenEMR:
sudo mysql -u root -p
---------Create a new database and user:
CREATE DATABASE openemr;
CREATE USER 'yourusername'@'localhost' IDENTIFIED BY 'P@ssw0rd';
GRANT ALL PRIVILEGES ON openemr.* TO 'yourusername'@'localhost';
FLUSH PRIVILEGES;
EXIT;

-------- Download version 6.0.0 of OpenEMR:
Open the Firefox browser on your VM, copy and paste this link, then wait a few seconds to download
https://sourceforge.net/projects/openemr/files/OpenEMR%20Current/6.0.0/openemr-
6.0.0.tar.gz/download
------- Navigate to Downloads on the terminal;
cd Downloads
------- Extract the downloaded archive:
sudo tar -xvzf openemr-6.0.0.tar.gz
------- Rename the extracted folder to 'openemr':
sudo mv openemr-6.0.0 openemr
------ Move the renamed openemr to html
sudo mv openemr /var/www/html/
------ Change to the '/var/www/html' directory:
cd /var/www/html
------ Check if openemr is present:
ls

------- Change the ownership and permissions of the 'openemr' folder:
sudo chown -R www-data:www-data openemr
sudo chmod -R 755 openemr
-------- Configure Apache:Create a new Apache configuration file for OpenEMR:
sudo nano /etc/apache2/sites-available/openemr.conf
the following lines to the file, then save and exit (Ctrl+X, Y, Enter):
<VirtualHost *:80>
ServerAdmin yourmtuemailaddress
DocumentRoot /var/www/html/openemr
ServerName vmipaddress
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
-------- Enable the new OpenEMR site and disable the default site:
sudo a2ensite openemr
sudo a2dissite 000-default
-------- Enable the Apache 'rewrite' module:
sudo a2enmod rewrite
-------- Restart Apache:
sudo systemctl restart apache2
-------- Complete OpenEMR installation via the web-based setup.
 Open your web browser and navigate to http://vmipaddress


 ## The above code is used to describe the process of installing and configuring the OpenEMR on the virtual machines:

 One of the key challenges with this project was troubleshooting each code to understand why it was not running, and with the help of the
 OpenEmr documentation, I was able to fix the problems and use additional support from LLM models.

 Additionally, the kinds of possible attacks the systems go through, such as ransomware, were discussed, and how to mitigate them.


