#mysql约束
#2.2建立含约束的表



#环境 MySQL语句
git clone https://github.com/shiyanlou/SQL3.git
1.
$ sudo service mysql start                        [15:19:02]
 * Starting MySQL database server mysqld                                 [ OK ] 
$ mysql  -u root  
2.实验用 现实中慎用！！！
#删除库
mysql> DROP DATABASE mysql_shiyan;
Query OK, 0 rows affected (0.01）


#根据自己环境导入文件 MySQL-03-01.sql
mysql> source /home/shiyanlou/Desktop/SQL3/MySQL-03-01.sql;
Query OK, 1 row affected (0.01 sec)

Database changed
Query OK, 0 rows affected (0.12 sec)

Query OK, 0 rows affected (0.10 sec)

Query OK, 0 rows affected (0.06 sec)

mysql> show tables;
+------------------------+
| Tables_in_mysql_shiyan |
+------------------------+
| department             |
| employee               |
| project                |
+------------------------+
3 rows in set (0.00 sec)
#插入测试数据
mysql> INSERT INTO department(dpt_name,people_num) VALUES('dpt1',11);
Query OK, 1 row affected (0.05 sec)

mysql> INSERT INTO department(dpt_name) VALUES('dpt2');
Query OK, 1 row affected (0.02 sec)

#查询表 people_num 被 Default 的值（10）填充
mysql> select * from department;
+----------+------------+
| dpt_name | people_num |
+----------+------------+
| dpt1     |         11 |
| dpt2     |         10 |
+----------+------------+
2 rows in set (0.00 sec)
#Unique 值不能重复

mysql> insert into employee values(01,'Tome',25,3000,110110,'dpt1');
Query OK, 1 row affected (0.02 sec)
#出现Error插入错误，插入失败  sql 语句中 箭头上下键勿碰 ！！！
mysql> insert into employee values(02,'Jack',30,3500,110110,'dpt2');
ERROR 1062 (23000): Duplicate entry '110110' for key 'phone'

#外健 Foreign key 确保数据完整 给文章添加用户id的外健 ，文章所属用户id ,外健将确保指向记录存在。

#插入失败
mysql> INSERT INTO employee VALUES(02,'Jack',30,3500,114114,'dpt3');
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`mysql_shiyan`.`employee`, CONSTRAINT `emp_fk` FOREIGN KEY (`in_dpt`) REFERENCES `department` (`dpt_name`))

#dpt3改dpt2 插入成功（department 表中有 dpt2)
mysql> INSERT INTO employee VALUES(02,'Jack',30,3500,114114,'dpt2');
Query OK, 1 row affected (0.04 sec)

#age int(10)  插入成功
mysql> insert into employee(id,name,salary,phone,in_dpt) value(03,'Jim',3400,119119,'dpt2');
Query OK, 1 row affected (0.01 sec)

#salary int(10) NOT NUll 有非空约束 插入失败
mysql> insert into employee(id,name,age,phone,in_dpt) value(04,'Bob',23,123456,'dpt1');
ERROR 1364 (HY000): Field 'salary' doesn't have a default value

#emplloyee 的内容
mysql> select * from employee;
+----+------+------+--------+--------+--------+
| id | name | age  | salary | phone  | in_dpt |
+----+------+------+--------+--------+--------+
|  1 | Tome |   25 |   3000 | 110110 | dpt1   |
|  2 | Jack |   30 |   3500 | 114114 | dpt2   |
|  3 | Jim  | NULL |   3400 | 119119 | dpt2   |
+----+------+------+--------+--------+--------+
3 rows in set (0.01 sec)








