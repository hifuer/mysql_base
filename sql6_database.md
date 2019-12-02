mysql6 database 

#环境
#cd Desktop                                            [16:30:17]
$git clone https://github.com/shiyanlou/SQL6 

$ sudo service mysql start                        [16:30:58]
 * Starting MySQL database server mysqld                                 [ OK ] 
$ mysql -u root       

mysql> source /home/shiyanlou/Desktop/SQL6/MySQL-06.sql
Query OK, 1 row affected (0.01 sec)

Database changed
Query OK, 0 rows affected (0.10 sec)

Query OK, 0 rows affected (0.08 sec)

Query OK, 0 rows affected (0.05 sec)

#1.建索引 唯一型
#alter table 表名 add index 索引名 （列名）；
#create index 索引名 on 表名（列名）;
#1.1 表的 id列建 idx_id 索引
mysql> alter table employee add index idx_id (id);
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0
#1.2 表 name列 建 idx_name 的索引
mysql> create index idx_name on employee (name);
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0


mysql> show index from employee
    -> ;
+----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table    | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| employee |          0 | PRIMARY  |            1 | id          | A         |           5 |     NULL | NULL   |      | BTREE      |         |               |
| employee |          0 | phone    |            1 | phone       | A         |           5 |     NULL | NULL   |      | BTREE      |         |               |
| employee |          1 | emp_fk   |            1 | in_dpt      | A         |           3 |     NULL | NULL   |      | BTREE      |         |               |
| employee |          1 | idx_id   |            1 | id          | A         |           5 |     NULL | NULL   |      | BTREE      |         |               |
| employee |          1 | idx_name |            1 | name        | A         |           5 |     NULL | NULL   | YES  | BTREE      |         |               |
+----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
5 rows in set (0.00 sec)
#2视图 虚拟的表 使用视图时，把它当作一张表 创建

#CREATE VIEW 视图名(列a,列b,列c) AS SELECT 列1,列2,列3 FROM 表名;
mysql> create view v_emp(v_name,v_age,v_phone) as select name,age,phone from employee;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from v_emp;
+--------+-------+---------+
| v_name | v_age | v_phone |
+--------+-------+---------+
| Tom    |    26 |  119119 |
| Jack   |    24 |  120120 |
| Jobs   |  NULL |   19283 |
| Tony   |  NULL |  102938 |
| Rose   |    22 |  114114 |
+--------+-------+---------+
5 rows in set (0.01 sec)


#3导入 sql 语句  : source *.sql
#3.1数据文件导入  
#LOAD DATA INFILE '文件路径和文件名' INTO TABLE 表名;

#3.2查看路径变量：
mysql> show variables like '%secure%';
+--------------------------+-----------------------+
| Variable_name            | Value                 |
+--------------------------+-----------------------+
| require_secure_transport | OFF                   |
| secure_auth              | ON                    |
| secure_file_priv         | /var/lib/mysql-files/ |
+--------------------------+-----------------------+
3 rows in set (0.01 sec)
# secure_file_priv 变量指定安全路径 为 /var/lib/mysql-files/ ，导入数据要移动到安全路径下。
#另开终端
$ sudo cp -a /home/shiyanlou/Desktop/SQL6/ /var/lib/mysql-files   
$ sudo vim /var/lib/mysql-files/SQL6/in.txt 

mysql> select *from employee
    -> ;
+----+------+------+--------+--------+--------+
| id | name | age  | salary | phone  | in_dpt |
+----+------+------+--------+--------+--------+
|  1 | Tom  |   26 |   2500 | 119119 | dpt4   |
|  2 | Jack |   24 |   2500 | 120120 | dpt2   |
|  3 | Jobs | NULL |   3600 |  19283 | dpt2   |
|  4 | Tony | NULL |   3400 | 102938 | dpt3   |
|  5 | Rose |   22 |   2800 | 114114 | dpt3   |
+----+------+------+--------+--------+--------+
5 rows in set (0.01 sec)
#导入数据 
mysql> load data infile '/var/lib/mysql-files/SQL6/in.txt' into table employee;
Query OK, 7 rows affected (0.03 sec)
Records: 7  Deleted: 0  Skipped: 0  Warnings: 0


