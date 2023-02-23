# SQL通用语法

- ​	在学习具体的SQL语句之前，先来了解一下SQL语言的同于语法
  - SQL语句可以单行或多行书写，以分号结尾
  - SQL语句可以使用空格/缩进来增强语句的可读性
  - MySQL数据库的SQL语句不区分大小写，关键字建议使用大写
  - 注释:
    - 多行注释：/* 注释内容 */
    - 单行注释：-- 注释内容 或 # 注释内容

## SQL分类

- ​	SQL语句，根据其功能，主要分为四类：DDL、DML、DQL、DCL

  - ​	![](E:\图片\笔记\SQL分类.png)


## DDL

- ​	Data Definition Language，数据定义语言，用来定义数据库对象(数据库，表，字段) 。 


### 数据库操作

- ​	查询所有数据库

  - `show databases ; `
  - ![](E:\图片\笔记\24.png)\

- ​    查询当前数据库

  - `select database() ; `

- 创建数据库

  - ```sql
    create database [ if not exists ] 数据库名 [ default charset 字符集 ] [ collate 排序 规则 ] ;
    ```

- 案例:

  - 创建一个itcast数据库, 使用数据库默认的字符集
    - `create database itcast; `
    - ![](E:\图片\笔记\25.png)\
  - 在同一个数据库服务器中，不能创建两个名称相同的数据库，否则将会报错
    - ![](E:\图片\笔记\26.png)\
  - 可以通过if not exists 参数来解决这个问题，数据库不存在, 则创建该数据库，如果存在，则不创建
    - `create database if not extists itcast; `
    - ![](E:\图片\笔记\28.png)\
  - 创建一个itheima数据库，并且指定字符集
    - `create database itheima default charset utf8mb4; `
    - ![](E:\图片\笔记\27.png)\

- 删除数据库

  - `drop database [ if exists ] 数据库名 ; `
  - 如果删除一个不存在的数据库，将会报错。此时，可以加上参数 if exists ，如果数据库存在，再执行删除，否则不执行删除
  - ![](E:\图片\笔记\29.png)\

- 切换数据库

  - `use 数据库名 ; `
  - 我们要操作某一个数据库下的表时，就需要通过该指令，切换到对应的数据库下，否则是不能操作的。比如，切换到itcast数据，执行如下SQL
  - `use itcast;`

### 表操作

​	查询当前数据库所有表

- `show tables;`
- 比如,我们可以切换到sys这个系统数据库,并查看系统数据库中的所有表结构
- `use sys; `
- `show tables`
- ![](E:\图片\笔记\31.png)\

​    查看指定表结构

- `desc 表名 ; `
- ![](E:\图片\笔记\32.png)\

查询指定表的建表语句

`show create table 表名 ;`

通过这条指令，主要是用来查看建表语句的，而有部分参数我们在创建表的时候，并未指定也会查询到，因为这部分是数据库的默认值，如：存储引擎、字符集等。

<img src="E:\图片\笔记\33.png" style="zoom:200%;" />

创建表结构

- ```sql
  CREATE TABLE 表名( 
      字段1 字段1类型 [ COMMENT 字段1注释 ], 
      字段2 字段2类型 [COMMENT 字段2注释 ], 
      字段3 字段3类型 [COMMENT 字段3注释 ], 
      ...... 
      字段n 字段n类型 [COMMENT 字段n注释 ] 
  ) [ COMMENT 表注释 ] ; 
  注意: [...] 内为可选参数，最后一个字段后面没有逗号
  ```

- 比如，我们创建一张表 tb_user ，对应的结构如下，那么建表语句为：

- ![](E:\图片\笔记\30.png)\

- ```sql
  create table tb_user( 
      id int comment '编号', 
      name varchar(50) comment '姓名',
      age int comment '年龄', 
      gender varchar(1) comment '性别' 
  ) comment '用户表';
  ```

数据类型



MySQL中的数据类型有很多，主要分为三类：数值类型、字符串类型、日期时间类型

#### 数值类型

​	![](E:\图片\笔记\mysql数值型.png)

```sql
如: 
1. 年龄字段 -- 不会出现负数, 而且人的年龄不会太大 age tinyint unsigned 2). 
分数 -- 总分100分, 最多出现一位小数 score double(4,1) 
```

#### 字符串类型

​	![](E:\图片\笔记\mysql字符串.png)

char 与 varchar 都可以描述字符串，char是定长字符串，指定长度多长，就占用多少个字符，和字段值的长度无关 。而varchar是变长字符串，指定的长度为最大占用长度 。相对来说，char的性能会更高些。

```sql
如： 
1. 用户名 username ------> 长度不定, 最长不会超过50 username varchar(50) 
2. 性别 gender ---------> 存储值, 不是男,就是女 gender char(1) 
3. 手机号 phone --------> 固定长度为11 phone char(11) 
```

#### 日期时间类型

​	![](E:\图片\笔记\mysql日期时间类型.png)

```sql
如: 
1. 生日字段 birthday birthday date 
2. 创建时间 createtime createtime datetime
```

#### 案例

```sql
设计一张员工信息表，要求如下：
	编号（纯数字）
	员工工号 (字符串类型，长度不超过10位)
	员工姓名（字符串类型，长度不超过10位）
	性别（男/女，存储一个汉字）
	年龄（正常人年龄，不可能存储负数）
	身份证号（二代身份证号均为18位，身份证中有X这样的字符）
	入职时间（取值年月日即可）
对应的建表语句如下:
	create table emp( 
        id int comment '编号', 
        workno varchar(10) comment '工号', 
        name varchar(10) comment '姓名', 
        gender char(1) comment '性别', 
        age tinyint unsigned comment '年龄', 
        idcard char(18) comment '身份证号', 
        entrydate date comment '入职时间' 
    ) comment '员工表';
```

SQL语句编写完毕之后，就可以在MySQL的命令行中执行SQL，然后也可以通过 desc 指令查询表结构信息：

![](E:\图片\笔记\1.png)

表结构创建好了，里面的name字段是varchar类型，最大长度为10，也就意味着如果超过10将会报错，如果我们想修改这个字段的类型 或 修改字段的长度该如何操作呢？接下来再来讲解DDL语句中，如何操作表字段。

#### 修改表

​	**添加字段**

​	`ALTER TABLE 表名 ADD 字段名 类型 (长度) [ COMMENT 注释 ] [ 约束 ]; `

​	**案例:** 

​	为emp表增加一个新的字段”昵称”为nickname，类型为varchar(20)

​	`ALTER TABLE emp ADD nickname varchar(20) COMMENT '昵称';`

​	**修改数据类型**

​	`ALTER TABLE 表名 MODIFY 字段名 新数据类型 (长度); `

​	**修改字段名和字段类型**

​	`ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型 (长度) [ COMMENT 注释 ] [ 约束 ];`

​	**案例: **

​	将emp表的nickname字段修改为username，类型为varchar(30)

​	`ALTER TABLE emp CHANGE nickname username varchar(30) COMMENT '昵称';`

​	**删除字段**

​	`ALTER TABLE 表名 DROP 字段名; `

​	**案例:** 

​	**将emp表的字段username删除**

​	`ALTER TABLE emp DROP username;`

​	**修改表名**

​	`ALTER TABLE 表名 RENAME TO 新表名; `

​	**案例:**

​	将emp表的表名修改为 employee

​	`ALTER TABLE emp RENAME TO employee; `

#### 删除表

​	**删除表**

​	`DROP TABLE [ IF EXISTS ] 表名; `

​	可选项 IF EXISTS 代表，只有表名存在时才会删除该表，表名不存在，则不执行删除操作(如果不加该参数项，删除一张不存在的表，执行将会报错)。	

​	**案例:**

​	如果tb_user表存在，则删除tb_user表 

​	`DROP TABLE IF EXISTS tb_user; `

​	**删除指定表, 并重新创建表**

`TRUNCATE TABLE 表名; `

## 图形化界面工具

​	上述，我们已经讲解了通过DDL语句，如何操作数据库、操作表、操作表中的字段，而通过DDL语句执行在命令进行操作，主要存在以下两点问题：

​		会影响开发效率

​		使用起来，并不直观，并不方便

​	所以呢，我们在日常的开发中，会借助于MySQL的图形化界面，来简化开发，提高开发效率。而目前mysql主流的图形化界面工具，有以下几种：

​	![](E:\图片\笔记\2.png)

​	我们使用DataGrip，这种图形化界面工具，功能更加强大，界面提示更加友好

### 安装

- ​	找到资料中准备好的安装包，双击开始安装

  - ![](E:\图片\笔记\3.png)\




- ​	 点击next，一步一步的完成安装

  - ![](E:\图片\笔记\4.png)\




- ​	选择DataGrip的安装目录，然后选择下一步

  - ![](E:\图片\笔记\5.png)\

  - ![](E:\图片\笔记\6.png)\

- ​	下一步，执行安装

  - ![](E:\图片\笔记\7.png)\
  - ![](E:\图片\笔记\8.png)\


