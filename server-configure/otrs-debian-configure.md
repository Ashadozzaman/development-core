# How to install OTRS (OpenSource Trouble Ticket System) on Debian 11.
OTRS is an open-source Ticket Request System that helps organizations process customer tickets and requests. It is one of the most popular service management software used for helpdesk and customer support. It offers a flexible web-based panel to track general IT-related issues from the central point. It is written in Perl and uses PostgreSQL, and MySQL as a database backend. If you are looking for helpdesks, call centers, and IT service management systems then OTRS is the best option for you.

This post will explain how to install OTRS on Debian 11 server.

### Step 1 — Installing the OTRS Package and Perl Modules
- OTRS is written in Perl, so you must install all Perl dependencies to your server.
- First, update and upgrade all the system packages using the following command.

To do this, first log into your debian server
```
ssh ashadozzaman@debian_Server_IP
```
First, update and upgrade all the system packages using the following command.
```
apt update -y
apt upgrade -y
```
Then download the source archive with the wget command. For this tutorial, you will download version 6.0.35;
```
sudo wget https://otrscommunityedition.com/download/otrs-community-edition-6.0.35.tar.gz
tar xzf otrs-community-edition-6.0.35.tar.gz
sudo mv otrs-community-edition-6.0.35 /opt/otrs
```
Because OTRS is written in Perl, it uses a number of Perl modules. Check for missing modules by using the CheckModules.pl script included with OTRS:
```
sudo /opt/otrs/bin/otrs.CheckModules.pl
```
OutPut like:
```
Output
  o Apache::DBI......................FAILED! Not all prerequisites for this module correctly installed.
  o Apache2::Reload..................ok (v0.13)
. . .
  o XML::LibXML......................Not installed! Use: 'apt-get install -y libxml-libxml-perl' (required - Required for XML processing.)
  o XML::LibXSLT.....................Not installed! Use: 'apt-get install -y libxml-libxslt-perl' (optional - Required for Generic Interface XSLT mapping module.)
  o XML::Parser......................Not installed! Use: 'apt-get install -y libxml-parser-perl' (optional - Recommended for XML processing.)
  o YAM
```

Next, install all required Perl modules on your server by running the following command:
```
sudo apt install perl libapache2-mod-perl2 libdbd-mysql-perl libtimedate-perl libnet-dns-perl libnet-ldap-perl libio-socket-ssl-perl libpdf-api2-perl libdbd-mysql-perl libsoap-lite-perl libtext-csv-xs-perl libjson-xs-perl libapache-dbi-perl libxml-libxml-perl libxml-libxslt-perl libyaml-perl libarchive-zip-perl libcrypt-eksblowfish-perl libencode-hanextra-perl libmail-imapclient-perl libtemplate-perl libmoo-perl libauthen-ntlm-perl libjavascript-minifier-xs-perl libdbd-odbc-perl libcss-minifier-xs-perl libdbd-pg-perl libdatetime-perl -y
```
After installing all the required dependencies, you can proceed to the next step.

Optional
```
sudo apt install libmoo-perl
sudo /opt/otrs/bin/otrs.CheckModules.pl
sudo apt install apache2
sudo systemctl restart apache2
```
### Step 2 — Configuring OTRS, Apache, and MySQL server
In this step, you will create a system user for OTRS, and then configure Apache and MySQL server to work with OTRS.

Create a user named otrs to run OTRS functions with the useradd command:
```
sudo useradd -d /opt/otrs -c 'OTRS user' otrs
```
`-d` sets the user’s home directory as `/opt/otrs`, and `-c` sets the 'OTRS user' comment to describe the user.

Next, add otrs to the webserver group:
```
sudo usermod -G www-data otrs
sudo cp /opt/otrs/Kernel/Config.pm.dist /opt/otrs/Kernel/Config.pm
cd /opt/otrs
sudo bin/otrs.SetPermissions.pl
```
```
Output
Setting permissions on /opt/otrs
```