mysql> select * from employee;
+----+------+------+--------+--------+--------+
| id | name | age  | salary | phone  | in_dpt |
+----+------+------+--------+--------+--------+
|  1 | Tom  |   26 |   2500 | 119119 | dpt4   |
|  2 | Jack |   24 |   2500 | 120120 | dpt2   |
|  3 | Jobs | NULL |   3600 |  19283 | dpt2   |
|  4 | Tony | NULL |   3400 | 102938 | dpt3   |
|  5 | Rose |   22 |   2800 | 114114 | dpt3   |
|  6 | Alex |   26 |   3000 | 123456 | dpt1   |
|  7 | Ken  |   27 |   3500 | 654321 | dpt1   |
|  8 | Rick |   24 |   3500 | 987654 | dpt3   |
|  9 | Joe  |   31 |   3600 | 100129 | dpt2   |
| 10 | Mike |   23 |   3400 | 110110 | dpt1   |
| 11 | Jim  |   35 |   3000 | 100861 | dpt4   |
| 12 | Mary |   21 |   3000 | 100101 | dpt2   |
+----+------+------+--------+--------+--------+
12 rows in set (0.00 sec)

#4.导出 out.txt
#SELECT 列1，列2 INTO OUTFILE '文件路径和文件名' FROM 表名;
#注意 文件路径下不能有同名文件 
mysql> select * into outfile '/var/lib/mysql-files/out.txt' from employee;
Query OK, 12 rows affected (0.00 sec)

#另开终端 查看数据
$ sudo cat /var/lib/mysql-files/out.txt                 [17:38:35]
1	Tom	26	2500	119119	dpt4
2	Jack	24	2500	120120	dpt2
3	Jobs	\N	3600	19283	dpt2
4	Tony	\N	3400	102938	dpt3
5	Rose	22	2800	114114	dpt3
6	Alex	26	3000	123456	dpt1
7	Ken	27	3500	654321	dpt1
8	Rick	24	3500	987654	dpt3
9	Joe	31	3600	100129	dpt2
10	Mike	23	3400	110110	dpt1
11	Jim	35	3000	100861	dpt4
12	Mary	21	3000	100101	dpt2

#5备份 mysqldump  是备份工具 在终端执行，不是mysql交互环境下
mysqldump -u root 数据库名>备份文件名;   #备份整库

mysqldump -u root 数据库名 表名>备份文件名;   #备份整表

mysql> quit
Bye
$ cd ~
$ mysqldump -u root mysql_shiyan >bak.sql;              [17:44:59]
$ ls                                                    [17:46:18]
bak.sql  Desktop  lib           package.json  webpack.config.js
Code     golang   node_modules  src-gen       yarn.lock

#6恢复
source /tmp/SQL6/MySQL-06.sql 

#终端
mysql -u root

create database test; #建新库

退出MySQL

mysql -u root test <bak.sql

$ mysql -u root test < bak.sql                          [17:56:45]
$ mysql -u root   


建立员工名字 employee.name 和对应部门人数 department.people_num 的视图并展示。
mysql> CREATE VIEW name_people_num (name, people_num)
    -> AS SELECT name, people_num FROM employee, department
    -> WHERE in_dpt = dpt_name;
Query OK, 0 rows affected (0.01 sec)

mysql> SELECT * FROM name_people_num;
+------+------------+
| name | people_num |
+------+------------+
| Alex |         11 |
| Ken  |         11 |
| Mike |         11 |
| Jack |         12 |
| Jobs |         12 |
| Joe  |         12 |
| Mary |         12 |
| Tony |         10 |
| Rose |         10 |
| Rick |         10 |
| Tom  |         15 |
| Jim  |         15 |
+------+------------+
12 rows in set (0.00 sec)
 












