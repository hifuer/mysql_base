#1检查服务 进入mysql

$sudo service mysql start  
$mysql -u root  

#2 创建数据库
mysql> CREATE DATABASE mysql_shiyan;
Query OK, 1 row affected (0.01 sec)


mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| mysql              |
| mysql_shiyan       |


#3 连接数据库
mysql> use mysql_shiyan;
Database changed

#4查看表
mysql> show tables;
Empty set (0.00 sec)


#4table
#ID	name	phone
#01	Tom	110110110
#02	Jack	119119119
#03	Rose	114114114

#4.1 table创建表1
mysql> CREATE TABLE employee(id int(10),name char(20),phone int(12));
Query OK, 0 rows affected (0.09 sec)

#4.2 TABLE创建表2
mysql> CREATE TABLE department
    -> (
    -> dpt_name CHAR(20),
    -> dpt_phone INT(12)
    -> );
Query OK, 0 rows affected (0.07 sec)

#-> 换行自动产生的符号

#4.3 show tables;
mysql> show tables;
+------------------------+
| Tables_in_mysql_shiyan |
+------------------------+
| department             |
| employee               |
+------------------------+
2 rows in set (0.00 sec)

#5 查看表内容
mysql> SELECT * FROM employee;
Empty set (0.03 sec)

#6 插入数据 [Ctrl+p] 上条语句
#6.1
mysql> INSERT INTO employee(id,name,phone) VALUES(01,'Tom',110110110);
Query OK, 1 row affected (0.01 sec)

#6.2
mysql> INSERT INTO employee(id,name,phone) VALUES(01,'Tom',110110110);
Query OK, 1 row affected (0.01 sec)

#6.3
mysql> INSERT INTO employee(id,name) VALUES(03,'Rose');
Query OK, 1 row affected (0.01 sec)

#6.4
mysql> SELECT * FROM employee;
+------+------+-----------+
| id   | name | phone     |
+------+------+-----------+
|    1 | Tom  | 110110110 |
|    2 | Jack | 119119119 |
|    3 | Rose |      NULL |
+------+------+-----------+
3 rows in set (0.00 sec)



mysql> CREATE DATABASE name1;
Query OK, 1 row affected (0.01 sec)

mysql> CREATE DATABASE name2;
Query OK, 1 row affected (0.01 sec)

mysql> CREATE database name3;
Query OK, 1 row affected (0.01 sec)

mysql> create DAtabaSE name4;
Query OK, 1 row affected (0.01 sec)

#sql 不区分大小写

#练习 创建库library ,包含 book，reader表