### 使用

- ​	添加数据源

  - ![](E:\图片\笔记\9.png)\
  - 配置以及驱动jar包下载完毕之后，就可以点击 "Test Connection" 就可以测试，是否可以连接MySQL，如果出现 "Successed"，就表名连接成功了 。
  - ![](E:\图片\笔记\10.png)\

  

- ​	展示所有数据库

  - 连接上了MySQL服务之后，并未展示出所有的数据库，此时，我们需要设置，展示所有的数据库，具体操作如下：
  - ##### ![](E:\图片\笔记\11.png)\

- ​	创建数据库

  - ![](E:\图片\笔记\12.png)\
  - 注意:以下两种方式都可以创建数据库：
    - `create database db01;`
    - `create schema db01;`

- ​	创建表

  - 在指定的数据库上面右键，选择new --> Table
  - ![](E:\图片\笔记\13.png)\
  - ![](E:\图片\笔记\14.png)\

- ​	修改表结构

  - 在需要修改的表上，右键选择 "Modify Table...
  - ![](E:\图片\笔记\15.png)\
  - 如果想增加字段，直接点击+号，录入字段信息，然后点击Execute即可。
  - 如果想删除字段，直接点击-号，就可以删除字段，然后点击Execute即可。
  - 如果想修改字段，双击对应的字段，修改字段信息，然后点击Execute即可。
  - 如果要修改表名，或表的注释，直接在输入框修改，然后点击Execute即可。

- ​	在DataGrip中执行SQL语句

  - 在指定的数据库上，右键，选择 New --> Query Console
  - ![](E:\图片\笔记\16.png)\

  

## DML

- DML英文全称是Data Manipulation Language(数据操作语言)，用来对数据库中表的数据记录进行增、删、改操作。
  - 添加数据（INSERT）
  - 修改数据（UPDATE）
  - 删除数据（DELETE）

### 添加数据

- ​	给指定字段添加数据 

  - `INSERT INTO 表名 (字段名1, 字段名2, ...) VALUES (值1, 值2, ...);`

  - 案例: 给employee表所有的字段添加数据 ；

    - ```sql
      insert into employee(id,workno,name,gender,age,idcard,entrydate) values(1,'1','Itcast','男',10,'123456789012345678','2000-01-01');
      ```

    - 插入数据完成之后，我们有两种方式，查询数据库的数据：

    - 方式一

      - 在左侧的表名上双击，就可以查看这张表的数据。

      - ![image-20220817163505286](E:\图片\笔记\17)\

      - 方式二

        - 可以直接一条查询数据的SQL语句, 语句如下

          `select *from employee`

        - 案例: 给employee表所有的字段添加数据

        - 执行如下SQL，添加的年龄字段值为-1。

        - ```sql
          insert into employee(id,workno,name,gender,age,idcard,entrydate) 
          values(1,'1','Itcast','男',-1,'123456789012345678','2000-01-01');
          ```

        - 执行上述的SQL语句时，报错了，具体的错误信息如下：

        - ![image-20220817163644178](E:\图片\笔记\18)\

        - 因为 employee 表的age字段类型为 tinyint，而且还是无符号的 unsigned ，所以取值只能在0-255 之间

        - ![](E:\图片\笔记\19.png)\

- ​	给全部字段添加数据

  - `INSERT INTO 表名 VALUES (值1, 值2, ...); `

  - 案例：插入数据到employee表，具体的SQL如下：

    1. ```sql
       insert into employee values(2,'2','张无忌','男',18,'123456789012345670','2005-01- 01'); 
       ```

       

- ​	批量添加数据

  - ```sql
    INSERT INTO 表名 (字段名1, 字段名2, ...) VALUES (值1, 值2, ...), (值1, 值2, ...), (值 1, 值2, ...) ;
    INSERT INTO 表名 VALUES (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...) ;
    ```

  - 案例：批量插入数据到employee表，具体的SQL如下：

    - ```sql
      insert into employee 
      values(3,'3','韦一笑','男',38,'123456789012345670','2005-01- 01'),
      (4,'4','赵敏','女',18,'123456789012345670','2005-01-01');
      ```

  - 注意事项:

    - 插入数据时，指定的字段顺序需要与值的顺序是一一对应的
    - 字符串和日期型数据应该包含在引号中
    - 插入的数据大小，应该在字段的规定范围内

### 修改数据

- ​	修改数据的具体语法为:

  ​	`UPDATE 表名 SET 字段名1 = 值1 , 字段名2 = 值2 , .... [ WHERE 条件 ] ;`

- ​	案例:

  - 修改id为1的数据，将name修改为itheima

    `update employee set name = 'itheima' where id = 1; `

  - 修改id为1的数据, 将name修改为小昭, gender修改为 女

    `update employee set name = '小昭',gender = '女' where id = 1`

  - 将所有的员工入职日期修改为 2008-01-01

    `update employee  set entrydate = '2008-01-01'`

- ​	注意事项:

  - 修改语句的条件可以有，也可以没有，如果没有条件，则会修改整张表的所有数据

### 删除数据

- ​	删除数据的具体语法为：

  ​	`DELETE FROM 表名 [ WHERE 条件 ] ; `

- 案例:

  - 删除gender为女的员工

    `delete from employee where gender = '女'`

  - 删除所有员工

    `delete from employee`

- 注意事项:

  - DELETE 语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据
  - DELETE 语句不能删除某一个字段的值(可以使用UPDATE，将该字段值置为NULL即 可)
  - 当进行删除全部数据操作时，datagrip会提示我们，询问是否确认删除，我们直接点击Execute即可
  - ![](E:\图片\笔记\20.png)\

## DQL

- ​	DQL英文全称是Data Query Language(数据查询语言)，数据查询语言，用来查询数据库中表的记录

- ​	查询关键字: SELECT

- ​	在一个正常的业务系统中，查询操作的频次是要远高于增删改的，当我们去访问企业官网、电商网站，在这些网站中我们所看到的数据，实际都是需要从数据库中查询并展示的。而且在查询的过程中，可能还会涉及到条件、排序、分页等操作

- ​	准备如下数据:

  ```sql
  drop table if exists employee;
  
  create table emp( 
      id int comment '编号', 
      workno varchar(10) comment '工号', 
      name varchar(10) comment '姓名', 
      gender char(1) comment '性别', 
      age tinyint unsigned comment '年龄', 
      idcard char(18) comment '身份证号', 
      workaddress varchar(50) comment '工作地址',
      entrydate date comment '入职时间' 
  )comment '员工表'; 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (1, '00001', '柳岩666', '女', 20, '123456789012345678', '北京', '2000-01- 01');
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (2, '00002', '张无忌', '男', 18, '123456789012345670', '北京', '2005-09- 01');
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (3, '00003', '韦一笑', '男', 38, '123456789712345670', '上海', '2005-08- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (4, '00004', '赵敏', '女', 18, '123456757123845670', '北京', '2009-12-01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (5, '00005', '小昭', '女', 16, '123456769012345678', '上海', '2007-07-01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (6, '00006', '杨逍', '男', 28, '12345678931234567X', '北京', '2006-01-01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (7, '00007', '范瑶', '男', 40, '123456789212345670', '北京', '2005-05-01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (8, '00008', '黛绮丝', '女', 38, '123456157123645670', '天津', '2015-05- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (9, '00009', '范凉凉', '女', 45, '123156789012345678', '北京', '2010-04- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (10, '00010', '陈友谅', '男', 53, '123456789012345670', '上海', '2011-01- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (11, '00011', '张士诚', '男', 55, '123567897123465670', '江苏', '2015-05- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (12, '00012', '常遇春', '男', 32, '123446757152345670', '北京', '2004-02- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (13, '00013', '张三丰', '男', 88, '123656789012345678', '江苏', '2020-11- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (14, '00014', '灭绝', '女', 65, '123456719012345670', '西安', '2019-05- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (15, '00015', '胡青牛', '男', 70, '12345674971234567X', '西安', '2018-04- 01'); 
  INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES (16, '00016', '周芷若', '女', 18, null, '北京', '2012-06-01');
  ```

### 基本语法

- ​	DQL 查询语句，语法结构如下：

  ```sql
  SELECT
  	字段列表 
  FROM
  	表名列表 
  WHERE
  	条件列表 
  GROUP BY 
  	分组字段列表 
  HAVING
  	分组后条件列表 
  ORDER BY 
  	排序字段列表 
  LIMIT
  	分页参数
  ```

- ​	我们在讲解这部分内容的时候，会将上面的完整语法进行拆分，分为以下几个部分：

  - 基本查询（不带任何条件）
  - 条件查询（WHERE）
  - 聚合函数（count、max、min、avg、sum）
  - 分组查询（group by）
  - 排序查询（order by）
  - 分页查询（limit） 

### 基础查询

在基本查询的DQL语句中，不带任何的查询条件，查询的语法如下

- ​	查询多个字段

  ```sql
  SELECT 字段1, 字段2, 字段3 ... FROM 表名 ; 
  SELECT * FROM 表名 ;
  -- 注意 : * 号代表查询所有字段，在实际开发中尽量少用（不直观、影响效率）。
  ```

