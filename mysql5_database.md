database_table

#1.
$cd Desktop
$git clone https://github.com/shiyanlou/SQL5.git 
$sudo service mysql start                        [13:01:46]
 * Starting MySQL database server mysqld  
$mysql -u root
#mysql> drop database mysql_shiyan; 

mysql> source /home/shiyanlou/Desktop/SQL5/MySQL-05.sql  
Query OK, 1 row affected (0.01 sec)

Query OK, 1 row affected (0.00 sec)

Database changed
Query OK, 0 rows affected (0.09 sec)

Query OK, 0 rows affected (0.10 sec)

Query OK, 0 rows affected (0.08 sec)

Query OK, 0 rows affected (0.07 sec)

Query OK, 1 row affected (0.05 sec)

Query OK, 1 row affected (0.02 sec)
#1.查询
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| mysql              |
| mysql_shiyan       |
| performance_schema |
| sys                |
| test_01            |
+--------------------+
7 rows in set (0.01 sec)

#2.删库 test_01
mysql> drop database test_01;
Query OK, 0 rows affected (0.01 sec)
#3.查询
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| mysql              |
| mysql_shiyan       |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.00 sec)

#4\重命名表 
#4.1 rename table 原名 to 新名；
#4.2 alter table 原名 rename 新名
#4.3 alter table 原名 rename to 新名

mysql> use mysql_shiyan
Database changed
#查表
mysql> show tables;
+------------------------+
| Tables_in_mysql_shiyan |
+------------------------+
| department             |
| employee               |
| project                |
| table_1                |
+------------------------+
4 rows in set (0.00 sec)
#改表
mysql> rename table table_1 to table_2;
Query OK, 0 rows affected (0.09 sec)
#查结果
mysql> show tables;
+------------------------+
| Tables_in_mysql_shiyan |
+------------------------+
| department             |
| employee               |
| project                |
| table_2                |
+------------------------+
4 rows in set (0.01 sec)

#5删表 drop table 表名 
mysql> drop table table_2;
Query OK, 0 rows affected (0.09 sec)

