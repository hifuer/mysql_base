select 


#1.进入桌面
$cd /home/shiyanlou/Desktop

#2.git数据 sql (MYSQL-04-01.sql 创建数据库，MYSQL-04-02.sql 插入数据)
$git clone https://github.com/shiyanlou/SQL4.git

#3.启动数据库
$ sudo service mysql start
$mysql -u root

#4.删除上个实验的数据库 mysql_shiyan
>DROP DATABASE mysql_shiyan;

#5.建立数据库  注意文件名大小写 
#mysql> source /home/shiyanlou/Desktop/SQL4/MYSQL-04-01.sql
#ERROR: 
#Failed to open file '/home/shiyanlou/Desktop/SQL4/MYSQL-04-01.sql', error: 2

mysql> source /home/shiyanlou/Desktop/SQL4/MySQL-04-01.sql
Query OK, 1 row affected (0.01 sec)

Database changed
Query OK, 0 rows affected (0.09 sec)

Query OK, 0 rows affected (0.09 sec)

Query OK, 0 rows affected (0.05 sec)
#6.插入数据
mysql> source /home/shiyanlou/Desktop/SQL4/MySQL-04-02.sql
Query OK, 1 row affected (0.02 sec)

Query OK, 1 row affected (0.03 sec)

Query OK, 1 row affected (0.03 sec)

Query OK, 1 row affected (0.03 sec)

Query OK, 1 row affected (0.02 sec)

Query OK, 1 row affected (0.03 sec)

Query OK, 1 row affected (0.02 sec)

Query OK, 1 row affected (0.02 sec)

Query OK, 1 row affected (0.04 sec)

Query OK, 1 row affected (0.03 sec)

Query OK, 1 row affected (0.01 sec)

Query OK, 1 row affected (0.01 sec)

Query OK, 1 row affected (0.01 sec)

Query OK, 1 row affected (0.02 sec)

Query OK, 1 row affected (0.00 sec)

Query OK, 1 row affected (0.00 sec)

Query OK, 1 row affected (0.01 sec)

Query OK, 1 row affected (0.05 sec)

Query OK, 1 row affected (0.04 sec)

Query OK, 1 row affected (0.01 sec)

Query OK, 1 row affected (0.02 sec)

Query OK, 1 row affected (0.03 sec)
#7查询 看employee表的name,age
mysql> select name,age from employee;
+------+------+
| name | age  |
+------+------+
| Tom  |   26 |
| Jack |   24 |
| Rose |   22 |
| Jim  |   35 |
| Mary |   21 |
| Alex |   26 |
| Ken  |   27 |
| Rick |   24 |
| Joe  |   31 |
| Mike |   23 |
| Jobs | NULL |
| Tony | NULL |
+------+------+
12 rows in set (0.00 sec)
#8 筛选age > 25 对比上图
mysql> select name,age from employee where age>25;
+------+------+
| name | age  |
+------+------+
| Tom  |   26 |
| Jim  |   35 |
| Alex |   26 |
| Ken  |   27 |
| Joe  |   31 |
+------+------+
5 rows in set (0.01 sec)
#9查询名字 Mary员工的name,age ,phone 上下箭头 可切上一语句 ；号不要忘
mysql> select name,age,phone from employee where name='Mary'
    -> ; 
+------+------+--------+
| name | age  | phone  |
+------+------+--------+
| Mary |   21 | 100101 |
+------+------+--------+
1 row in set (0.01 sec)
#10 or    筛选age<25 或age>30  下实例用了 or
mysql> select name,age from employee where age<25 or age>30;
+------+------+
| name | age  |
+------+------+
| Jack |   24 |
| Rose |   22 |
| Jim  |   35 |
| Mary |   21 |
| Rick |   24 |
| Joe  |   31 |
| Mike |   23 |
+------+------+
7 rows in set (0.01 sec)

#10.1 and   筛选age>25 ,切age<30  下实例用了 and
mysql> select name,age from employee where age>25 and age<30;
+------+------+
| name | age  |
+------+------+
| Tom  |   26 |
| Alex |   26 |
| Ken  |   27 |
+------+------+
3 rows in set (0.01 sec)
#11 in ,  not in  筛选 在或不在 查询在 dpt3 或 dpt4的人
mysql> select name,age phone,in_dpt from employee where in_dpt in ('dpt3','dpt4');
+------+-------+--------+
| name | phone | in_dpt |
+------+-------+--------+
| Tom  |    26 | dpt4   |
| Rose |    22 | dpt3   |
| Rick |    24 | dpt3   |
| Mike |    23 | dpt4   |
| Tony |  NULL | dpt3   |
+------+-------+--------+
5 rows in set (0.00 sec)
#11.1 not in  查询不在 dpt1 也不在dpt3的人：
mysql> select name,age phone,in_dpt from employee where in_dpt not in ('dpt1','dpt3');
+------+-------+--------+
| name | phone | in_dpt |
+------+-------+--------+
| Tom  |    26 | dpt4   |
| Jack |    24 | dpt2   |
| Mary |    21 | dpt2   |
| Joe  |    31 | dpt2   |
| Mike |    23 | dpt4   |
| Jobs |  NULL | dpt2   |
+------+-------+--------+
6 rows in set (0.01 sec)