- ​	字段设置别名

  ```sql
  SELECT 字段1 [ AS 别名1 ] , 字段2 [ AS 别名2 ] ... FROM 表名;
  SELECT 字段1 [ 别名1 ] , 字段2 [ 别名2 ] ... FROM 表名;
  ```

- ​	去除重复记录

  ```sql
  SELECT DISTINCT 字段列表 FROM 表名;
  ```

- ​    案例

  - 查询指定字段 name, workno, age并返回

    `select name,workno,age from emp`

  - 查询返回所有字段

    `select id ,workno,name,gender,age,idcard,workaddress,entrydate from emp`

    `select * from emp`

  - 查询所有员工的工作地址,起别名

    `select workaddress as '工作地址' from emp`

    省略 as

    `select workaddress '工作地址' from emp`

  - 查询公司员工的上班地址有哪些(不要重复) 

    `select distinct workaddress from emp`

### 条件查询

- ​	语法

  `SELECT 字段列表 FROM 表名 WHERE 条件列表 ; `

- ​	条件

  - 常用的比较运算符如下:

    ![](E:\图片\笔记\21.png)\

  - 常用的逻辑运算符如下:

    ![](E:\图片\笔记\22.png)\

  - 案例:

    - 查询年龄等于 88 的员工

      `select * from emp where age = 88`

    - 查询年龄小于 20 的员工信息

      `select * from emp where age < 20`

    - 查询年龄小于等于 20 的员工信息

      `select * from emp where age <= 20`

    - 查询没有身份证号的员工信息

      `select * from emp where idcard is null `

    - 查询有身份证号的员工信息

      `select * from emp where idcard is not null`

    - 查询年龄不等于 88 的员工信息

      `select * from emp where age != 88`

      `select * from emp where age <> 88`

    - 查询年龄在15岁(包含) 到 20岁(包含)之间的员工信息

      `select * from emp where age >= 15 and age <= 20`

      `select * from emp where age >=15 && age <= 20`

      `select * from emp where age betwenn 15 and 20`

    - 查询性别为 女 且年龄小于 25岁的员工信息

      `select * from emp where gender = '女' and age < 25 `

    - 查询年龄等于18 或 20 或 40 的员工信息

      `select * from emp where age = 18 or age = 20 or age = 40`

      `select * from emp where age in(18,20,40)`

    - 查询姓名为两个字的员工信息 _ %

      `select * from emp where link '__%'`

    - 查询身份证号最后一位是X的员工信息

      `select * from emp where idcard '%X'`

      `select * from emp where idcard '_________________X'`

### 聚合函数

- ​	介绍

  将一列数据作为一个整体，进行纵向计算

- ​    常见的聚合函数

  ![](E:\图片\笔记\23.png)\

- ​    语法

  `SELECT 聚合函数(字段列表) FROM 表名 ;`

  注意 : NULL值是不参与所有聚合函数运算的

  - 案例：

    - 统计该企业员工数量

      `select count(*) from emp	-- 统计的是总记录数 `

      `select count(idcard) from emp  -- 统计的是idcard字段不为null的记录数`

      对于count聚合函数，统计符合条件的总记录数，还可以通过 count(数字/字符串)的形式进行统计查询，比如：

      `select count(1) from emp; `

    - 统计该企业员工的平均年龄

      `select avg(age) from emp`

    - 统计该企业员工的最大年龄

      `select max(age) from emp`

    - 统计该企业员工的最小年龄

      `select min(age) from emp`

    - 统计西安地区员工的年龄之和

      `select sun(age) from emp`

### 分组查询

- ​	语法

  `SELECT 字段列表 FROM 表名 [ WHERE 条件 ] GROUP BY 分组字段名 [ HAVING 分组 后过滤条件 ]; `

- ​	where与having区别

  - 执行时机不同：where是分组之前进行过滤，不满足where条件，不参与分组；而having是分组之后对结果进行过滤

  - 判断条件不同：where不能对聚合函数进行判断，而having可以。

  - 注意事项:

    - 分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义
    - 执行顺序: where > 聚合函数 > having
    - 支持多字段分组, 具体语法为 : group by columnA,columnB

  - 案例:

    - 根据性别分组 , 统计男性员工 和 女性员工的数量

      `select count(*) from emp group by gender`

    - 根据性别分组 , 统计男性员工 和 女性员工的平均年龄

      `select gender,avg(age) emp group by gender`

    - 查询年龄小于45的员工 , 并根据工作地址分组 , 获取员工数量大于等于3的工作地址

      `select workaddress,count(*) address_count from emp where age < 45 droup by workaddress having address_count >= 3`

    - 统计各个工作地址上班的男性及女性员工的数量

      `select workaddress,gender,count(*) as '数量' from emp group by gender,workaddress`

### 排序查询

- ​	语法

  `SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1 , 字段2 排序方式2 ; `

- ​	排序方式

  - ASC : 升序(默认值)

  - DESC: 降序

  - 注意事项：

    -  如果是升序, 可以不指定排序方式ASC ;
    -  如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序 ;

  - 案例:

    - 根据年龄对公司的员工进行升序排序

      `select * from emp order by age asc`

      `select * from emp order by`

    - 根据入职时间, 对员工进行降序排序

      `select * from emp order by entrydate desc`

    - 根据年龄对公司的员工进行升序排序 , 年龄相同 , 再按照入职时间进行降序排序

      `select * from emp order by age asc , entrydate desc`

### 分页查询

- ​	分页操作在业务系统开发时，也是非常常见的一个功能，我们在网站中看到的各种各样的分页条，后台都需要借助于数据库的分页操作。

- ​	语法

  - `SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询记录数 ;`
  - 注意事项:
    -  起始索引从0开始，起始索引 = （查询页码 - 1）* 每页显示记录数。
    -  分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT。
    -  如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10。
  - 案例:
    - 查询第1页员工数据, 每页展示10条记录
    - 查询第2页员工数据, 每页展示10条记录 --------> (页码-1)*页展示记录数

- 案例

  - 查询年龄为20,21,22,23岁的员工信息。

    `select * from emp where age in(20,21,22,23)`

  - 查询性别为 男 ，并且年龄在 20-40 岁(含)以内的姓名为三个字的员工

    `select * from emp gender = '男' adn age between 20,40 and name link '%___'`

  - 统计员工表中, 年龄小于60岁的 , 男性员工和女性员工的人数

    `select gender,count(*) from emp where age < 60 group by gender`

  - 查询所有年龄小于等于35岁员工的姓名和年龄，并对查询结果按年龄升序排序，如果年龄相同按入职时间降序排序

    `select age,name from emp where age <= 35 ordey by age asc,entrydate desc`

  - 查询性别为男，且年龄在20-40 岁(含)以内的前5个员工信息，对查询的结果按年龄升序排序，年龄相同按入职时间升序排序

    `select * from emp where gender = '男' and age between 20 , 40 order by age asc,entrydate asc  limit 0,5`

### 执行顺序

- 在讲解DQL语句的具体语法之前，我们已经讲解了DQL语句的完整语法，及编写顺序，接下来，我们要来说明的是DQL语句在执行时的执行顺序，也就是先执行那一部分，后执行那一部分。
- ![](E:\图片\笔记\sql执行顺序.png)\
- 验证：
- 查询年龄大于15的员工姓名、年龄，并根据年龄进行升序排序
  - `select * from emp where age > 15 order by age asc`
- 在查询时，我们给emp表起一个别名 e，然后在select 及 where中使用该别名
  - `select e.name , e.age  from emp as e where e.age > 15 order by age asc `
- 执行上述SQL语句后，我们看到依然可以正常的查询到结果，此时就说明： from 先执行, 然后where 和 select 执行。那 where 和 select 到底哪个先执行呢?
- 此时，此时我们可以给select后面的字段起别名，然后在 where 中使用这个别名，然后看看是否可以执行成功。
  - `select e.name ename , e.age eage from emp e where eage > 15 order by age asc; `
- 执行上述SQL报错了:
  - ![](E:\图片\笔记\34.png)
  - 由此我们可以得出结论: from 先执行，然后执行 where ， 再执行select 。
- 接下来，我们再执行如下SQL语句，查看执行效果
  - `select e.name ename , e.age eage from emp e where e.age > 15 order by eage asc; `
  - 结果执行成功。 那么也就验证了: order by 是在select 语句之后执行的。
- 综上所述，我们可以看到DQL语句的执行顺序为： from ... where ... group by ...having ... select ... order by ... limit ...

## 函数