mysql> show tables;
+------------------------+
| Tables_in_mysql_shiyan |
+------------------------+
| department             |
| employee               |
| project                |
+------------------------+
3 rows in set (0.01 sec)
#6修改表结构
#6.1加一列 
#6.1.1 alter table 表名 add column 列名 数据类型 约束；
#6.1.2 alter table 表名 add  列名 数据类型 约束；
#6 表employee 增加身高 height 制定 default 约束  int(4)是值显示宽度  加 lafter 列1  ：新列在列1后
mysql> alter table employee add height int(4) default 170;
Query OK, 0 rows affected (0.23 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from employee;
+----+------+------+--------+--------+--------+--------+
| id | name | age  | salary | phone  | in_dpt | height |
+----+------+------+--------+--------+--------+--------+
|  1 | Tom  |   26 |   2500 | 119119 | dpt4   |    170 |
|  2 | Jack |   24 |   2500 | 120120 | dpt2   |    170 |
|  3 | Rose |   22 |   2800 | 114114 | dpt3   |    170 |
|  4 | Jim  |   35 |   3000 | 100861 | dpt1   |    170 |
|  5 | Mary |   21 |   3000 | 100101 | dpt2   |    170 |
|  6 | Alex |   26 |   3000 | 123456 | dpt1   |    170 |
+----+------+------+--------+--------+--------+--------+
6 rows in set (0.00 sec)

#6.2 制定位置加列 age（年龄） 后 加入 weigh (体重）
mysql> alter table employee add wight int(4) default 120 after age;
Query OK, 0 rows affected (0.24 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from employee;
+----+------+------+-------+--------+--------+--------+--------+
| id | name | age  | wight | salary | phone  | in_dpt | height |
+----+------+------+-------+--------+--------+--------+--------+
|  1 | Tom  |   26 |   120 |   2500 | 119119 | dpt4   |    170 |
|  2 | Jack |   24 |   120 |   2500 | 120120 | dpt2   |    170 |
|  3 | Rose |   22 |   120 |   2800 | 114114 | dpt3   |    170 |
|  4 | Jim  |   35 |   120 |   3000 | 100861 | dpt1   |    170 |
|  5 | Mary |   21 |   120 |   3000 | 100101 | dpt2   |    170 |
|  6 | Alex |   26 |   120 |   3000 | 123456 | dpt1   |    170 |
+----+------+------+-------+--------+--------+--------+--------+
6 rows in set (0.01 sec)

#6.3 第一列插入
mysql> alter table employee add test int(10) default 11 first;
Query OK, 0 rows affected (0.25 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from employee;
+------+----+------+------+-------+--------+--------+--------+--------+
| test | id | name | age  | wight | salary | phone  | in_dpt | height |
+------+----+------+------+-------+--------+--------+--------+--------+
|   11 |  1 | Tom  |   26 |   120 |   2500 | 119119 | dpt4   |    170 |
|   11 |  2 | Jack |   24 |   120 |   2500 | 120120 | dpt2   |    170 |
|   11 |  3 | Rose |   22 |   120 |   2800 | 114114 | dpt3   |    170 |
|   11 |  4 | Jim  |   35 |   120 |   3000 | 100861 | dpt1   |    170 |
|   11 |  5 | Mary |   21 |   120 |   3000 | 100101 | dpt2   |    170 |
|   11 |  6 | Alex |   26 |   120 |   3000 | 123456 | dpt1   |    170 |
+------+----+------+------+-------+--------+--------+--------+--------+
6 rows in set (0.01 sec)



#7删除列
#7.1 alter table  表名 drop column 列名;
#7.2 alter table  表名 drop  列名;
#7 drop test
mysql> alter table employee drop test;
Query OK, 0 rows affected (0.18 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from employee;
+----+------+------+-------+--------+--------+--------+--------+
| id | name | age  | wight | salary | phone  | in_dpt | height |
+----+------+------+-------+--------+--------+--------+--------+
|  1 | Tom  |   26 |   120 |   2500 | 119119 | dpt4   |    170 |
|  2 | Jack |   24 |   120 |   2500 | 120120 | dpt2   |    170 |
|  3 | Rose |   22 |   120 |   2800 | 114114 | dpt3   |    170 |
|  4 | Jim  |   35 |   120 |   3000 | 100861 | dpt1   |    170 |
|  5 | Mary |   21 |   120 |   3000 | 100101 | dpt2   |    170 |
|  6 | Alex |   26 |   120 |   3000 | 123456 | dpt1   |    170 |
+----+------+------+-------+--------+--------+--------+--------+
6 rows in set (0.01 sec)

#8.重命名一列
#ALTER TABLE 表名 CHANGE 原列名 新列名 数据类型 约束；
mysql> alter table employee change height shengao int(4) default 170;
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0 

mysql> select * from employee;
+----+------+------+-------+--------+--------+--------+---------+
| id | name | age  | wight | salary | phone  | in_dpt | shengao |
+----+------+------+-------+--------+--------+--------+---------+
|  1 | Tom  |   26 |   120 |   2500 | 119119 | dpt4   |     170 |
|  2 | Jack |   24 |   120 |   2500 | 120120 | dpt2   |     170 |

#9.改变数据类型
#alter table 表名 modify 列名 新数据类型；！！！要慎用！！！

#10修改表中的值

#UPDATE 表名 SET 列1=值1,列2=值2 WHERE 条件;  一定要有where条件 
# tom 的 age改为21 ，salary 改为3000
mysql> update employee set age=21,salary=3000 where name='Tom';
Query OK, 1 row affected (0.03 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from employee where name='tom';
+----+------+------+--------+--------+--------+--------+---------+
| id | name | age  | weight | salary | phone  | in_dpt | shengao |
+----+------+------+--------+--------+--------+--------+---------+
|  1 | Tom  |   21 |    120 |   3000 | 119119 | dpt4   |     170 |
+----+------+------+--------+--------+--------+--------+---------+


#11删除一行数据
#DELETE FROM 表名 WHERE 条件;
mysql> delete from employee where name='Tom'
    -> ;
Query OK, 1 row affected (0.01 sec)
mysql> select * from employee;
+----+------+------+--------+--------+--------+--------+---------+
| id | name | age  | weight | salary | phone  | in_dpt | shengao |
+----+------+------+--------+--------+--------+--------+---------+
|  2 | Jack |   24 |    120 |   2500 | 120120 | dpt2   |     170 |
|  3 | Rose |   22 |    120 |   2800 | 114114 | dpt3   |     170 |
|  4 | Jim  |   35 |    120 |   3000 | 100861 | dpt1   |     170 |
|  5 | Mary |   21 |    120 |   3000 | 100101 | dpt2   |     170 |
|  6 | Alex |   26 |    120 |   3000 | 123456 | dpt1   |     170 |
+----+------+------+--------+--------+--------+--------+---------+
5 rows in set (0.00 sec)

mysql> select * from employee
    -> ;
+----+------+------+--------+--------+--------+--------+---------+
| id | name | age  | weight | salary | phone  | in_dpt | shengao |
+----+------+------+--------+--------+--------+--------+---------+
|  2 | Jack |   24 |    120 |   2500 | 120120 | dpt2   |     170 |
|  3 | Rose |   22 |    120 |   2800 | 114114 | dpt3   |     170 |
|  4 | Jim  |   35 |    120 |   3000 | 100861 | dpt1   |     170 |
|  5 | Mary |   21 |    120 |   3000 | 100101 | dpt2   |     170 |
|  6 | Alex |   26 |    120 |   3000 | 123456 | dpt1   |     170 |
+----+------+------+--------+--------+--------+--------+---------+
5 rows in set (0.01 sec)


#update 没有  where 条件  更新所有 数据
mysql> update employee set salary=2500;
Query OK, 4 rows affected (0.01 sec)
Rows matched: 5  Changed: 4  Warnings: 0

mysql> select * from employee;
+----+------+------+--------+--------+--------+--------+---------+
| id | name | age  | weight | salary | phone  | in_dpt | shengao |
+----+------+------+--------+--------+--------+--------+---------+
|  2 | Jack |   24 |    120 |   2500 | 120120 | dpt2   |     170 |
|  3 | Rose |   22 |    120 |   2500 | 114114 | dpt3   |     170 |
|  4 | Jim  |   35 |    120 |   2500 | 100861 | dpt1   |     170 |
|  5 | Mary |   21 |    120 |   2500 | 100101 | dpt2   |     170 |
|  6 | Alex |   26 |    120 |   2500 | 123456 | dpt1   |     170 |
+----+------+------+--------+--------+--------+--------+---------+
5 rows in set (0.01 sec)