#12 LIKE ： 模糊查询    通配符 下划线  _ 代表一个未指定字符  % 代表 不定个 未指定字符
#只记住电话前4位 1101  忘记电话后两位 用两个下划线—— 通配符代替 
mysql> select name,age,phone from employee where phone like '1101__'
    -> ;
+------+------+--------+
| name | age  | phone  |
+------+------+--------+
| Joe  |   31 | 110129 |
| Mike |   23 | 110110 |
+------+------+--------+
2 rows in set (0.01 sec)

#12.1查询首字母为J的人
mysql> select name,age,phone from employee where name like 'J%';
+------+------+--------+
| name | age  | phone  |
+------+------+--------+
| Jack |   24 | 120120 |
| Jim  |   35 | 100861 |
| Joe  |   31 | 110129 |
+------+------+--------+
4 rows in set (0.01 sec)
#13 对结果排序 order by 结果是升序  关键字  asc 升  desc 降  不加关键字 博客按时间先后排序显示博文
mysql> select name,age,salary,phone from employee order by salary desc;
+------+------+--------+--------+
| name | age  | salary | phone  |
+------+------+--------+--------+
| Joe  |   31 |   3600 | 110129 |
| Jobs | NULL |   3600 |  19283 |
| Ken  |   27 |   3500 | 654321 |
| Rick |   24 |   3500 | 987654 |
| Mike |   23 |   3400 | 110110 |
| Tony | NULL |   3400 | 102938 |
| Jim  |   35 |   3000 | 100861 |
| Mary |   21 |   3000 | 100101 |
| Alex |   26 |   3000 | 123456 |
| Rose |   22 |   2800 | 114114 |
| Tom  |   26 |   2500 | 119119 |
| Jack |   24 |   2500 | 120120 |
+------+------+--------+--------+
12 rows in set (0.00 sec)
#14sql函数 count:计数 sum：求和 avg：平均值 max：最大值 min：最小值 
#求salary 的最大值，最小值
mysql> select max(salary) as max_salary, min(salary) from employee;
+------------+-------------+
| max_salary | min(salary) |
+------------+-------------+
|       3600 |        2500 |
+------------+-------------+

#15子查询 多表查询 查询‘Tom’员工所在部门做了几个工程  。员工信息在employee 表中，工程信息在project表中
mysql> select of_dpt,count(proj_name) as count_project from project group by of_dpt having of_dpt in (select in_dpt from employee where name='Tom');
+--------+---------------+
| of_dpt | count_project |
+--------+---------------+
| dpt4   |             2 |
+--------+---------------+
1 row in set (0.01 sec)
#上有2个 select ,第2个select 返回一个集合的数据形式，然后被第一个select语句用 in 进行判断
#having 关键字可以的作用和where是一样的，都是说明接下来要进行筛选操作 
#区别在与 having 用于对分组后的数据进行筛选  
#子查询可扩展3.4或更多层

#16连接查询 join  思路把两个表或多个表当一个新表来操作
mysql> select id ,name,people_num 
    -> from employee,department
    -> where employee.in_dpt=department.dpt_name
    -> order by id;
+----+------+------------+
| id | name | people_num |
+----+------+------------+
|  1 | Tom  |         15 |
|  2 | Jack |         12 |
|  3 | Rose |         10 |
|  4 | Jim  |         11 |
|  5 | Mary |         12 |
|  6 | Alex |         11 |
|  7 | Ken  |         11 |
|  8 | Rick |         10 |
|  9 | Joe  |         12 |
| 10 | Mike |         15 |
| 11 | Jobs |         12 |
| 12 | Tony |         10 |
+----+------+------------+
12 rows in set (1.40 sec)

#mysql> select id ,name,people_num                 #id ,name来自 employee，people_num来自department
#    -> from employee,department		   #查询2个表
#    -> where employee.in_dpt=department.dpt_name  #关联内容
#    -> order by id;


#16.1 join on 结果同上
mysql> select id ,name,people_num  from employee join department on employee.in_dpt=department.dpt_name order by id;
+----+------+------------+
| id | name | people_num |
+----+------+------------+
|  1 | Tom  |         15 |
|  2 | Jack |         12 |
|  3 | Rose |         10 |
|  4 | Jim  |         11 |
|  5 | Mary |         12 |
|  6 | Alex |         11 |
|  7 | Ken  |         11 |
|  8 | Rick |         10 |
|  9 | Joe  |         12 |
| 10 | Mike |         15 |
| 11 | Jobs |         12 |
| 12 | Tony |         10 |
+----+------+------------+
12 rows in set (0.00 sec)

