- 函数 是指一段可以直接被另一段程序调用的程序或代码。 也就意味着，这一段程序或代码在MySQL中 已经给我们提供了，我们要做的就是在合适的业务场景调用对应的函数完成对应的业务需求即可。 那 么，函数到底在哪儿使用呢？
- 我们先来看两个场景：
- ![](E:\图片\笔记\38.png)
- 在企业的OA或其他的人力系统中，经常会提供的有这样一个功能，每一个员工登录上来之后都能 够看到当前员工入职的天数。 而在数据库中，存储的都是入职日期，如 2000-11-12，那如果快速计 算出天数呢？
- 在做报表这类的业务需求中,我们要展示出学员的分数等级分布。而在数据库中，存储的是学生的 分数值，如98/75，如何快速判定分数的等级呢？
- 其实，上述的这一类的需求呢，我们通过MySQL中的函数都可以很方便的实现
- MySQL中的函数主要分为以下四类： 字符串函数、数值函数、日期函数、流程函数。

- 字符串函数

  - MySQL中内置了很多字符串函数，常用的几个如下：
  - ![](E:\图片\笔记\39.png)\
  - 演示如下：
    -  concat : 字符串拼接
       - `select concat('Hello' , ' MySQL');`
    -  lower : 全部转小写
       - `select lower('Hello');`
    -  upper : 全部转大写
       - `select upper('Hello');`
    -  lpad : 左填充
       - `select lpad('01', 5, '-');`
    -  rpad : 右填充
       - `select rpad('01', 5, '-');`
    -  trim : 去除空格
       - `select trim(' Hello MySQL ');`
    -  substring : 截取子字符串
       - `select substring('Hello MySQL',1,5);`
  - 案例:
    - ![](E:\图片\笔记\40.png)\
    - 由于业务需求变更，企业员工的工号，统一为5位数，目前不足5位数的全部在前面补0。比如： 1号员 工的工号应该为00001。
    - update emp set workno = lpad(workno, 5, '0');
    - 处理完毕后, 具体的数据为:
    - ![](E:\图片\笔记\41.png)\

- 数值函数

  - 常见的数值函数如下：
  - ![](E:\图片\笔记\42.png)\
  - 演示如下：
    -  ceil：向上取整
       - `select ceil(1.1);`
    -  floor：向下取整
       - `select floor(1.9);`
    -  mod：取模
       - `select mod(7,4);`
    -  rand：获取随机数
       - `select rand();`
    -  round：四舍五入
       - `select round(2.344,2);`
  - 案例：
    - 通过数据库的函数，生成一个六位数的随机验证码。
    - 思路： 获取随机数可以通过rand()函数，但是获取出来的随机数是在0-1之间的，所以可以在其基础 上乘以1000000，然后舍弃小数部分，如果长度不足6位，补0
    - `select lpad(round(rand()*1000000 , 0), 6, '0');`

- 日期函数

  - 常见的日期函数如下：
  - ![](E:\图片\笔记\43.png)\
  - 演示如下
    - curdate：当前日期
      - `select curdate();`
    - curtime：当前时间
      - `select curtime();`
    - now：当前日期和时间
      - `select now();`
    - YEAR , MONTH , DAY：当前年、月、日
      - `select YEAR(now()); `
      - `select MONTH(now()); `
      - `select DAY(now());`
    - date_add：增加指定的时间间隔
      - `select date_add(now(), INTERVAL 70 YEAR );`
    - datediff：获取两个日期相差的天数
      - `select datediff('2021-10-01', '2021-12-01');`
  - 案例：
    - 查询所有员工的入职天数，并根据入职天数倒序排序
    - 思路： 入职天数，就是通过当前日期 - 入职日期，所以需要使用datediff函数来完成。
    - `select name, datediff(curdate(), entrydate) as 'entrydays' from emp order by entrydays desc;`

- 流程函数

  - 流程函数也是很常用的一类函数，可以在SQL语句中实现条件筛选，从而提高语句的效率

  - ![](E:\图片\笔记\44.png)\

  - 演示如下：

    - if
      - `select if(false, 'Ok', 'Error');`
    - ifnull
      - `select ifnull('Ok','Default');`
      - `select ifnull('','Default');`
      - `select ifnull(null,'Default');`
    - case when then else end
      - 需求: 查询emp表的员工姓名和工作地址 (北京/上海 ----> 一线城市 , 其他 ----> 二线城市)
      - `select name (case workaddress when '北京' then '一线城市' when '上海' then '一线城市' else '二线城市' end) as '工作地址'`

  - 案例:

    - ```sql
      create table score(
      id int comment 'ID',
      name varchar(20) comment '姓名',
      math int comment '数学',
      english int comment '英语',
      chinese int comment '语文'
      ) comment '学员成绩表';
      insert into score(id, name, math, english, chinese) VALUES (1, 'Tom', 67, 88, 95), (2, 'Rose' , 23, 66, 90),(3,'Jack', 56, 98, 76);
      ```

    - 具体的SQL语句如下:

    - ```sql
      select id,name 
      	(case when math >= 85 then '优秀' when math >=60 then '及格' else '不及格' end ) as '数学',
      	(case when english >= 85 then '优秀' when english >=60 then '及格' else '不及格'end ) as '英语',
      	(case when chinese >= 85 then '优秀' when chinese >=60 then '及格' else '不及格'end ) as '语文' 
      from score
      ```

    - MySQL的常见函数我们学习完了，那接下来，我们就来分析一下，在前面讲到的两个函数的案例场景， 思考一下需要用到什么样的函数来实现?

    - 数据库中，存储的是入职日期，如 2000-01-01，如何快速计算出入职天数呢？ --------> 答案: datediff

    - 数据库中，存储的是学生的分数值，如98、75，如何快速判定分数的等级呢？ ----------> 答案: case ... when ...

## DCL

- DCL英文全称是**Data Control Language**(数据控制语言)，用来管理数据库用户、控制数据库的访问权限。

- ![](E:\图片\笔记\35.png)\

- 管理用户
  - 查询用户
  - `select * from mysql.user; `
  - 查询结果如下:
  - ![](E:\图片\笔记\36.png)
  - 其中 Host代表当前用户访问的主机, 如果为localhost, 仅代表只能够在当前本机访问，是不可以 远程访问的。 User代表的是访问该数据库的用户名。在MySQL中需要通过Host和User来唯一标识一 个用户

- 创建用户

  - ` CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';`

- 修改用户密码

  - `ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码' ;`

- 删除用户

  - `DROP USER '用户名'@'主机名' ;`

- 注意事项:

  - 在MySQL中需要通过用户名@主机名的方式，来唯一标识一个用户
  - 主机名可以使用 % 通配
  - 这类SQL开发人员操作的比较少，主要是DBA（ Database Administrator 数据库 管理员）使用

- 案例：

  - 创建用户itcast, 只能够在当前主机localhost访问, 密码123456;
    - `create user 'itcast'@'localhost' identified by '123456';`
  - 创建用户heima, 可以在任意主机访问该数据库, 密码123456;
    - `create user 'heima'@'%' identified by '123456';`
  - 修改用户heima的访问密码为1234;
    - `alter user 'heima'@'%' identified with mysql_native_password by '1234';`
  - 删除 itcast@localhost 用户
    - `drop user 'itcast'@'localhost';`

- 权限控制

  - MySQL中定义了很多种权限，但是常用的就以下几种：
  - ![](E:\图片\笔记\37.png)\
  - 上述只是简单罗列了常见的几种权限描述，其他权限描述及含义，可以直接参考官方文档。
  - 查询权限
    - `SHOW GRANTS FOR '用户名'@'主机名' ;`
  - 授予权限
    - `GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';`
  - 撤销权限
    - `REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';`
  - 注意事项：
    - 多个权限之间，使用逗号分隔
    - 授权时， 数据库名和表名可以使用 * 进行通配，代表所有。
  - 案例:
    -  查询 'heima'@'%' 用户的权限
       - `show grants for 'heima'@'%';`
    -  授予 'heima'@'%' 用户itcast数据库所有表的所有操作权限
       - `grant all on itcast.* to 'heima'@'%';`
    -  撤销 'heima'@'%' 用户的itcast数据库的所有权限
       - `revoke all on itcast.* from 'heima'@'%';`


## 约束

### 概述

- 概念：约束是作用于表中字段上的规则，用于限制存储在表中的数据。
- 目的：保证数据库中数据的正确、有效性和完整性。
- 分类:
- ![](E:\图片\笔记\45.png)\
- 注意：约束是作用于表中字段上的，可以在创建表/修改表的时候添加约束

### 约束演示

- 上面我们介绍了数据库中常见的约束，以及约束涉及到的关键字，那这些约束我们到底如何在创建表、 修改表的时候来指定呢，接下来我们就通过一个案例，来演示一下。

- 案例需求： 根据需求，完成表结构的创建。需求如下：

- ![](E:\图片\笔记\46.png)\

- 对应的建表语句为：

  - ```sql
    create table tb_user(
    	id int auto_tncrement primary key comment '唯一表示',
        name varchar(10) not null unique comment '姓名',
        age int check(age > 0 and age <= 120) comment '年龄',
        status char(1) default '1' comment '状态',
        gender char(1) comment '性别'
    );
    ```

