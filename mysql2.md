mysql 
1 .检查服务
$ sudo service mysql start      

                      
 * Starting MySQL database server mysqld  
#mysql: unrecognized service  mysql 未安装

#安装 MySQL 服务端
sudo apt-get install mysql-server

#安装 MySQL 客户端
sudo apt-get install mysql-client          

#过程 输入YES ，设置root密码


#验证是否成功。
sudo netstat -tap | grep mysql   

$ sudo netstat -tap | grep mysql                        [13:20:11]
tcp        0      0 localhost:mysql         *:*                     LISTEN      -               

#根据需要修改配置文件（my.cnf)
sudo gedit /etc/mysql/my.cnf    


# 1.
$ sudo service mysql start                              [13:24:19]
 * Starting MySQL database server mysqld                                 [ OK ] 
$ mysql -u root                                         [13:24:33]
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.7.27-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 

2.查看数据库
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)


3.连接数据库
mysql> use information_schema
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> 

4.查看表
mysql> show tables;
+---------------------------------------+
| Tables_in_information_schema          |
+---------------------------------------+
| CHARACTER_SETS                        |
| COLLATIONS                            |
| COLLATION_CHARACTER_SET_APPLICABILITY |
| COLUMNS                               |
| COLUMN_PRIVILEGES                     |
| ENGINES                               |
| EVENTS                                |
| FILES                                 |
| GLOBAL_STATUS                         |
| GLOBAL_VARIABLES                      |
| KEY_COLUMN_USAGE                      |
| OPTIMIZER_TRACE                       |
| PARAMETERS                            |
| PARTITIONS         



5.退出 或 exit
mysql> quit
Bye



  

