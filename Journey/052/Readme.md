
# MariaDB on CentOS 7 For LFCS Exam

## Introduction

This post will cover the commands for installing MariaDB (specifically ```mariadb-server``` which unlike the ```mariadb``` package includes the server and not just the client side software) and some basic commands that you'll need to know for the LFCS.

## Prerequisite

A CentOS 7 VM.

## Use Case

While I can think of many uses where it is appropriate to use databases, the LFCS does not require a very deep knowledge of databases. It only requires you to create a database, create a table, and understand the syntax for creating fields and inserting values into those fields. 

## Cloud Research

MariaDB is a fork of MySQL. At this time there doesn't appear to be a concencus among the distros for which database technology to use. For example: Ubuntu (as I understand it) uses MySQL while on CentOS it is preferable to use MariaDB. PostgreSQL is also a good alternative for Oracle related things as it supports enterprise features.

## Try yourself

Follow along and you'll be able to create more complicated databases in no-time at all. 

### Step 1 — Installing Required Packages

```
[root@centos ~]# yum install mariadb-server
Loaded plugins: fastestmirror, langpacks, product-id, search-disabled-repos, subscription-manager

This system is not registered with an entitlement server. You can use subscription-manager to register.

Loading mirror speeds from cached hostfile
 * base: mirror.calgah.com
 * extras: mirror.calgah.com
 * updates: mirror.calgah.com
base                                                                                     | 3.6 kB  00:00:00     
epel                                                                                     | 4.7 kB  00:00:00     
extras                                                                                   | 2.9 kB  00:00:00     
google-chrome                                                                            | 1.3 kB  00:00:00     
updates                                                                                  | 2.9 kB  00:00:00     
(1/3): google-chrome/primary                                                             | 1.8 kB  00:00:00     
(2/3): epel/x86_64/updateinfo                                                            | 1.0 MB  00:00:00     
(3/3): epel/x86_64/primary_db                                                            | 6.9 MB  00:00:02     
google-chrome                                                                                               3/3
Resolving Dependencies
--> Running transaction check
---> Package mariadb-server.x86_64 1:5.5.65-1.el7 will be installed
--> Processing Dependency: mariadb(x86-64) = 1:5.5.65-1.el7 for package: 1:mariadb-server-5.5.65-1.el7.x86_64
--> Processing Dependency: perl-DBD-MySQL for package: 1:mariadb-server-5.5.65-1.el7.x86_64
--> Running transaction check
---> Package mariadb.x86_64 1:5.5.65-1.el7 will be installed
---> Package perl-DBD-MySQL.x86_64 0:4.023-6.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================================================
 Package                       Arch                  Version                          Repository           Size
================================================================================================================
Installing:
 mariadb-server                x86_64                1:5.5.65-1.el7                   base                 11 M
Installing for dependencies:
 mariadb                       x86_64                1:5.5.65-1.el7                   base                8.7 M
 perl-DBD-MySQL                x86_64                4.023-6.el7                      base                140 k

Transaction Summary
================================================================================================================
Install  1 Package (+2 Dependent packages)

Total download size: 20 M
Installed size: 107 M
Is this ok [y/d/N]: y
Downloading packages:
(1/3): mariadb-5.5.65-1.el7.x86_64.rpm                                                   | 8.7 MB  00:00:01     
(2/3): perl-DBD-MySQL-4.023-6.el7.x86_64.rpm                                             | 140 kB  00:00:00     
(3/3): mariadb-server-5.5.65-1.el7.x86_64.rpm                                            |  11 MB  00:00:02     
----------------------------------------------------------------------------------------------------------------
Total                                                                           9.7 MB/s |  20 MB  00:00:02     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 1:mariadb-5.5.65-1.el7.x86_64                                                                1/3 
  Installing : perl-DBD-MySQL-4.023-6.el7.x86_64                                                            2/3 
  Installing : 1:mariadb-server-5.5.65-1.el7.x86_64                                                         3/3 
  Verifying  : 1:mariadb-server-5.5.65-1.el7.x86_64                                                         1/3 
  Verifying  : perl-DBD-MySQL-4.023-6.el7.x86_64                                                            2/3 
  Verifying  : 1:mariadb-5.5.65-1.el7.x86_64                                                                3/3 

Installed:
  mariadb-server.x86_64 1:5.5.65-1.el7                                                                          

Dependency Installed:
  mariadb.x86_64 1:5.5.65-1.el7                       perl-DBD-MySQL.x86_64 0:4.023-6.el7                      

Complete!
```