- 在为字段添加约束时，我们只需要在字段之后加上约束的关键字即可，需要关注其语法。我们执行上面 的SQL把表结构创建完成，然后接下来，就可以通过一组数据进行测试，从而验证一下，约束是否可以 生效。

  - ```sql
    insert into tb_user(name,age,status,gender) values ('Tom1',19,'1','男'),('Tom2',25,'0','男');
    insert into tb_user(name,age,status,gender) values ('Tom3',19,'1','男');
    insert into tb_user(name,age,status,gender) values (null,19,'1','男');
    insert into tb_user(name,age,status,gender) values ('Tom3',19,'1','男');
    insert into tb_user(name,age,status,gender) values ('Tom4',80,'1','男');
    insert into tb_user(name,age,status,gender) values ('Tom5',-1,'1','男');
    insert into tb_user(name,age,status,gender) values ('Tom5',121,'1','男');
    insert into tb_user(name,age,gender) values ('Tom5',120,'男');
    ```

- 上面，我们是通过编写SQL语句的形式来完成约束的指定，那加入我们是通过图形化界面来创建表结构 时，又该如何来指定约束呢？ 只需要在创建表的时候，根据我们的需要选择对应的约束即可。

- ![](E:\图片\笔记\47.png)\

###  外键约束

- 介绍

  - 外键：用来让两张表的数据之间建立连接，从而保证数据的一致性和完整性。

  - 我们来看一个例子：

  - ![](E:\图片\笔记\48.png)\

  - 左侧的emp表是员工表，里面存储员工的基本信息，包含员工的ID、姓名、年龄、职位、薪资、入职日 期、上级主管ID、部门ID，在员工的信息中存储的是部门的ID dept_id，而这个部门的ID是关联的 部门表dept的主键id，那emp表的dept_id就是外键,关联的是另一张表的主键。

  - 注意：目前上述两张表，只是在逻辑上存在这样一层关系；在数据库层面，并未建立外键关联， 所以是无法保证数据的一致性和完整性的。

  - 没有数据库外键关联的情况下，能够保证一致性和完整性呢，我们来测试一下

  - 准备数据

  - ```sql
    create table dept(
    id int auto_increment comment 'ID' primary key,
    name varchar(50) not null comment '部门名称'
    )comment '部门表';
    
    INSERT INTO dept (id, name) VALUES (1, '研发部'), (2, '市场部'),(3, '财务部'), (4,'销售部'), (5, '总经办');
    
    create table emp(
    id int auto_increment comment 'ID' primary key,
    name varchar(50) not null comment '姓名',
    age int comment '年龄',
    job varchar(20) comment '职位',
    salary int comment '薪资',
    entrydate date comment '入职时间',
    managerid int comment '直属领导ID',
    dept_id int comment '部门ID'
    )comment '员工表';
    
    INSERT INTO emp (id, name, age, job,salary, entrydate, managerid, dept_id)VALUES(1, '金庸', 66, '总裁',20000, '2000-01-01', null,5),
    (2, '张无忌', 20,'项目经理',12500, '2005-12-05', 1,1),
    (3, '杨逍', 33, '开发', 8400,'2000-11-03', 2,1),
    (4, '韦一笑', 48, '开发',11000, '2002-02-05', 2,1),
    (5, '常遇春', 43, '开发',10500, '2004-09-07', 3,1),
    (6, '小昭', 19, '程序员鼓励师',6600, '2004-10-12', 2,1);
    ```

  - ![](E:\图片\笔记\48.png)\

  - 接下来，我们可以做一个测试，删除id为1的部门信息

  - ![](E:\图片\笔记\49.png)\

  - 结果，我们看到删除成功，而删除成功之后，部门表不存在id为1的部门，而在emp表中还有很多的员 工，关联的为id为1的部门，此时就出现了数据的不完整性。 而要想解决这个问题就得通过数据库的 外键约束

- 语法

  - 添加外键

    - ```sql
      CREATE TABLE 表名(
      字段名 数据类型,
      ...
      [CONSTRAINT] [外键名称] FOREIGN KEY (外键字段名) REFERENCES 主表 (主表列名)
      );
      ```

    - ```sql
      ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名)
      REFERENCES 主表 (主表列名) ;
      ```

  - 案例:

    - 为emp表的dept_id字段添加外键约束,关联dept表的主键id。

    - ```sql
      alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references dept(id);
      ```

    - 添加了外键约束之后，我们再到dept表(父表)删除id为1的记录，然后看一下会发生什么现象。 此时 将会报错，不能删除或更新父表记录，因为存在外键约束。

    - ![](E:\图片\笔记\50.png)

  - 删除外键

    - `ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;`

  - 案例

    - 删除emp表的外键fk_emp_dept_id。
    - `alter table emp drop foreign key fk_emp_dept_id;`

- 删除/更新行为

  - 添加了外键之后，再删除父表数据时产生的约束行为，我们就称为删除/更新行为。具体的删除/更新行 为有以下几种:

  - ![](E:\图片\笔记\51.png)、

  - 具体语法为:

  - ```sql
    ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段) REFERENCES 主表名 (主表字段名) ON UPDATE CASCADE ON DELETE CASCADE;
    ```

  - 演示如下：

  - 由于NO ACTION 是默认行为，我们前面语法演示的时候，已经测试过了，就不再演示了，这里我们再 演示其他的两种行为：CASCADE、SET NULL。

  - CASCADE

    - ```sql
      alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references dept(id) on update cascade on delete cascade ;
      ```

    - 修改父表id为1的记录，将id修改为6

    - ![](E:\图片\笔记\52.png)\

    - 我们发现，原来在子表中dept_id值为1的记录，现在也变为6了，这就是cascade级联的效果。

    - 在一般的业务系统中，不会修改一张表的主键值。

    - 删除父表id为6的记录

    - ![](E:\图片\笔记\53.png)\

    - 我们发现，父表的数据删除成功了，但是子表中关联的记录也被级联删除了。

  -  SET NULL

    - 在进行测试之前，我们先需要删除上面建立的外键 fk_emp_dept_id。然后再通过数据脚本，将 emp、dept表的数据恢复了。

    - ```
      alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references dept(id) on update set null on delete set null ;
      ```

    - 接下来，我们删除id为1的数据，看看会发生什么样的现象。

    - ![](E:\图片\笔记\54.png)\

    - 我们发现父表的记录是可以正常的删除的，父表的数据删除之后，再打开子表 emp，我们发现子表emp 的dept_id字段，原来dept_id为1的数据，现在都被置为NULL了。

    - ![](E:\图片\笔记\55.png)\

## 多表查询

- ​	我们之前在讲解SQL语句的时候，讲解了DQL语句，也就是数据查询语句，但是之前讲解的查询都是单 表查询，而本章节我们要学习的则是多表查询操作，主要从以下几个方面进行讲解。

### 多表关系

- 项目开发中，在进行数据库表结构设计时，会根据业务需求及业务模块之间的关系，分析并设计表结 构，由于业务之间相互关联，所以各个表结构之间也存在着各种联系，基本上分为三种：
- 一对多(多对一)
- 多对多
- 一对一

- 一对多

  - 案例: 部门 与 员工的关系
  - 关系: 一个部门对应多个员工，一个员工对应一个部门实现: 
  - 在多的一方建立外键，指向一的一方的主键
  - ![](E:\图片\笔记\56.png)、

- 多对多

  - 案例: 学生 与 课程的关系

  - 关系: 一个学生可以选修多门课程，一门课程也可以供多个学生选择

  - 实现: 建立第三张中间表，中间表至少包含两个外键，分别关联两方主键

  - ![](E:\图片\笔记\57.png)、

  - 对应的SQL脚本:

  - ```sql
    create table student(
    	id int auto_increment primary key comment '主键ID',
    	name varchar(10) comment '姓名',
    	no varchar(10) comment '学号'
    ) comment '学生表';
    
    insert into student values (null, '黛绮丝', '2000100101'),(null, '谢逊','2000100102'),(null, '殷天正', '2000100103'),(null, '韦一笑', '2000100104');
    
    create table course(
    	id int auto_increment primary key comment '主键ID',
    	name varchar(10) comment '课程名称'
    ) comment '课程表';
    
    insert into course values (null, 'Java'), (null, 'PHP'), (null , 'MySQL') ,(null, 'Hadoop');
    
    create table student_course(
        id int auto_increment comment '主键' primary key,
    	studentid int not null comment '学生ID',
    	courseid int not null comment '课程ID',
    	constraint fk_courseid foreign key (courseid) references course (id),
    	constraint fk_studentid foreign key (studentid) references student (id)
    )comment '学生课程中间表';
    
    insert into student_course values (null,1,1),(null,1,2),(null,1,3),(null,2,2),(null,2,3),(null,3,4);
    ```

