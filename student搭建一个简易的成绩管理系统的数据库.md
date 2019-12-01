#简单的成绩管理系统数据库

#student 学生表:学生id,学生姓名，性别

student
    sid	(主键）   sname  gender
      1    	tom 	  male
      2	   	Jack	  male	
      3   	 Rose	  female 

#课程表 

course 
课程id（主键）  课程名
cid		cname
1		math
2		physic
3		chemistry

#成绩表

mark
成绩id		学生id	课程id	分数
mid（主键）	sid	cid	score
1		1	1	80
2		2	1	85
3		3	1	90
4		1	2	60
5		2	2	90
6		3	2	75
7		1	3	95
8		2	3	75
9			3	85


目标：
1检查MYSQL服务处于运行状态
2新建数据库 gradesystem
3.gradesystem包含：student ,course,mark;


#1
$ sudo service mysql start                              [16:30:59]
 * Starting MySQL database server mysqld  

#2
$ mysql -u root                                         [16:33:43]
#Welcome to the MySQL monitor.  Commands end with ; or \g.
#Your MySQL connection id is 5
#Server version: 5.7.27-0ubuntu0.16.04.1 (Ubuntu)

#3
mysql> create database gradesystem;
#Query OK, 1 row affected (0.01 sec)

mysql> use gradesystem;
Database changed

#3.1
mysql> show tables;
#Empty set (0.01 sec)

mysql> create table student(
    -> sid int NOT NULL AUTO_INCREMENT,
    -> sname varchar(20) NOT NULL,
    -> gender varchar(10) NOT NULL,
    -> PRIMARY KEY(sid)
    -> );
#Query OK, 0 rows affected (0.05 sec)

mysql> create table course(
    -> cid int NOT NULL AUTO_INCREMENT,
    -> cname varchar(20) NOT NULL,
    -> PRIMARY KEY(cid)
    -> );
#Query OK, 0 rows affected (0.05 sec)

mysql> create table mark(
    -> mid int NOT NULL AUTO_INCREMENT,
    -> sid int NOT NULL,
    -> cid int NOT NULL,
    -> score int NOT NULL,
    -> PRIMARY KEY(mid),
    -> FOREIGN KEY(sid) REFERENCES student(sid),
    -> FOREIGN KEY(cid) REFERENCES course(cid)
    -> );
#Query OK, 0 rows affected (0.11 sec)

mysql> insert into student values(1,'Tom','male'),(2,'Jack','male'),(3,'Rose','female');
#Query OK, 3 rows affected (0.04 sec)
#Records: 3  Duplicates: 0  Warnings: 0


mysql> insert into course values(1,'math'),(2,'physics'),(3,'chemistry');
#Query OK, 3 rows affected (0.02 sec)
#Records: 3  Duplicates: 0  Warnings: 0

mysql> insert into mark values(1,1,1,80),(2,2,1,85),(3,3,1,90),(4,1,2,60),(5,2,2,90),(6,3,2,75),(7,1,3,95),(8,2,3,75)
    -> ;
#Query OK, 8 rows affected (0.01 sec)
#Records: 8  Duplicates: 0  Warnings: 0