### Step 2 — Starting The Service

```
[root@centos ~]# systemctl enable --now mariadb
Created symlink from /etc/systemd/system/multi-user.target.wants/mariadb.service to /usr/lib/systemd/system/mariadb.service.
[root@centos ~]# systemctl status mariadb
● mariadb.service - MariaDB database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2020-10-01 15:22:40 CDT; 4s ago
  Process: 3618 ExecStartPost=/usr/libexec/mariadb-wait-ready $MAINPID (code=exited, status=0/SUCCESS)
  Process: 3535 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir %n (code=exited, status=0/SUCCESS)
 Main PID: 3617 (mysqld_safe)
    Tasks: 20
   Memory: 102.1M
   CGroup: /system.slice/mariadb.service
           ├─3617 /bin/sh /usr/bin/mysqld_safe --basedir=/usr
           └─3780 /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/p...

Oct 01 15:22:38 centos mariadb-prepare-db-dir[3535]: MySQL manual for more instructions.
Oct 01 15:22:38 centos mariadb-prepare-db-dir[3535]: Please report any problems at http://mariadb.org/jira
Oct 01 15:22:38 centos mariadb-prepare-db-dir[3535]: The latest information about MariaDB is available at ...g/.
Oct 01 15:22:38 centos mariadb-prepare-db-dir[3535]: You can find additional information about the MySQL p...at:
Oct 01 15:22:38 centos mariadb-prepare-db-dir[3535]: http://dev.mysql.com
Oct 01 15:22:38 centos mariadb-prepare-db-dir[3535]: Consider joining MariaDB's strong and vibrant community:
Oct 01 15:22:38 centos mariadb-prepare-db-dir[3535]: https://mariadb.org/get-involved/
Oct 01 15:22:38 centos mysqld_safe[3617]: 201001 15:22:38 mysqld_safe Logging to '/var/log/mariadb/mariadb.log'.
Oct 01 15:22:38 centos mysqld_safe[3617]: 201001 15:22:38 mysqld_safe Starting mysqld daemon with databas...ysql
Oct 01 15:22:40 centos systemd[1]: Started MariaDB database server.
Hint: Some lines were ellipsized, use -l to show in full.
```

### Step 3 — mysql Installation

```
[root@centos ~]# mysql #using tab completion to find installation command
mysql                       mysqld_safe_helper          mysql_secure_installation
mysqlaccess                 mysqldump                   mysql_setpermission
mysqladmin                  mysqldumpslow               mysqlshow
mysqlbinlog                 mysql_find_rows             mysqlslap
mysqlbug                    mysql_fix_extensions        mysqltest
mysqlcheck                  mysqlhotcopy                mysql_tzinfo_to_sql
mysql_convert_table_format  mysqlimport                 mysql_upgrade
mysqld_multi                mysql_install_db            mysql_waitpid
mysqld_safe                 mysql_plugin                mysql_zap
[root@centos ~]# mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none): 
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] y
New password: 
Re-enter new password: 
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

### Step 4 — Create MySQL root password

```
[root@centos ~]# mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 10
Server version: 5.5.65-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
```

### Step 5 — Create database

```
MariaDB [people]> create database cities;
Query OK, 1 row affected (0.00 sec)

MariaDB [people]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| cities             |
| mysql              |
| people             |
| performance_schema |
+--------------------+
5 rows in set (0.00 sec)

MariaDB [people]> use cities;
Database changed
```

### Step 6 — Create table in database & insert values

```
MariaDB [cities]> create table city(city VARCHAR(20), country VARCHAR(20));
Query OK, 0 rows affected (0.01 sec)

MariaDB [cities]> select * from city;
Empty set (0.00 sec)

MariaDB [cities]> insert into city(city, country) values('Toronto', 'Canada');
```

### Step 7 — Verify data is now in table

```
MariaDB [cities]> select * from city;
+---------+---------+
| city    | country |
+---------+---------+
| Toronto | Canada  |
+---------+---------+
1 row in set (0.00 sec)

MariaDB [cities]> select * from city where country='Canada';
+---------+---------+
| city    | country |
+---------+---------+
| Toronto | Canada  |
+---------+---------+
1 row in set (0.00 sec)
```

## ☁️ Cloud Outcome

You know know all the MariaDB relating things that you need to know for the LFCS!

## Next Steps

Configuring Basic Email Handling labs and other material.

## Social Proof

[Tweet]()