- 一对一

  - 案例: 用户 与 用户详情的关系

  - 关系: 一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其他详情字段放在另 一张表中，以提升操作效率

  - 实现: 在任意一方加入外键，关联另外一方的主键，并且设置外键为唯一的(UNIQUE)

  - ![](E:\图片\笔记\58.png)\

  - 对应的SQL脚本:

  - ```sql
    create table tb_user(  
    	id int auto_increment primary key comment '主键ID',
    	name varchar(10) comment '姓名',
    	age int comment '年龄',
    	gender char(1) comment '1: 男 , 2: 女',
    	phone char(11) comment '手机号'
    ) comment '用户基本信息表';
    
    create table tb_user_edu(
    	id int auto_increment primary key comment '主键ID',
    	degree varchar(20) comment '学历',
    	major varchar(50) comment '专业',
    	primaryschool varchar(50) comment '小学',
    	middleschool varchar(50) comment '中学',
        university varchar(50) comment '大学',
    	userid int unique comment '用户ID',
    	constraint fk_userid foreign key (userid) references tb_user(id)
    ) comment '用户教育信息表';
    
    insert into tb_user(id, name, age, gender, phone) values(null,'黄渤',45,'1','18800001111'),(null,'冰冰',35,'2','18800002222'),(null,'码云',55,'1','18800008888'),(null,'李彦宏',50,'1','18800009999');
    
    insert into tb_user_edu(id, degree, major, primaryschool, middleschool,university, userid) values
    (null,'本科','舞蹈','静安区第一小学','静安区第一中学','北京舞蹈学院',1),
    (null,'硕士','表演','朝阳区第一小学','朝阳区第一中学','北京电影学院',2),
    (null,'本科','英语','杭州市第一小学','杭州市第一中学','杭州师范大学',3),
    (null,'本科','应用数学','阳泉第一小学','阳泉区第一中学','清华大学',4);
    ```

### 多表查询概述

- ​	数据准备

  -  删除之前 emp, dept表的测试数据

  - 执行如下脚本，创建emp表与dept表并插入测试数据

  - ```sql
    -- 创建dept表，并插入数据
    create table dept(
    	id int auto_increment comment 'ID' primary key,
    	name varchar(50) not null comment '部门名称'
    )comment '部门表';
    
    INSERT INTO dept (id, name) VALUES (1, '研发部'), (2, '市场部'),(3, '财务部'), (4,'销售部'), (5, '总经办'), (6, '人事部');
    -- 创建emp表，并插入数据
    
    create table emp(
    	id int auto_increment comment 'ID' primary key,
        name varchar(50) not null comment '姓名',
    	age int comment '年龄',
    	job varchar(20) comment '职位',
    	salary int comment '薪资',
    	entrydate date comment '入职时间',
    	managerid int comment '直属领导ID',
    	dept_id int comment '部门ID'
    )comment '员工表';
    
    -- 添加外键
    alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references dept(id);
    
    INSERT INTO emp (id, name, age, job,salary, entrydate, managerid, dept_id)
    VALUES
    (1, '金庸', 66, '总裁',20000, '2000-01-01', null,5),
    (2, '张无忌', 20, '项目经理',12500, '2005-12-05', 1,1),
    (3, '杨逍', 33, '开发', 8400,'2000-11-03', 2,1),
    (4, '韦一笑', 48, '开发',11000, '2002-02-05', 2,1),
    (5, '常遇春', 43, '开发',10500, '2004-09-07', 3,1),
    (6, '小昭', 19, '程序员鼓励师',6600, '2004-10-12', 2,1),
    (7, '灭绝', 60, '财务总监',8500, '2002-09-12', 1,3),
    (8, '周芷若', 19, '会计',48000, '2006-06-02', 7,3),
    (9, '丁敏君', 23, '出纳',5250, '2009-05-13', 7,3),
    (10, '赵敏', 20, '市场部总监',12500, '2004-10-12', 1,2),
    (11, '鹿杖客', 56, '职员',3750, '2006-10-03', 10,2),
    (12, '鹤笔翁', 19, '职员',3750, '2007-05-09', 10,2),
    (13, '方东白', 19, '职员',5500, '2009-02-12', 10,2),
    (14, '张三丰', 88, '销售总监',14000, '2004-10-12', 1,4),
    (15, '俞莲舟', 38, '销售',4600, '2004-10-12', 14,4),
    (16, '宋远桥', 40, '销售',4600, '2004-10-12', 14,4),
    (17, '陈友谅', 42, null,2000, '2011-10-12', 1,null);
    ```

- 概述

  - 多表查询就是指从多张表中查询数据。
  - 原来查询单表数据，执行的SQL形式为：select * from emp;
  - 那么我们要执行多表查询，就只需要使用逗号分隔多张表即可，如： select * from emp , dept ; 具体的执行结果如下:
  - 
  - 此时,我们看到查询结果中包含了大量的结果集，总共102条记录，而这其实就是员工表emp所有的记录 (17) 与 部门表dept所有记录(6) 的所有组合情况，这种现象称之为笛卡尔积。接下来，就来简单 介绍下笛卡尔积
  - 笛卡尔积: 笛卡尔乘积是指在数学中，两个集合A集合 和 B集合的所有组合情况。
  - ![59](E:\图片\笔记\59.png)\
  - 而在多表查询中，我们是需要消除无效的笛卡尔积的，只保留两张表关联部分的数据
  - ![](E:\图片\笔记\60.png)\
  - 在SQL语句中，如何来去除无效的笛卡尔积呢？ 我们可以给多表查询加上连接查询的条件即可
  - `select * from emp , dept where emp.dept_id = dept.id`
  - 
  - 而由于id为17的员工，没有dept_id字段值，所以在多表查询时，根据连接查询的条件并没有查询 到。

- 分类

  - 连接查询
    - 内连接：相当于查询A、B交集部分数据
    - 外连接：
    - 左外连接：查询左表所有数据，以及两张表交集部分数据
    - 右外连接：查询右表所有数据，以及两张表交集部分数据
    - 自连接：当前表与自身的连接查询，自连接必须使用表别名
  - 子查询
    - ![](E:\图片\笔记\61.png)\

### 内连接

- ![](E:\图片\笔记\62.png)、内连接查询的是两张表交集部分的数据。(也就是绿色部分的数据)

- 内连接的语法分为两种: 隐式内连接、显式内连接。先来学习一下具体的语法结构

  - 隐式内连接
    - `SELECT 字段列表 FROM 表1 , 表2 WHERE 条件 ... ;`
  - 显式内连接
    - `SELECT 字段列表 FROM 表1 [ INNER ] JOIN 表2 ON 连接条件 ... ;`

- 案例:

  - 查询每一个员工的姓名 , 及关联的部门的名称 (隐式内连接实现)

  - 表结构: emp , dept

  - 连接条件: emp.dept_id = dept.id

  - ```sql
    select emp.name ,dept.name from emp,dept where emp.dep_id = dept.id
    -- 为每一张表起别名,简化SQL编写
    selecr e.name,d.naem from emp as e,dept as d where e.dep_id = d.id;
    ```

  - 查询每一个员工的姓名 , 及关联的部门的名称 (显式内连接实现) --- INNER JOIN ... ON ...

  - 表结构: emp , dept

  - 连接条件: emp.dept_id = dept.id

  - ```sql
    select e.name, d.name from emp e inner join dept d on e.dept_id = d.id;
    -- 为每一张表起别名,简化SQL编写
    select e.name, d.name from emp e join dept d on e.dept_id = d.id;
    ```

- 表的别名:

  - tablea as 别名1 , tableb as 别名2 ;
  - tablea 别名1 , tableb 别名2 ;

- 注意事项:

  - 一旦为表起了别名，就不能再使用表名来指定对应的字段了，此时只能够使用别名来指定字 段。

### 外连接

- ![](E:\图片\笔记\62.png)\

- 外连接分为两种，分别是：左外连接 和 右外连接。具体的语法结构为：

-  左外连接

  - ```sql
    SELECT 字段列表 FROM 表1 LEFT [ OUTER ] JOIN 表2 ON 条件 ... ;
    ```

  - 左外连接相当于查询表1(左表)的所有数据，当然也包含表1和表2交集部分的数据。

- 右外连接

  - ```sql
    SELECT 字段列表 FROM 表1 RIGHT [ OUTER ] JOIN 表2 ON 条件 ... ;
    ```

  - 右外连接相当于查询表2(右表)的所有数据，当然也包含表1和表2交集部分的数据

- 案例:

  - 查询emp表的所有数据, 和对应的部门信息

    - 由于需求中提到，要查询emp的所有数据，所以是不能内连接查询的，需要考虑使用外连接查询。

    - 表结构: emp, dept

    - 连接条件: emp.dept_id = dept.id

    - ```sql
      select e.*,d.name from emp as e left outer join dept as d on e.dept_id = d.id
      
      select e.*,d.name from emp as e left join dept as d on e.dept_id = d.id
      ```

  -  查询dept表的所有数据, 和对应的员工信息(右外连接)

    - 由于需求中提到，要查询dept表的所有数据，所以是不能内连接查询的，需要考虑使用外连接查 询。

    - 表结构: emp, dept

    - 连接条件: emp.dept_id = dept.id

    - ```sql
      select d.*,e.* from emp as e right outer join dept as d on e.dept_id = d.id
      
      select d.*,e.* from emp as e roght join dept as d on e.dept_id = d.id 
      ```

