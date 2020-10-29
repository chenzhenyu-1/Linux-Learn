



# 打开MySQL并登录

linux下：

下载完成后，输入命令开启 MySQL 服务并使用 root 用户登录：

```bash
#打开 MySQL 服务
sudo service mysql start

#使用 root 用户登录
mysql -u root
```

windows下：

在 Windows 系统下，打开命令窗口(cmd)，进入 MySQL 安装目录的 bin 目录。

启动：

```
cd c:/mysql/bin
mysqld --console
```

关闭：

```
cd c:/mysql/bin
mysqladmin -uroot shutdown
```

# 创建数据库并插入数据

## 新建数据库

首先，我们创建一个数据库，给它一个名字，比如 `mysql_shiyan`，以后的几次实验也是对 `mysql_shiyan` 这个数据库进行操作。 语句格式为 `CREATE DATABASE <数据库名字>;`，（注意不要漏掉分号 `;`），前面的 CREATE DATABASE 也可以使用小写，具体命令为：

```sql
CREATE DATABASE mysql_shiyan;
```

创建成功后输入命令 `show databases;` （注意不要漏掉`;`）检查一下：

![01](https://doc.shiyanlou.com/MySQL/sql-02-01.png)

在大多数系统中，SQL 语句都是不区分大小写的，因此以下语句都是合法的：

```sql
CREATE DATABASE name1;
create database name2;
CREATE database name3;
create DAtabaSE name4;
```

但是出于严谨，而且便于区分保留字（***保留字(reserved word)：指在高级语言中已经定义过的字，使用者不能再将这些字作为变量名或过程名使用。\***）和变量名，我们把保留字大写，把变量和数据小写。

## 连接数据库

接下来的操作，就在刚才创建的 `mysql_shiyan` 中进行，由于一个系统中可能会有多个数据库，要确定当前是对哪一个数据库操作，使用语句 `use `：

```sql
use mysql_shiyan;
```

如图显示，则连接成功：

![02](https://doc.shiyanlou.com/MySQL/sql-02-02.png)

输入命令 `show tables;` 可以查看当前数据库里有几张表，现在 `mysql_shiyan` 里还是空的：

![03](https://doc.shiyanlou.com/MySQL/sql-02-03.png)

## 数据表

数据表（`table`）简称表，它是数据库最重要的组成部分之一。数据库只是一个框架，表才是实质内容。

而一个数据库中一般会有多张表，这些各自独立的表通过建立关系被联接起来，才成为可以交叉查阅、一目了然的数据库。如下便是一张表：

| ID   | name | phone     |
| ---- | ---- | --------- |
| 01   | Tom  | 110110110 |
| 02   | Jack | 119119119 |
| 03   | Rose | 114114114 |

## 新建数据表

在数据库中新建一张表的语句格式为：

```sql
CREATE TABLE 表的名字
(
列名a 数据类型(数据长度),
列名b 数据类型(数据长度)，
列名c 数据类型(数据长度)
);
```

我们尝试在 `mysql_shiyan` 中新建一张表 `employee`，包含姓名，ID 和电话信息，所以语句为：

```sql
CREATE TABLE employee (id int(10),name char(20),phone int(12));
```

然后再创建一张表 `department`，包含名称和电话信息，想让命令看起来更整洁，你可以这样输入命令：

![04](https://doc.shiyanlou.com/MySQL/sql-02-04.png)

这时候再 `show tables;` 一下，可以看到刚才添加的两张表：

![05](https://doc.shiyanlou.com/MySQL/sql-02-05.png)

## 数据类型

在刚才新建表的过程中，我们提到了数据类型，MySQL 的数据类型和其他编程语言大同小异，下表是一些 MySQL 常用数据类型：

| 数据类型 | 大小(字节) | 用途             | 格式              |
| -------- | ---------- | ---------------- | ----------------- |
| INT      | 4          | 整数             |                   |
| FLOAT    | 4          | 单精度浮点数     |                   |
| DOUBLE   | 8          | 双精度浮点数     |                   |
| ENUM     | --         | 单选,比如性别    | ENUM('a','b','c') |
| SET      | --         | 多选             | SET('1','2','3')  |
| DATE     | 3          | 日期             | YYYY-MM-DD        |
| TIME     | 3          | 时间点或持续时间 | HH:MM:SS          |
| YEAR     | 1          | 年份值           | YYYY              |
| CHAR     | 0~255      | 定长字符串       |                   |
| VARCHAR  | 0~255      | 变长字符串       |                   |
| TEXT     | 0~65535    | 长文本数据       |                   |

整数除了 INT 外，还有 TINYINT、SMALLINT、MEDIUMINT、BIGINT。

**CHAR 和 VARCHAR 的区别:** CHAR 的长度是固定的，而 VARCHAR 的长度是可以变化的，比如，存储字符串 “abc"，对于 CHAR(10)，表示存储的字符将占 10 个字节(包括 7 个空字符)，而同样的 VARCHAR(12) 则只占用 4 个字节的长度，`增加一个额外字节来存储字符串本身的长度`，12 只是最大值，当你存储的字符小于 12 时，按实际长度存储。

**ENUM 和 SET 的区别:** ENUM 类型的数据的值，必须是定义时枚举的值的其中之一，即单选，而 SET 类型的值则可以多选。

想要了解更多关于 MySQL 数据类型的信息，可以参考下面两篇博客。

- [MySQL 中的数据类型介绍](http://blog.csdn.net/anxpp/article/details/51284106#comments)
- [MySQL 数据类型](http://www.cnblogs.com/bukudekong/archive/2011/06/27/2091590.html)

## 插入数据

刚才我们新建了两张表，使用语句 `SELECT * FROM employee;` 查看表中的内容，可以看到 employee 表中现在还是空的：

![06](https://doc.shiyanlou.com/MySQL/sql-02-06.png)

***刚才使用的 SELECT 语句将在下一节实验中详细介绍\***

我们通过 INSERT 语句向表中插入数据，语句格式为：

```sql
INSERT INTO 表的名字(列名a,列名b,列名c) VALUES(值1,值2,值3);
```

我们尝试向 employee 中加入 Tom、Jack 和 Rose：

```sql
INSERT INTO employee(id,name,phone) VALUES(01,'Tom',110110110);

INSERT INTO employee VALUES(02,'Jack',119119119);

INSERT INTO employee(id,name) VALUES(03,'Rose');
```

你已经注意到了，有的数据需要用单引号括起来，比如 Tom、Jack、Rose 的名字，这是由于它们的数据类型是 CHAR 型。此外 **VARCHAR,TEXT,DATE,TIME,ENUM** 等类型的数据也需要单引号修饰，而 **INT,FLOAT,DOUBLE** 等则不需要。

第一条语句比第二条语句多了一部分：`(id,name,phone)` 这个括号里列出的，是将要添加的数据 `(01,'Tom',110110110)` 其中每个值在表中对应的列。而第三条语句只添加了 `(id,name)` 两列的数据，**所以在表中 Rose 的 phone 为 NULL**。

现在我们再次使用语句 `SELECT * FROM employee;` 查看 employee 表，可见 Tom 和 Jack 的相关数据已经保存在其中了：

![07](https://doc.shiyanlou.com/MySQL/sql-02-07.png)

# SQL的约束

## 主键

在数据库中，如果有两行记录数据完全一样，那么如何来区分呢？ 答案是无法区分，如果有两行记录完全相同，那么对于 Mysql 就会认定它们是同一个实体，这于现实生活是存在差别的。

假如我们要存储一个学生的信息，信息包含姓名，身高，性别，年龄。

不幸的是有两个女孩都叫小梦，且她们的身高和年龄相同，数据库将无法区分这两个实体，这时就需要用到主键了。

主键（PRIMARY KEY）作为数据表中一行数据的唯一标识符，在一张表中通过主键就能准确定位到某一行数据，因此主键十分重要，它不能有重复记录且不能为空。

在 `MySQL-03-01.sql` 中，这里有主键：

![07](https://doc.shiyanlou.com/MySQL/sql-03-07.png)

也可以这样定义主键：

![08-](https://doc.shiyanlou.com/1sql-03-08-.png)

还有一种特殊的主键——复合主键。主键不仅可以是表中的一列，也可以由表中的两列或多列来共同标识，比如：

![09-](https://doc.shiyanlou.com/1sql-03-09-.png)

## 默认值约束

默认值约束 (DEFAULT) 规定，当有 DEFAULT 约束的列，插入数据为空时，将使用默认值。

默认值常用于一些可有可无的字段，比如用户的个性签名，如果用户没有设置，系统给他应该设定一个默认的文本，比如空文本或 ‘这个人太懒了，没有留下任何信息’

在 `MySQL-03-01.sql` 中，这段代码包含了 DEFAULT 约束：

```sql
people_num INT(10) DEFAULT 10,
```

DEFAULT 约束只会在使用 INSERT 语句（上一实验介绍过）时体现出来， INSERT 语句中，如果被 DEFAULT 约束的位置没有值，那么这个位置将会被 DEFAULT 的值填充，如语句：

```sql
# 正常插入数据
INSERT INTO department(dpt_name,people_num) VALUES('dpt1',11);

#插入新的数据，people_num 为空，使用默认值
INSERT INTO department(dpt_name) VALUES('dpt2');
```

输入命令 `SELECT * FROM department;`，可见表中第二行的 people_num 被 DEFAULT 的值 (10) 填充：

![01](https://doc.shiyanlou.com/MySQL/sql-03-01.png)

## 唯一约束

唯一约束 (UNIQUE) 比较简单，它规定一张表中指定的一列的值必须不能有重复值，即这一列每个值都是唯一的。

在 `MySQL-03-01.sql` 中，也有 UNIQUE 约束：

![11](https://doc.shiyanlou.com/MySQL/sql-03-11.png)

当 INSERT 语句新插入的数据和已有数据重复的时候，如果有 UNIQUE 约束，则 INSERT 失败，比如：

```sql
INSERT INTO employee VALUES(01,'Tom',25,3000,110110,'dpt1');
INSERT INTO employee VALUES(02,'Jack',30,3500,110110,'dpt2');
```

结果如图：

![02](https://doc.shiyanlou.com/MySQL/sql-03-02.png)

## 外键约束

外键 (FOREIGN KEY) 既能确保数据完整性，也能表现表之间的关系。

比如，现在有用户表和文章表，给文章表中添加一个指向用户 id 的外键，表示这篇文章所属的用户 id，外键将确保这个外键指向的记录是存在的，如果你尝试删除一个用户，而这个用户还有文章存在于数据库中，那么操作将无法完成并报错。因为你删除了该用户过后，他发布的文章都没有所属用户了，而这样的情况是不被允许的。同理，你在创建一篇文章的时候也不能为它指定一个不存在的用户 id。

一个表可以有多个外键，每个外键必须 REFERENCES (参考) 另一个表的主键，被外键约束的列，取值必须在它参考的列中有对应值。

![12-](https://doc.shiyanlou.com/1sql-03-12-.png)

在 INSERT 时，如果被外键约束的值没有在参考列中有对应，比如以下命令，参考列 (department 表的 dpt_name) 中没有 dpt3，则 INSERT 失败：

```sql
INSERT INTO employee VALUES(02,'Jack',30,3500,114114,'dpt3');
```

可见之后将 dpt3 改为 dpt2（department 表中有 dpt2），则插入成功：

![03](https://doc.shiyanlou.com/MySQL/sql-03-03.png)


## 非空约束

非空约束 (NOT NULL),听名字就能理解，被非空约束的列，在插入值时必须非空。

![13](https://doc.shiyanlou.com/MySQL/sql-03-13.png)

在 MySQL 中违反非空约束，会报错，比如以下语句：

```sql
#INSERT 成功 age 为空，因为没有非空约束，表中显示 NULL
INSERT INTO employee(id,name,salary,phone,in_dpt) VALUES(03,'Jim',3400,119119,'dpt2');

#报错 salary 被非空约束，插入数据失败
INSERT INTO employee(id,name,age,phone,in_dpt) VALUES(04,'Bob',23,123456,'dpt1');
```

结果如图，插入数据失败，实验楼的 MySQL 环境是 `5.7.22`，禁止插入不符合非空约束的数据：

![04](https://doc.shiyanlou.com/document-uid600404labid73timestamp1529106622613.png)

此时 employee 表的内容为：

![05](https://doc.shiyanlou.com/document-uid600404labid73timestamp1529106642913.png)

# 

# [mysql常用命令总结](https://www.cnblogs.com/janken/p/11516128.html)

连接：**mysql [-h127.0.0.1] [-P3306] -uroot -p**  (端口要用大写P，与密码p加以区分）

查看mysql的数据库列表：**show databases;**

使用某个库：**use [数据库名];**

查看表列表：**show tables;**

查看数据库的创建sql：**show create database [数据库名称];**

查看表的创建sql：**show create table [表名];**

查看数据的字符集相关信息: **show variables like '%char%';**

![img](https://img2018.cnblogs.com/blog/379702/201908/379702-20190822145334348-1263288214.png)

其中client、connection、results会根据不同连接设置不同的字符集，cmd下默认就是gbk；

与开发有关的是database与server，其中database必须为utf-8；server是用于设置默认的连接字符集，如果连接设置了字符集则使用连接的，如果未设置则使用server的字符集。

修改server字符集的方法

windows下是修改my.ini文件。

my.ini可以位于以下两个位置：

1、services.msc中配置的MYSQL服务中启动参数 --defaults-file指定的my.ini;

2、如果启动的服务未指定文件路径，则是mysql安装根目录下的my.ini

ubuntu下是修改my.cnf。

my.cnf所在的位置是：

/etc/mysql

修改方式：

```
`[mysqld]` `character-``set``-server=utf8`
```

以上修改完成后，需要重启MYSQL服务。

ubuntu的mysql重启命令：**sudo service mysql restart**

 

查看当前登录的用户：**select user(); 或 select current_user();**

查看数据库系统配置的用户列表：**SELECT \* FROM mysql.user;** （其中权限相关的信息也在这个表中，用户超期也在这个表中）

**创建用户编辑用户、创建数据库建议用MySqlWorkBench工具，强大可视，避免错误。**

创建用户：**CREATE USER 'test'@'localhost' IDENTIFIED BY '123456';**

root账户修改用户的密码的方式**：udpate mysql.user set authentication_string=password('[你的密码]') where user='[需要修改的用户名]'；**

有的老版本的mysql保存密码的字段为'password',修改密码是需要根据不同的字段名来调整sql是用authentication_string还是用password。

为用户授权：**GRANT ALL PRIVILEGES ON db.\* TO 'test'@'localhost';**

修改用户信息后刷新用户权限：**flush privileges;**

创建数据库： **create database [数据库名称] default character set utf8 collate utf8_general_ci;**

查看用户的授权语句：**show grants for [用户名];**

移除某个授权：**revoke [drop | 权限] on [数据库名称].\* from [用户名称];**

 删除某个数据库实例：**DROP DATABASE [数据库名称];**

查询一个用户有几个schemas（数据库实例）的访问权限：***\*show grants for [用户名]; (会将赋权给用户访问的数据列出来）\****

查看mysql的权限关键字列表：***\*show privilege;\****

查看某个schema（数据库实例）有哪些用户可以访问：***\*select host,db,user from mysql.db;\****