Next, activate the `apache2` configuration file and make sure it is loaded after all other configurations. To do this, make a symbolic link with the `zzz_` prefix:
```
sudo ln -s /opt/otrs/scripts/apache2-httpd.include.conf /etc/apache2/sites-enabled/zzz_otrs.conf
```
OTRS requires a few Apache modules to be active for optimal operation. You can activate them via the tool a2enmod. Although some of these have already been enabled, it is a good idea to check them all:
```
sudo a2enmod perl
sudo a2enmod headers
sudo a2enmod deflate
sudo a2enmod filter
sudo systemctl restart apache2
```
Restart your web server to apply new configurations:
```
sudo systemctl restart apache2
```
#### MySql Configure
It's MYSQL 5.7 for OTRS `6.0.35`
```
sudo apt update

wget https://dev.mysql.com/get/mysql-apt-config_0.8.18-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.18-1_all.deb

sudo apt update
sudo apt install mysql-server-5.7

// If get error gnupg
sudo apt install gnupg
// If get apt-key error
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B7B3B788A8D3785C

sudo apt update

# sudo apt install mysql-server
# Sometime face some differents kinds of error

sudo systemctl start mysql.service
```

Before you go to the next step and run the web installer, change some of the MySQL configuration settings. Open the MySQL configuration file in your preferred text editor. This tutorial uses nano:
```
//It's for ubuntu
#sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf 

// It's for debian
sudo nano /etc/mysql/my.cnf  
```
Look for the following options under the [mysqld] section. For max_allowed_packet and query_cache_size, change the values to 64M and 32M respectively, as highlighted in the following code block:
```
max_allowed_packet      = 64M
thread_stack            = 192K
thread_cache_size       = 8
# This replaces the startup script and checks MyISAM tables if needed
# the first time they are touched
myisam-recover-options  = BACKUP
#max_connections        = 100
#table_open_cache       = 64
#thread_concurrency     = 10
#
# * Query Cache Configuration
#
query_cache_limit       = 1M
query_cache_size        = 32M
```
This adjusts the maximum allowed packet size and the query cache size so that MySQL can interface with OTRS.

Then add the following highlighted additional options under the [mysqld] section, at the end of the file:
```
# ssl-cert=/etc/mysql/server-cert.pem
# ssl-key=/etc/mysql/server-ikey.pem
innodb_log_file_size = 256M
collation-server = utf8_unicode_ci
init-connect='SET NAMES utf8'
character-set-server = utf8
```
This sets the database logfile size, determines the character set and collation, and creates an init_connect string to set the character set upon starting the MySQL server.

Save and close `mysqld.cnf `by pressing `CTRL + X`, followed by `Y` and then `ENTER`. Then, restart your MySQL server to apply the new parameters:
```
sudo systemctl restart mysql.service
```

Now Create Mysql User and Crendtial
```

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Start@123';
// INSTALL PLUGIN auth_socket SONAME 'auth_socket.so';
ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;

ALTER USER 'otrs'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Start@123';
CREATE USER 'otrs'@'localhost' IDENTIFIED WITH mysql_native_password BY ' Start@123';

// Check user
SELECT user FROM mysql.user WHERE user='otrs';

ALTER USER 'otrs'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

GRANT CREATE, ALTER, DROP, INSERT, UPDATE, INDEX, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'otrs'@'localhost' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON *.* TO 'otrs'@'localhost' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON otrs.* TO 'otrs'@'localhost';
FLUSH PRIVILEGES;
exit
systemctl status mysql.service
```
## Step 3 — Using the Web Installer
In this step, you will configure OTRS’s database settings in a web browser and start the OTRS daemon process on the command line.

Open` https://example.com/otrs/installer.pl `in your favorite web browser, replacing `example.com` with your domain name. You will find a welcome screen with the message Welcome to OTRS 6 and information about the OTRS offices.


## Optional If Need Migration
Some common error solution show here:-
- `Error 2020: Got packet bigger than 'max_allowed_packet' bytes when dumping table `article_data_mime_attachment` at row: 16048`

```
// solution
mysqldump -u root -p --max-allowed-packet=512M otrs > otrs_backup.sql

sudo systemctl restart mysql
```