- 注意事项：

  - 左外连接和右外连接是可以相互替换的，只需要调整在连接查询时SQL中，表结构的先后顺 序就可以了。而我们在日常开发使用时，更偏向于左外连接

### 自连接

- 自连接查询

  - 自连接查询，顾名思义，就是自己连接自己，也就是把一张表连接查询多次。我们先来学习一下自连接 的查询语法：

  - `SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件 ... ;`

  - 而对于自连接查询，可以是内连接查询，也可以是外连接查询。

  - 案例：

    -  查询员工 及其 所属领导的名字 表结构: emp

      - ```sql
        select a.name ,b.name from emp as a,emp as b where a.managerid  = b.id
        ```

    - 查询所有员工 emp 及其领导的名字 emp , 如果员工没有领导, 也需要查询出来 表结构: emp a , emp b

    - ```sql
      select a.name as '员工',b.name as '领导' from emp as a left join emp as b on amanagerid = b.id
      ```

  - 注意事项:

    - 在自连接查询中，必须要为表起别名，要不然我们不清楚所指定的条件、返回的字段，到底 是哪一张表的字段。

- 联合查询

  - 对于union查询，就是把多次查询的结果合并起来，形成一个新的查询结果集。

  - ```sql
    SELECT 字段列表 FROM 表A ...
    UNION [ ALL ]
    SELECT 字段列表 FROM 表B ....;
    ```

  - 对于联合查询的多张表的列数必须保持一致，字段类型也需要保持一致

  - union all 会将全部的数据直接合并在一起，union 会对合并之后的数据去重

  - 案例:

    - 将薪资低于 5000 的员工 , 和 年龄大于 50 岁的员工全部查询出来.

    - 当前对于这个需求，我们可以直接使用多条件查询，使用逻辑运算符 or 连接即可。 那这里呢，我们 也可以通过union/union all来联合查询.

    - ```sql
      select * from emp where salary < 5000
      union all
      select * from emp where age > 50
      ```

    - union all查询出来的结果，仅仅进行简单的合并，并未去重。

    - ```sql
      select * from emp where salary < 5000
      union
      select * from emp where age > 50
      ```

    - union 联合查询，会对查询出来的结果进行去重处理。

  - 注意：

    - 如果多条查询语句查询出来的结果，字段数量不一致，在进行union/union all联合查询时，将会报 错。如：

### 子查询

- ​	概述

  - SQL语句中嵌套SELECT语句，称为嵌套查询，又称子查询。

  - ```sql
    SELECT * FROM t1 WHERE column1 = ( SELECT column1 FROM t2 );
    ```

  - 子查询外部的语句可以是INSERT / UPDATE / DELETE / SELECT 的任何一个。

- 分类

  - 根据子查询结果不同，分为：
    -  标量子查询（子查询结果为单个值）
    - 列子查询(子查询结果为一列)
    -  行子查询(子查询结果为一行)
    - 表子查询(子查询结果为多行多列)
  - 根据子查询位置，分为：
    - WHERE之后
    - FROM之后
    - SELECT之后

- 标量子查询

  - 子查询返回的结果是单个值（数字、字符串、日期等），最简单的形式，这种子查询称为标量子查询。 常用的操作符：= <> > >= < <= 

  - 案例:

    - 查询 "销售部" 的所有员工信息

      - 完成这个需求时，我们可以将需求分解为两步：

      - 查询 "销售部" 部门ID

      - ```sql
        select id from dept where name = '销售部'
        ```

      - 根据 "销售部" 部门ID, 查询员工信息

      - ```sql
        select * from emp where dept_id = (select id from dept where naem = '销售部');
        ```

    - 查询在 "方东白" 入职之后的员工信息

      - 完成这个需求时，我们可以将需求分解为两步：

      -  查询 方东白 的入职日期

      - ```sql
        select entrydate from emp where name = '东方白'
        ```

      -  查询指定入职日期之后入职的员工信息

      - ```sql
        select * from emp where entrydate > (select entrydate from emp where name='东方白');
        ```

- 列子查询

  - 子查询返回的结果是一列（可以是多行），这种子查询称为列子查询。

  - 常用的操作符：IN 、NOT IN 、 ANY 、SOME 、 ALL

  - ![](E:\图片\笔记\63.png)\

  - 案例:

    - 查询 "销售部" 和 "市场部" 的所有员工信息

      - 分解为以下两步:

      - 查询 "销售部" 和 "市场部" 的部门ID

      - ```sql
        select id from dept where name ='销售部' or name ='市场部';
        ```

      -  根据部门ID, 查询员工信息

      - ```sql
        select * from emp where dept_id in (select id from dept where naem = '销售部' or name ='市场部');
        ```

    - 查询比 财务部 所有人工资都高的员工信息

      - 分解为以下两步:

      - 查询所有 财务部 人员工资

      - ```sql
        select id from dept where name = '财务部';
        
        select salary from emp where dept_id = (select id from dept where name = '财务部');
        ```

      - 比 财务部 所有人工资都高的员工信息

      - ```sql
        select * from emp where salary > all(select salary from emp where dept_id =(select id from dept where name = '财务部'));
        ```

    - 查询比研发部其中任意一人工资高的员工信息

      - 分解为以下两步:

      - 查询研发部所有人工资

      - ```sql
        select id from dept where name ='研发部';
        
        select salary from emp where dept_id=(select id from dept where name = '研发部')
        ```

      - 比研发部其中任意一人工资高的员工信息

      - ```sql
        select * from emp where salary > all(select salary from emp where dept_id =(select id from dept where name = '研发部'));
        ```

- 行子查询

  - 子查询返回的结果是一行（可以是多列），这种子查询称为行子查询。

  - 常用的操作符：= 、<> 、IN 、NOT IN

  - 案例:

    - 查询与 "张无忌" 的薪资及直属领导相同的员工信息 ;

      - 这个需求同样可以拆解为两步进行:

      -  查询 "张无忌" 的薪资及直属领导

      - ```sql
        select salary, managerid from emp where name = '张无忌'
        ```

      -  查询与 "张无忌" 的薪资及直属领导相同的员工信息

      - ```sql
        select * from emp where (salary,managerid) = (select salary, managerid from emp where name = '张无忌');
        ```

- 表子查询

  - 子查询返回的结果是多行多列，这种子查询称为表子查询。

  - 常用的操作符：IN

  - 案例:

    -  查询与 "鹿杖客" , "宋远桥" 的职位和薪资相同的员工信息

      - 分解为两步执行:

      - 查询 "鹿杖客" , "宋远桥" 的职位和薪资

      - ```sql
        select job,salary from emp where name = '鹿杖客' or name = '宋远桥';
        ```

      - 查询与 "鹿杖客" , "宋远桥" 的职位和薪资相同的员工信息

      - ```sql
        select * from emp where (job,salary) in (select job,salary from emp where name = '鹿杖客' or name = '宋远桥');
        ```

    - 查询入职日期是 "2006-01-01" 之后的员工信息 , 及其部门信息

      - 分解为两步执行:

      - 入职日期是 "2006-01-01" 之后的员工信息

      - ```sql
        select * from emp where entrydate > 2006-01-01
        ```

      - 查询这部分员工, 对应的部门信息

      - ```sql
        select e.*,d.* from (select * from emp where entrydate > 2006-01-01) as e left join dept as d on e.dept_id =d.id
        ```

### 多表查询案例

- 数据环境准备:

  - ```sql
    create table salgrade(
    grade int,
    losal int,
    hisal int
    ) comment '薪资等级表';
    insert into salgrade values (1,0,3000);
    insert into salgrade values (2,3001,5000);
    insert into salgrade values (3,5001,8000);
    insert into salgrade values (4,8001,10000);
    insert into salgrade values (5,10001,15000);
    insert into salgrade values (6,15001,20000);
    insert into salgrade values (7,20001,25000);
    insert into salgrade values (8,25001,30000);
    ```

- 在这个案例中，我们主要运用上面所讲解的多表查询的语法，完成以下的12个需求即可，而这里主要涉 及到的表就三张：emp员工表、dept部门表、salgrade薪资等级表 。

- 查询员工的姓名、年龄、职位、部门信息 （隐式内连接）

  - 表: emp , dept

  - 连接条件: emp.dept_id = dept.id

  - ```sql
    select e.name,e.age,e.job,d.name fr om emp as e,dept as d where e.dept_id = d.id
    ```

-  查询年龄小于30岁的员工的姓名、年龄、职位、部门信息（显式内连接）

  - 表: emp , dept

  - 连接条件: emp.dept_id = dept.id

  - ```sql
    select e.name,e.age,e.job,d.name from emp as e inner join dept as d on e.dept_id = d.id where age < 30
    ```

- 查询拥有员工的部门ID、部门名称

  - 表: emp , dept

  - 连接条件: emp.dept_id = dept.id

  - ```sql
    select distinct d.id,d.name , from emp as e,dept as d where e.dept_id = d.id
    ```

