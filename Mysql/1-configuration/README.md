# <p align="center"> Learn the general tools and configurations of a MySQL Server </p>

<p align="center"> 
	This is Part I of a short two part series on learning MySQL. 
	The second part can be seen <a <a href = "../2-queries/README.MD">here</a>.
</p>

<p align="center"> 
	This README will go over the general commands of installing and uninstalling MySQL, creating users and granting privelages to them, 
	seeing SSL related variables, etc. All in all, this readme is just a quick guide on how to utilize MySQL to fit the users needs.
</p>



<br></br>
## <p id = "toc"> Table of Contents </p>
1. [General MySQL Installation](#general)
2. [Users & Privelages](#users)
3. [SSL related goods](#ssl)
4. [Access MySQL on a remote server](#remote-access)



<br></br>
## <p align="center" id = "general"> General MySQL Installation | [Back to ToC](#general) 
</p>

### See if MySQL is installed
`shell> mysql` or <br> `shell> mysql --version`
or <br> `shell> mysql -V` 	

Results of command when ran locally vs on a VPS, 
> mysql  Ver 8.0.20-0ubuntu0.20.04.1 for Linux on x86_64 ((Ubuntu))

> mysql  Ver 14.14 Distrib 5.7.19, for Win64 (x86_64)

### Install MySQL
` sudo apt install mysql-server `

### How to uninstall & remove MySQL completely
```
> sudo apt-get remove --purge *mysql\*
> sudo apt-get autoremove
> sudo apt-get autoclean
```
[Source](https://askubuntu.com/questions/640899/how-do-i-uninstall-mysql-completely)

### Login via localhost
` mysql -u root -p -h localhost `

### Login MySQL server for Win64 via Git Bash
` winpty mysql -u root -p `

### Login via TCP protocol
` mysql -u root -p -h127.0.0.1 --protocol=TCP `

### Login via domain/IP address
` shell> mysql -u raza -p -h 168.235.86.169 `

### Restart MySQL service
` service mysql restart `

### Check Port MySQL running on (Default is 3306)
` mysql> SHOW GLOBAL VARIABLES LIKE 'PORT'; `

### Check Active Internet Connections (like TCP)
` sudo netstat -plunt `

One line of the output draws interest:
> tcp     0     0 0.0.0.0:3306     0.0.0.0:*     LISTEN     5858/mysqld

### Check status (used for SSL too)
` mysql> status ` or <br>
` mysql> \s `

### Best way to display SELECT query with many columns?
` Select * from mysql.user WHERE user='root'\G `

See the difference between the statement above and this one:
` Select * from mysql.user WHERE user='root'; `

> General format: 
> > SELECT * FROM sometable\G
[Source](https://stackoverflow.com/questions/924729/how-to-best-display-in-terminal-a-mysql-select-returning-too-many-fields)


### Show databases
` mysql> show databases; ` <br> <br>
An alternative way is: <br>

> shell> mysqlshow  
> [Source](https://dev.mysql.com/doc/refman/8.0/en/mysqlshow.html)


### Where MySQL bin folder is located (WAMP Server)
` C:\wamp64\bin\mysql\mysql5.7.19\bin `

### Mysqld
` shell> which mysqld `
 
###	See if MySQL is running
` shell> ps -Af | grep mysqld `





<br></br>
## <p align="center" id = "users"> Users & Privelages| [Back to ToC](#ToC)
</p>

### See Users
SELECT user FROM mysql.user\G

### See Users and Hosts
SELECT user, host FROM mysql.user\G

### See Current Mysql User
SELECT USER(),CURRENT_USER();

### Delete User
DELETE FROM mysql.user WHERE user = 'raza';

### Update host for mysql.user
UPDATE mysql.user SET host='%' WHERE user='raza';

```
GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';

GRANT ALL PRIVILEGES ON books.authors  TO 'tolkien'@'localhost';

GRANT ALL PRIVILEGES ON *.* TO 'tolkien'@'%';
```

If you have the following issue:
`Access denied for user 'raza'@'localhost' (using password: NO)`
<br>Run:
`grant all privileges on *.* to raza@localhost with grant option;`





<br></br>
## <p align="center" id = "ssl"> SSL Related Goods | [Back to ToC](#ToC) 
</p>

### Connect to MySQL client without SSL
` mysql -h <hostname> -u <username>  -p –ssl-mode=DISABLED `

### Check status (used for SSL too)
` mysql> status ` or <br>
` mysql> \s `

### See SSL variable/parameter
`SHOW VARIABLES LIKE '%ssl%'`

```
+--------------------+-----------------+
| Variable_name      | Value           |
+--------------------+-----------------+
| have_openssl       | YES             |
| have_ssl           | YES             |
| mysqlx_ssl_ca      |                 |
| mysqlx_ssl_capath  |                 |
| mysqlx_ssl_cert    |                 |
| mysqlx_ssl_cipher  |                 |
| mysqlx_ssl_crl     |                 |
| mysqlx_ssl_crlpath |                 |
| mysqlx_ssl_key     |                 |
| ssl_ca             | ca.pem          |
| ssl_capath         |                 |
| ssl_cert           | server-cert.pem |
| ssl_cipher         |                 |
| ssl_crl            |                 |
| ssl_crlpath        |                 |
| ssl_fips_mode      | OFF             |
| ssl_key            | server-key.pem  |
+--------------------+-----------------+
```

GREAT SSL related links to learn more from.

[DigitalOcean Source1](https://www.digitalocean.com/community/tutorials/how-to-configure-ssl-tls-for-mysql-on-ubuntu-16-04),
[DigitalOcean Source2](https://www.digitalocean.com/community/questions/is-it-possible-remote-access-mysql-via-standard-tcp-on-workbench-without-ssh)
and
[How to disable SSL Source3](https://serverfault.com/questions/770618/how-to-disable-ssl-plugin-on-mysql-5-7-server)





<br></br>
## <p align="center" id = "remote-access"> Access MySQL on a remote server  | [Back to ToC](#ToC) 
</p>


### General Resources:
[MySQL Dev Resource 1](https://dev.mysql.com/doc/refman/5.7/en/using-encrypted-connections.html)

[Stack Overflow Resource 2](https://stackoverflow.com/questions/10299148/mysql-error-1045-28000-access-denied-for-user-billlocalhost-using-passw/39842128)

[Blog Resource 3](https://tecadmin.net/create-user-in-mysql-with-full-privileges/)



### Remote into MySQL process
This short section will go over how to connect to a remote MySQL service.

DISCLAIMER: 
Your local computer and remote server must have MySQL installed. Additionally, if your server is using MySQL 8.0+, make sure your local version is up to date! 

When I initially tried to remote into a server via the command line. The server holds MySQL Ver 8.0.20 and my local computer MySQL Distrib was 5.7.19. Obviously, 5.7 does NOT match with version 8 and I got this error when I tried to connect with the command:

` shell> mysql -u raza -p -h 168.235.86.169 `

> ERROR 2026 (HY000): SSL connection error: unknown error number

Now, to solve the problem I updated the local mysql server to version 8.

I followed [this link](https://www.percona.com/blog/2018/05/14/installing-mysql-8-on-ubuntu-16-04-lts/) and was able to connect to it. The commands I used were as follows:

```
wget https://dev.mysql.com/get/mysql-apt-config_0.8.10-1_all.deb

dpkg -i mysql-apt-config_0.8.10-1_all.deb

THEN 

apt-get update 
apt-get install mysql-server
```

Now, I figured this out by reading [this Digital Ocean resource](https://www.digitalocean.com/community/questions/can-t-connect-to-mysql-instance-in-managed-databases).

A user named Bobby commented: 

> Regarding the MySQL cli, as far as I know on OSX the default MySQL client is 5.7 and you can not use MySQL 5.7 client to connect toMySQL 8. I tested that and I’m getting the same SSL error as you do when using MySQL 5.7 client...
> <br><br> Let me know how it goes! <br>
Regards, <br>
Bobby

Now that we have matching MySQL versions, lets begin.










<!-- =======================================================================================================================================================================================================================-->










+------------------+
### First, make sure your bind-address is configured to listen to hosts other than local. 

Open the mysql config file.

> $ nano /etc/mysql/my.cnf

OR <br>

> $ nano /etc/mysql/mysql.conf.d/mysqld.cnf 

Comment out the bind address that only listens to localhost

> #bind-address = 127.0.0.1 

Go one line below where that line was found and add this:

> bind-address = 0.0.0.0

[Source](https://www.tecmint.com/fix-error-2003-hy000-cant-connect-to-mysql-server-on-127-0-0-1-111/)



---------------------------

### Now, let's create a user.

Make sure that when you create the user, you specify % as the hostname, otherwise the user will only be able to connect from the localhost.

Create User accessible locally <br>
` CREATE USER raza@localhost IDENTIFIED BY 'pass'; ` 

Create User which can be remoted in <br>
` CREATE USER raza@'%' IDENTIFIED BY 'pass'; `

#### Once the user is created, grant them privelages

` GRANT ALL PRIVILEGES ON *.* to raza@'%' WITH GRANT OPTION; `

> Following statement indicates that the account has no SSL or X.509 requirements. [Source](https://dev.mysql.com/doc/refman/5.6/en/grant.html)

`grant all on *.* to raza@'%' REQUIRE NONE;`

#### After privileges have been set, run two more commands

Reload the permissions
` FLUSH PRIVILEGES; `

Restart the service
` service mysql restart `

After that has been done, you should be able to have remote into the server.