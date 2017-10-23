---
title: MySQL
date: 2015-10-19 10:26:19
tags: MySQL
categories: SQL
---

## 1.Windows下MySQL的配置

以 MySQL 5.1 免安装版为例, 下载 mysql-noinstall-5.1.69-win32.zip ( 官方下载页:http://dev.mysql.com/downloads/mysql/5.1.html#downloads )

配置步骤:

1. 将下载的 mysql-noinstall-5.1.69-win32.zip 解压至需要安装的位置, 如: C:\Program Files;

2. 在安装文件夹下找到 my-small.ini 配置文件, 将其重命名为 my.ini , 打开进行编辑, 在 [client] 与 [mysqld] 下均添加一行: default-character-set = gbk

3. 打开 Windows 环境变量设置, 新建变量名 MYSQL_HOME , 变量值为 MySQL 安装目录路径, 这里为 C:\Program Files\mysql-5.1.69-win32

4. 在 环境变量 的 Path 变量中添加 ;%MYSQL_HOME%\bin;

5. 安装 MySQL 服务, 打开Windows命令提示符, 执行命令: mysqld --install MySQL --defaults-file="my.ini" 提示"Service successfully installed."表示成功;

 

MySQL服务的启动、停止与卸载

在 Windows 命令提示符下运行:

启动: net start MySQL

停止: net stop MySQL

卸载: sc delete MySQL

## 2.SQL语句

### 1.登陆：  mysql -h 主机名 -u 用户名 -p 密码; 

### 2.创建数据库： create database 数据库名 [其他选项];  
```
例：create database db_test character set gbk;
```
### 3.查看数据库：show databases;

### 4.使用数据库： use 数据库名;   
```
例：use db_test;
```
### 5.创建数据库表：create table 表名称(列声明);  
```
create table students
	（
		id int unsigned not null auto_increment primary key,
		name char(8) not null,
		sex char(4) not null,
		age tinyint unsigned not null,
		tel char(13) null default "-"
	);
```

### 6.查看数据库有哪些表：show tables;

### 7.插入一条数据：insert into 表名 [(列名1, 列名2, 列名3, ...)] values (值1, 值2, 值3, ...); 
```
例： insert into students values(NULL, "王刚", "男", 20, "13811371377");
     insert into students (name, sex, age) values("孙丽华", "女", 21);
```
### 8.查询数据：select 列名称 from 表名称 [查询条件];  
```
例：select name, age from students;  
    select * from students where sex="女";
```

### 9.修改数据：update 表名称 set 列名称=新值 where 更新条件; 
```
将id为5的手机号改为默认的"-": update students set tel=default where id=5;

将所有人的年龄增加1: update students set age=age+1;

将手机号为 13288097888 的姓名改为 "张伟鹏", 年龄改为 19: update students set name="张伟鹏", age=19 where tel="13288097888";
```

### 10.删除数据：delete from 表名称 where 删除条件;
```
例:

删除id为2的行: delete from students where id=2;

删除所有年龄小于21岁的数据: delete from students where age<20;

删除表中的所有数据: delete from students;
```

### 11.修改表
```
添加列
  
基本形式: alter table 表名 add 列名 列数据类型 [after 插入位置];
  
示例:
  
在表的最后追加列 address: alter table students add address char(60);
  
在名为 age 的列后插入列 birthday: alter table students add birthday date after age;
  
修改列
  
基本形式: alter table 表名 change 列名称 列新名称 新数据类型;
  
示例:
  
将表 tel 列改名为 telphone: alter table students change tel telphone char(13) default "-";
  
将 name 列的数据类型改为 char(16): alter table students change name name char(16) not null;
  
删除列
  
基本形式: alter table 表名 drop 列名称;
  
示例:
  
删除 birthday 列: alter table students drop birthday;
  
重命名表
  
基本形式: alter table 表名 rename 新表名;
  
示例:
  
重命名 students 表为 workmates: alter table students rename workmates;
  
删除整张表
  
基本形式: drop table 表名;
  
示例: 删除 workmates 表: drop table workmates;
  
删除整个数据库
  
基本形式: drop database 数据库名;
  
示例: 删除 samp_db 数据库: drop database samp_db;
```