- 查询所有年龄大于40岁的员工, 及其归属的部门名称; 如果员工没有分配部门, 也需要展示出 来(外连接)

  - 表: emp , dept

  - 连接条件: emp.dept_id = dept.id

  - ```sql
    select e.*,d.name from emp as e left join dept as d on e.dept_id = d.id where e.age > 40
    ```

- 查询所有员工的工资等级

  - 表: emp , salgrade	

  - 连接条件 : emp.salary >= salgrade.losal and emp.salary <= salgrade.hisal

  - ```sql
    -- 方式一
    select e.* , s.grade , s.losal, s.hisal from emp e , salgrade s where e.salary >=s.losal and e.salary <= s.hisal;
    -- 方式二
    select e.* , s.grade , s.losal, s.hisal from emp e , salgrade s where e.salary between s.losal and s.hisal;
    ```

- 查询 "研发部" 所有员工的信息及 工资等级

  - 表: emp , salgrade , dept

  - 连接条件 : emp.salary between salgrade.losal and salgrade.hisal , emp.dept_id = dept.id

  - 查询条件 : dept.name = '研发部'

  - ```sql
    select e.* ,s.grade from emp as e,dept as d,salgrade as s where e.salary = d.id and (e.salary between s.losal and s.hisal ) and d.name = '研发部';
    ```

- 查询 "研发部" 员工的平均工资

  - 表: emp , dept

  - 连接条件 : emp.dept_id = dept.id

  - ```sql
    select avg(e.salary) from emp as e,dept as d where e.dept_id =d.id and d.name = '研发部';
    ```

-  查询工资比 "灭绝" 高的员工信息。

  -  查询 "灭绝" 的薪资

    - ```sql
      select salary from emp where name = '灭绝';
      ```

  - 查询比她工资高的员工数据

    - ```sql
      select * from emp where salary > (select salary from emp where name = '灭绝')
      ```

- 查询比平均薪资高的员工信息

  - 查询员工的平均薪资

    - ```sql
      select avg(salary) from emp
      ```

  - 查询比平均薪资高的员工信息

    - ```sql
      select * from emp where salary > (select avg(salary) from emp)
      ```

- 查询低于本部门平均工资的员工信息

  - 查询指定部门平均薪资

    - ```sql
      select avg(e1.salary) from emp e1 where e1.dept_id = 1;
      select avg(e1.salary) from emp e1 where e1.dept_id = 2;
      ```

  - 查询低于本部门平均工资的员工信息

    - ```sql
      select * from emp e2 where e2.salary < ( select avg(e1.salary) from emp e1 wheree1.dept_id = e2.dept_id );
      ```

- 查询所有的部门信息, 并统计部门的员工人数

  - ```sql
    select d.id, d.name , ( select count(*) from emp e where e.dept_id = d.id ) '人数'from dept d
    ```

- 查询所有学生的选课情况, 展示出学生名称, 学号, 课程名称

  - 表: student , course , student_course

  - 连接条件: student.id = student_course.studentid , course.id = student_course.courseid

  - ```sql
    select s.name , s.no , c.name from student s , student_course sc , course c where s.id = sc.studentid and sc.courseid = c.id ;
    ```

- 备注

  - 以上需求的实现方式可能会很多, SQL写法也有很多，只要能满足我们的需求，查询出符合条 件的记录即可

## 事务

### 事务简介

- 事务 是一组操作的集合，它是一个不可分割的工作单位，事务会把所有的操作作为一个整体一起向系 统提交或撤销操作请求，即这些操作要么同时成功，要么同时失败
- 就比如: 张三给李四转账1000块钱，张三银行账户的钱减少1000，而李四银行账户的钱要增加 1000。 这一组操作就必须在一个事务的范围内，要么都成功，要么都失败。
- ![](E:\图片\笔记\64.png)\
- 就比如: 张三给李四转账1000块钱，张三银行账户的钱减少1000，而李四银行账户的钱要增加 1000。 这一组操作就必须在一个事务的范围内，要么都成功，要么都失败。
- ![image-20220819151319897](E:\图片\笔记\65)\
- 异常情况: 转账这个操作, 也是分为以下这么三步来完成 , 在执行第三步是报错了, 这样就导致张 三减少1000块钱, 而李四的金额没变, 这样就造成了数据的不一致, 就出现问题了。
- ![](E:\图片\笔记\66.png)\
- 为了解决上述的问题，就需要通过数据的事务来完成，我们只需要在业务逻辑执行之前开启事务，执行 完毕后提交事务。如果执行过程中报错，则回滚事务，把数据恢复到事务开始之前的状态。
- ![](E:\图片\笔记\67.png)\
- 注意：
  - 默认MySQL的事务是自动提交的，也就是说，当执行完一条DML语句时，MySQL会立即隐 式的提交事务。

### 事务操作

- 数据准备：

  - ```sql
    drop table if exists account;
    
    create table account(
    	id int primary key AUTO_INCREMENT comment 'ID',
    	name varchar(10) comment '姓名',
    	money double(10,2) comment '余额'
    ) comment '账户表';
    
    insert into account(name, money) VALUES ('张三',2000), ('李四',2000);
    ```

- 未控制事务

  - 测试正常情况

    - ```sql
      -- 1. 查询张三余额
      select * from account where name = '张三';
      -- 2. 张三的余额减少1000
      update account set money = money - 1000 where name = '张三';
      -- 3. 李四的余额增加1000
      update account set money = money + 1000 where name = '李四'
      ```

    - 测试完毕之后检查数据的状态, 可以看到数据操作前后是一致的

    - ![](E:\图片\笔记\68.png)\

  - 测试异常情况

    - ```sql
      -- 1. 查询张三余额
      select * from account where name = '张三';
      -- 2. 张三的余额减少1000
      update account set money = money - 1000 where name = '张三';
      出错了....
      -- 3. 李四的余额增加1000
      update account set money = money + 1000 where name = '李四';
      ```

    - 我们把数据都恢复到2000， 然后再次一次性执行上述的SQL语句(出错了.... 这句话不符合SQL语 法,执行就会报错)，检查最终的数据情况, 发现数据在操作前后不一致了。

    - ![](E:\图片\笔记\69.png)\

- 控制事务一

  - 查看/设置事务提交方式

    - ```sql
      SELECT @@autocommit ;
      SET @@autocommit = 0 ;
      ```

  - 提交事务

    - ```sql
      COMMIT;
      ```

  - 回滚事务

    - ```sql
      ROLLBACK;
      ```

  - 注意：

    - 上述的这种方式，我们是修改了事务的自动提交行为, 把默认的自动提交修改为了手动提 交, 此时我们执行的DML语句都不会提交, 需要手动的执行commit进行提交。

- 控制事务二

  - 开启事务

    - ```sql
      START TRANSACTION 或 BEGIN ;
      ```

  - 提交事务

    - ```sql
      COMMIT
      ```

  - 回滚事务

    - ```sql
      ROLLBACK;
      ```

  - 转账案例：

    - ```sql
      -- 开启事务
      start transaction
      -- 1. 查询张三余额
      select * from account where name = '张三';
      -- 2. 张三的余额减少1000
      update account set money = money - 1000 where name = '张三';
      -- 3. 李四的余额增加1000
      update account set money = money + 1000 where name = '李四';
      -- 如果正常执行完毕, 则提交事务
      commit;
      -- 如果执行过程中报错, 则回滚事务
      -- rollback;
      ```

### 事务四大特性

- 原子性（Atomicity）：事务是不可分割的最小操作单元，要么全部成功，要么全部失败
- 一致性（Consistency）：事务完成时，必须使所有的数据都保持一致状态。
- 隔离性（Isolation）：数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行
- 持久性（Durability）：事务一旦提交或回滚，它对数据库中的数据的改变就是永久的
- 上述就是事务的四大特性，简称ACID。
- ![](E:\图片\笔记\70.png)\

### 并发事务问题

- 赃读：一个事务读到另外一个事务还没有提交的数据。
- ![](E:\图片\笔记\71.png)\
- 不可重复读：一个事务先后读取同一条记录，但两次读取的数据不同，称之为不可重复读。
- ![](E:\图片\笔记\72.png)\
-  幻读：一个事务按照条件查询数据时，没有对应的数据行，但是在插入数据时，又发现这行数据 已经存在，好像出现了 "幻影"。
- ![](E:\图片\笔记\73.png)\

### 事务隔离级别

- 为了解决并发事务所引发的问题，在数据库中引入了事务隔离级别。主要有以下几种：

- ![](E:\图片\笔记\74.png)\

- 查看事务隔离级别

  - ```sql
    SELECT @@TRANSACTION_ISOLATION;
    ```

- 设置事务隔离级别

  - ```sql
    SET [ SESSION | GLOBAL ] TRANSACTION ISOLATION LEVEL { READ UNCOMMITTED | READ COMMITTED | REPEATABLE READ | SERIALIZABLE}
    ```

- 注意

  - 事务隔离级别越高，数据越安全，但是性能越低