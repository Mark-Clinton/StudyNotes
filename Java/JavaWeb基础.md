<center>
    <h1>
        JavaWeb基础
    </h1>
</center>

## 1. JavaWeb课程介绍

**JavaWeb概念**

- 使用Java语言开发互联网项目。简单理解：使用Java语言开发网站

**学习路线**

- 数据库
- 网页前端
- Web核心技术
- 旅游管理系统

## 2. 数据库

### 2.1 数据库的基本概念

数据库的英文单词：DataBase。简称：DB

什么是数据库：用于存储和管理数据的仓库。

数据库的特点

- 持久化存储数据的。其实数据库就是一个文件系统。
- 方便存储和管理数据。
- 使用了统一的方式操作数据库。--SQL

常见的数据库软件：Oracle，MySQL，SQLServer，DB2等等

MySQL服务启动

- 手动
- cmd --> services.msc 打开服务的窗口
- 使用管理员打开cmd
  - net start mysql：启动mysql的服务
  - net stop mysql：关闭mysql的服务

MySQL登录

- mysql -uroot -proot：-u后为用户名，-p后为密码。
- mysql -hip -uroot -p连接目标的密码
- mysql --host=ip --user=root --password=连接目标的密码

MySQL退出

- exit
- quit

MySQL目录结构

1.MySQL安装目录

- 配置文件 my.ini

2.MySQL数据目录

- 几个概念
  - 数据库：文件夹
  - 表：文件
  - 数据

### 2.2 SQL基本概念

什么是SQL

- Structured Query Language：结构化查询语言。
- 其实就是定义了操作所有关系型数据库的规则。每一种数据库操作的方式存在不一样的地方，称为“方言”。

SQL通用语法

- SQL语句可以单行或多行书写，以分号结尾。
- 可使用空格和缩进来增强语句的可读性。
- MySQL数据库的SQL语句不区分大小写，关键字建议使用大写。
- 3种注释
  - 单行注释：-- 注释内容 或 # 注释内容(mysql 特有)
  - 多行注释：/* 注释 */

SQL分类

- DDL(Data Definition Language)数据定义语言
  - 用来定义数据库对象：数据库，表，列等。关键字：create，drop，alter等
- DML(Data Manipulation Language)数据操作语言
  - 用来对数据库中表的数据进行增删改。关键字：insert，delete，update等
- DQL(Data Query Language)数据查询语言
  - 用来查询数据库中表的记录(数据)。关键字：select，where等
- DCL(Data Control Language)数据控制语言
  - 用来定义数据库的访问权限和安全级别，及创建用户。关键字：GRANT，REVOKE等

### 2.3 SQL基本语法

**DDL：操作数据库，表**

操作数据库：CRUD

- C(Create) ：创建

  - 创建数据库
    - create database 数据库名称;
  - 创建数据库，判断不存在，再创建
    - create database if not exists 数据库名称;
  - 创建数据库，并指定字符集
    - create database 数据库名称 character set 字符集名;

  - 创建db4数据库，判断是否存在，并制定字符集为gbk
    - create database if not exists db4 character set gbk；

- R(Retrieve) ：查询

  - 查询所有数据库的名称
    - show databases;
  - 查询某个数据库的字符集：查看某个数据库的创建语句
    - show create database 数据库名称;

- U(Update) ：修改

  - 修改数据库的字符集
    - alter database 数据库名称 character set 字符集名称;

- D(Delete) ：删除

  - 删除数据库
    - drop database 数据库名称;
  - 判断数据库存在，存在再删除
    - drop database if exists 数据库名称;

- 使用数据库

  - 查询当前正在使用的数据库名称
    - select database();
  - 使用数据库
    - use 数据库名称;

操作表

- C(Create) ：创建

  - 创建表语法

    - ```SQL
      create table 表名(
          列名1 数据类型1,
          列名2 数据类型2,
          ....
          列名n 数据类型n
      );
      ```

    - 注意：最后一列，不需要加逗号(,)。

    - 常用数据库类型

      - 整数类型：int
      - 小数类型：double(共几位,小数位数)，
      - 日期：date，只包含年月日，yyyy-MM-dd
      - 日期时间：datetime，包含年月日，时分秒 yyyy-MM-dd HH:mm:ss
      - 时间戳类型：timestamp，包含年月日，时分秒 yyyy-MM-dd HH:mm:ss
        - 如果将来不给这个字段赋值，或赋值为null，则默认使用当前的系统时间，来自动赋值
      - 字符串：varchar
        - name varchar(20)：姓名最大20个字符

  - 案例

    - ```SQL
      create table student(
          id int,
          name varchar(32),
          age int,
          score double(4,1),
          birthday date,
          insert_time timestamp
      );
      ```

  - 复制表

    - create table 表名 like 被复制的表名;

- R(Retrieve) ：查询

  - 查询某个数据库中所有的表名称
    - show tables;
  - 查询表结构
    - desc 表名;

- U(Update) ：修改

  - 修改表名
    - alter table 表名 rename to 新的表名;
  - 修改表的字符集
    - alter table 表名 character set 字符集名称;
  - 添加一列
    - alter table 表名 add 列名 数据类型;
  - 修改列名称，类型
    - alter table 表名 change 列名 新列名 新数据类型;
    - alter table 表名 modify 列名 新数据类型;
  - 删除列
    - alter table 表名 drop 列名;

- D(Delete) ：删除

  - drop table 表名;
  - drop table if exists 表名;

客户端图形化工具：SQLYog

**DML：增删改表中数据**

1.添加数据

- 语法
  - insert into 表名(列名1, 列名2, ... 列名n) values(值1, 值2, ... 值n);
- 注意
  - 列名和值要一一对应。
  - 如果表名后，不定义列名，则默认给所有列添加值。
    - insert into 表名 values(值1, 值2, ... 值n);
  - 除了数字类型，其他类型需要使用引号(单双都可以)引起来。

2.删除数据

- 语法
  - delete from 表名 [where 条件];
- 注意
  - 如果不加条件，则删除表中所有记录。
  - 如果要删除所有记录
    - delete from 表名; --不推荐使用。有多少条记录就会执行多少次删除操作。
    - TRUNCATE TABLE 表名; --推荐使用，效率更高。先删除表，然后再创建一张一样的表。

3.修改数据

- 语法
  - update 表名 set 列名1 = 值1, 列名2 = 值2, ... [where 条件];
- 注意
  - 如果不加任何条件，则会将表中所有记录全部修改。

**DQL：查询表中的数据**

- select * from 表名;
- 语法
  - select 字段列表 from 表名列表 where 条件列表 group by 分组字段 having 分组之后的条件 order by 排序 limit 分页限定
- 基础查询
  - 多个字段的查询
    - select 字段名1, 字段名2, ... from 表名;
    - 如果查询所有字段，则可以使用*来替代字段列表。
  - 去除重复
    - distinct
  - 计算列
    - 一般可以使用四则运算计算一些列的值。(一般只会进行数值型的计算)。
    - ifnull(表达式1,表达式2)：null参与的运算，计算结果都为null。
      - 表达式1：哪个字段需要判断是否为null。
      - 表达式2：如果该字段为null后的替换值。
  - 起别名
    - as：as也可以省略。
- 条件查询
  - where子句后跟条件
  - 运算符
    - \>、< 、<=、>=、=、<>
    - BETWEEN...AND
    - IN(集合)
    - LIKE：模糊查询
      - 占位符
      - _：单个任意字符
      - %：多个任意字符
    - IS NULL
    - and 或 &&
    - or 或 ||
    - not 或 !
- 排序查询
  - 语法：order by 字句;
    - order by 排序字段1 排序方式1, 排序字段2 排序方式2...
  - 排序方式
    - ASC：升序，默认的。
    - DESC：降序。
  - 注意：如果有多个排序条件，则当前边的条件值一样时，才会判断第二条件。
- 聚合函数：将一列数据作为一个整体，进行纵向的计算。
  - count：计算个数
    - 一般选择非空的列：主键
    - count(*)
  - max：计算最大值
  - min：计算最小值
  - sum：计算和
  - avg：计算平均值
  - 注意：聚合函数的计算，排除null值。解决方案如下：
    - 选择不包含空值的列进行计算
    - IFNULL函数
- 分组查询
  - 语法：group by 分组字段;
  - 注意
    - 分组之后查询的字段：分组字段、聚合函数
    - where和having的区别
      - where在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果，则不会被查询出来
      - where后不可以跟聚合函数，having可以进行聚合函数的判断
- 分页查询
  - 语法：limit 开始的索引, 每页查询的条数;
  - 公式：开始的索引 =（当前的页码 - 1）* 每页显示的条数
  - 分页操作是一个“方言”

**DCL：管理用户，授权**

管理用户

- 添加用户

  - ```SQL
    -- 创建用户
    CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
    ```

- 删除用户

  - ```SQL
    -- 删除用户
    DROP USER '用户名'@'主机名';
    ```

- 修改用户密码

  - ```SQL
    -- 修改lisi用户密码为 abc
    UPDATE USER SET PASSWORD = PASSWORD('新密码') WHERE USER = '用户名';
    UPDATE USER SET PASSWORD = PASSWORD('abc') WHERE USER = 'lisi';
    FLUSH PRIVILEGES;
    
    SET PASSWORD FOR '用户名'@'主机名' = PASSWORD('新密码');
    SET PASSWORD FOR 'lisi'@'%' = PASSWORD('123');
    ```

  - mysql中忘记了root用户密码？

    - cmd --> net stop mysql 停止mysql服务(需要管理员运行该cmd)
    - 使用无验证方式启动mysql服务：mysql --skip-grant-tables
    - 打开新的cmd窗口，直接输入mysql命令，敲回车。就可以登录成功
    - use mysql;
    - UPDATE USER SET PASSWORD = PASSWORD('你的新密码') WHERE USER = 'root';
    - 关闭两个窗口
    - 打开任务管理器，手动结束mysql.exe的进程
    - 启动mysql服务
    - 使用新密码登录

- 查询用户

  - ```SQL
    -- 1.切换到mysql数据库
    USE mysql;
    -- 2.查询user表
    SELECT * FROM USER;
    ```

  - 通配符：%表示可以在任意主机使用用户登录数据库。

授权

- 查询权限

  - ```SQL
    -- 查询权限
    SHOW GRANTS FOR '用户名'@'主机名';
    SHOW GRANTS FOR 'lisi'@'%';
    ```

- 授予权限

  - ```SQL
    -- 授予权限
    GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
    GRANT SELECT,DELETE,UPDATE ON db3.account TO 'lisi'@'%';
    
    -- 给张三用户授予所有权限，在任意数据库任意表上
    GRANT ALL ON *.* TO 'zhangsan'@'localhost';
    ```

- 撤销权限

  - ```SQL
    -- 撤销权限
    REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
    REVOKE SELECT ON db3.account FROM 'lisi'@'%';
    ```

### 2.4 约束

**概念**：对表中的数据进行限定，保证数据的正确性、有效性和完整性。

**分类**

- 主键约束：primary key

- 非空约束：not null

- 唯一约束：unique

- 外键约束：foreign key

非空约束：not null，某一列的值不能为null

- 创建表时添加约束

- ```SQL
  CREATE TABLE stu(
  	id INT,
  	NAME VARCHAR(20) NOT NULL
  );
  ```

- 创建表完后，添加非空约束

- ```SQL
  ALTER TABLE stu MODIFY NAME VARCHAR(20) NOT NULL;
  ```

- 删除name的非空约束

- ```SQL
  ALTER TABLE stu MODIFY NAME VARCHAR(20);
  ```

唯一约束：unique，某一列的值不能重复

- 注意：唯一约束可以有null值，但是只能有一条记录为null

- 在创建表时，添加唯一约束

- ```SQL
  CREATE TABLE stu(
  	id INT,
  	phone_number VARCHAR(20) UNIQUE
  );
  ```

- 在表创建完后，添加唯一约束

- ```SQL
  ALTER TABLE stu MODIFY phone_number VARCHAR(20) UNIQUE;
  ```

- 删除唯一约束

- ```SQL
  ALTER TABLE stu DROP INDEX phone_number;
  ```

主键约束：primary key

- 含义：非空且唯一

- 一张表只能有一个字段为主键

- 主键就是表中记录的唯一标识

- 在创建表时，添加主键约束

- ```SQL
  CREATE TABLE stu(
  	id INT PRIMARY KEY,
      NAME VARCHAR(20)
  );
  ```

- 删除主键

- ```SQL
  ALTER TABLE stu DROP PRIMARY KEY;
  ```

- 创建完表后，添加主键

- ```SQL
  ALTER TABLE stu MODIFY id INT PRIMARY KEY;
  ```

- 自动增长

  - 概念：如果某一列是数值类型的，使用auto_increment可以来完成值的自动增长。

  - 在创建表时，添加主键约束，并且完成主键自动增长。

  - ```SQL
    CREATE TABLE stu(
    	id INT PRIMARY KEY AUTO_INCREMENT,
        NAME VARCHAR(20)
    );
    ```

  - 删除自动增长

  - ```SQL
    ALTER TABLE stu MODIFY id INT;
    ```

  - 添加自动增长

  - ```SQL
    ALTER TABLE stu MODIFY id INT AUTO_INCREMENT;
    ```

外键约束：foreign key

- 在创建表时，可以添加外键

- ```SQL
  create table 表名(
      ...
      外键列
      constraint 外键名称 foreign key (外键列名称) reference 主表名称(主表列名称)
  );
  ```

- 删除外键

- ```SQL
  ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
  ```

- 创建表之后，添加外键

- ```SQL
  ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);
  ```

- 级联操作

  - 添加级联操作

  - ```SQL
    ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称) ON UPDATE CASCADE ON DELETE CASCADE;
    ```

  - 级联更新：ON UPDATE CASCADE

  - 级联删除：ON DELETE CASCADE

### 2.5 数据库的设计

**多表之间的关系**

**分类**

一对一(了解)

- 如：人和身份证。
- 分析：一个人只有一个身份证，一个身份证只能对应一个人。

一对多(多对一)

- 如：部门和员工。
- 分析：一个部门有多个员工，一个员工只能对应一个部门。

多对多

- 如：学生和课程。
- 一个学生可以选择很多门课程，一个课程也可以被很多学生选择。

**实现关系**

- 一对多(多对一)
  - 实现方式：在多的一方建立外键，指向一的一方的主键。
- 多对多
  - 实现方式：多对多关系实现需要借助第三张中间表。中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两张表的主键。
- 一对一(了解)
  - 实现方式：一对一关系实现，可以在任意一方添加唯一外键指向另一方的主键。

**数据库设计的范式**

**概念：**设计数据库时，需要遵循的一些规范。要遵循后边的范式要求，必须先遵循前边的所有范式要求。

设计关系数据库时，遵从不同的规范要求，设计出合理的关系型数据库，这些不同的规范要求被称为不同的范式，各种范式呈递次规范，越高的范式数据库冗余越小。
关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。

**分类**

第一范式(1NF)：每一列都是不可分割的原子数据项。

第二范式(2NF)：在1NF的基础上，非码属性必须完全依赖于候选码（在1NF基础上消除非主属性对主码的部分函数依赖）。

- 几个概念
  - 函数依赖：A --> B，如果通过A属性(属性组)的值，可以确定唯一B属性的值。则称B依赖于A。
    - 如：学号 --> 姓名。(学号，课程名称) --> 分数
  - 完全函数依赖：A --> B，如果A是一个属性组，则B属性值的确定需要依赖于A属性组中所有的属性值。
    - 例如：(学号，课程名称) --> 分数
  - 部分函数依赖：A --> B，如果A是一个属性组，则B属性值的确定只需要依赖于A属性组中某一些值即可。
    - 例如：(学号，姓名，课程名称) --> 分数
  - 传递函数依赖：A --> B，B --> C，如果通过A属性(属性组)的值，可以确定唯一B属性的值，再通过B属性(属性组)的值可以确定唯一C属性的值，则称C传递函数依赖于A。
    - 例如：学号 --> 系名，系名 --> 系主任。
  - 码：如果在一张表中，一个属性或属性组，被其他所有属性所完全依赖，则称这个属性(属性组)为该表的码。
    - 例如：(学号，课程名称)。
    - 主属性：码属性组中的所有属性。
    - 非主属性：除过码属性组的属性。

第三范式(3NF)：在2NF基础上，任何非主属性不依赖于其它非主属性（在2NF基础上消除传递依赖）。

**数据库的备份和还原**

命令行

- 语法
  - 备份：mysqldump -u用户名 -p密码 数据库名称 > 保存的路径
  - 还原
    - 登录数据库
    - 创建数据库
    - 使用数据库
    - 执行文件：source 文件路径

图形化工具

### 2.6 多表查询

查询语法

```SQL
select 
	列名列表
from
	表名列表
where...
```

案例

```SQL
# 创建部门表
CREATE TABLE dept(
id INT PRIMARY KEY AUTO_INCREMENT,
NAME VARCHAR(20)
);
INSERT INTO dept (NAME) VALUES ('开发部'),('市场部'),('财务部');
# 创建员工表
CREATE TABLE emp (
id INT PRIMARY KEY AUTO_INCREMENT,
NAME VARCHAR(10),
gender CHAR(1), -- 性别
salary DOUBLE, -- 工资
join_date DATE, -- 入职日期
dept_id INT,
FOREIGN KEY (dept_id) REFERENCES dept(id) -- 外键，关联部门表(部门表的主键)
);
INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('孙悟空','男',7200,'2013-02-24',1);
INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('猪八戒','男',3600,'2010-12-02',2);
INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('唐僧','男',9000,'2008-08-08',2);
INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('白骨精','女',5000,'2015-10-07',3);
INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('蜘蛛精','女',4500,'2011-03-14',1);
```

笛卡尔积

- 有两个集合A，B。取这两个集合的所有组成情况。
- 要完成多表查询，需要消除无用的数据。

**多表查询的分类**

内连接查询

- 隐式内连接：使用where条件消除无用数据。

  - ```SQL
    SELECT
    	t1.name,
    	t1.gender,
    	t2.name
    FROM
    	emp t1,
    	dept t2
    WHERE
    	t1.`dept_id` = t2.`id`;
    ```

- 显式内连接

  - 语法：select 字段列表 from 表名1 [inner] join 表名2 on 条件;

  - ```SQL
    SELECT * FROM emp INNER JOIN dept ON emp.`dept_id` = dept.`id`;
    SELECT * FROM emp JOIN dept ON emp.`dept_id` = dept.`id`;
    ```

- 内连接查询思维逻辑

  - 从哪些表中查询数据
  - 条件是什么
  - 查询哪些字段

外连接查询

- 左外连接

  - 语法：select 字段列表 from 表1 left [outer] join 表2 on 条件;

  - 查询的是左表所有数据以及其交集部分。

  - ```SQL
    SELECT t1.*,t2.`name` FROM emp t1 LEFT JOIN dept t2 ON t1.`dept_id` = t2.`id`;
    ```

- 右外连接

  - 语法：select 字段列表 from 表1 right [outer] join 表2 on 条件;

  - 查询的是右表所有数据以及其交集部分。

  - ```SQL
    SELECT t1.*,t2.`name` FROM emp t1 RIGHT JOIN dept t2 ON t1.`dept_id` = t2.`id`;
    ```

子查询

- 概念：查询中嵌套查询，称嵌套查询为子查询。

- ```SQL
  -- 查询工资最高的员工信息
  -- 查询最高的工资是多少 9000
  SELECT MAX(salary) FROM emp;
  -- 查询员工信息，并且工资等于9000的
  SELECT * FROM emp WHERE emp.`salary` = 9000;
  -- 一条SQL就完成这个操作。子查询
  SELECT * FROM emp WHERE emp.`salary` = (SELECT MAX(salary) FROM emp);
  ```

- 子查询不同情况

  - 子查询的结果是单行单列的

    - 子查询可以作为条件，使用运算符去判断。运算符：>、>=、<、<=、=

    - ```SQL
      SELECT * FROM emp WHERE emp.salary < (SELECT AVG(salary) FROM emp);
      ```

  - 子查询的结果是多行单列的

    - 子查询可以作为条件，使用运算符in来判断

    - ```SQL
      -- 查询‘财务部’和‘市场部’所有的员工信息
      SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部'; 
      SELECT * FROM emp WHERE dept_id = 3 OR dept_id = 2;
      -- 子查询
      SELECT * FROM emp WHERE dept_id IN (SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部');
      ```

  - 子查询的结果是多行多列的

    - 子查询可以作为一张虚拟表

    - ```SQL
      -- 查询员工入职日期是2011-11-11日之后的员工信息和部门信息
      -- 子查询
      SELECT * FROM dept t1,(SELECT * FROM emp WHERE emp.`join_date` > '2011-11-11') t2 WHERE t1.id = t2.dept_id;
      -- 普通内连接
      SELECT * FROM emp t1,dept t2 WHERE t1.`dept_id` = t2.`id` AND t1.`join_date` > '2011-11-11';
      ```

多表的综合练习

```SQL
-- 部门表
CREATE TABLE dept (
  id INT PRIMARY KEY PRIMARY KEY, -- 部门id
  dname VARCHAR(50), -- 部门名称
  loc VARCHAR(50) -- 部门所在地
);

-- 添加4个部门
INSERT INTO dept(id,dname,loc) VALUES 
(10,'教研部','北京'),
(20,'学工部','上海'),
(30,'销售部','广州'),
(40,'财务部','深圳');



-- 职务表，职务名称，职务描述
CREATE TABLE job (
  id INT PRIMARY KEY,
  jname VARCHAR(20),
  description VARCHAR(50)
);

-- 添加4个职务
INSERT INTO job (id, jname, description) VALUES
(1, '董事长', '管理整个公司，接单'),
(2, '经理', '管理部门员工'),
(3, '销售员', '向客人推销产品'),
(4, '文员', '使用办公软件');



-- 员工表
CREATE TABLE emp (
  id INT PRIMARY KEY, -- 员工id
  ename VARCHAR(50), -- 员工姓名
  job_id INT, -- 职务id
  mgr INT , -- 上级领导
  joindate DATE, -- 入职日期
  salary DECIMAL(7,2), -- 工资
  bonus DECIMAL(7,2), -- 奖金
  dept_id INT, -- 所在部门编号
  CONSTRAINT emp_jobid_ref_job_id_fk FOREIGN KEY (job_id) REFERENCES job (id),
  CONSTRAINT emp_deptid_ref_dept_id_fk FOREIGN KEY (dept_id) REFERENCES dept (id)
);

-- 添加员工
INSERT INTO emp(id,ename,job_id,mgr,joindate,salary,bonus,dept_id) VALUES 
(1001,'孙悟空',4,1004,'2000-12-17','8000.00',NULL,20),
(1002,'卢俊义',3,1006,'2001-02-20','16000.00','3000.00',30),
(1003,'林冲',3,1006,'2001-02-22','12500.00','5000.00',30),
(1004,'唐僧',2,1009,'2001-04-02','29750.00',NULL,20),
(1005,'李逵',4,1006,'2001-09-28','12500.00','14000.00',30),
(1006,'宋江',2,1009,'2001-05-01','28500.00',NULL,30),
(1007,'刘备',2,1009,'2001-09-01','24500.00',NULL,10),
(1008,'猪八戒',4,1004,'2007-04-19','30000.00',NULL,20),
(1009,'罗贯中',1,NULL,'2001-11-17','50000.00',NULL,10),
(1010,'吴用',3,1006,'2001-09-08','15000.00','0.00',30),
(1011,'沙僧',4,1004,'2007-05-23','11000.00',NULL,20),
(1012,'李逵',4,1006,'2001-12-03','9500.00',NULL,30),
(1013,'小白龙',4,1004,'2001-12-03','30000.00',NULL,20),
(1014,'关羽',4,1007,'2002-01-23','13000.00',NULL,10);



-- 工资等级表
CREATE TABLE salarygrade (
  grade INT PRIMARY KEY,   -- 级别
  losalary INT,  -- 最低工资
  hisalary INT -- 最高工资
);

-- 添加5个工资等级
INSERT INTO salarygrade(grade,losalary,hisalary) VALUES 
(1,7000,12000),
(2,12010,14000),
(3,14010,20000),
(4,20010,30000),
(5,30010,99990);

-- 需求：

-- 1.查询所有员工信息。查询员工编号，员工姓名，工资，职务名称，职务描述
SELECT
	t1.`id`,
	t1.`ename`,
	t1.`salary`,
	t2.`jname`,
	t2.`description`
FROM
	emp t1,job t2
WHERE
	t1.`job_id` = t2.`id`;

-- 2.查询员工编号，员工姓名，工资，职务名称，职务描述，部门名称，部门位置
SELECT
	t1.`id`,
	t1.`ename`,
	t1.`salary`,
	t2.`jname`,
	t2.`description`,
	t3.`dname`,
	t3.`loc`
FROM
	emp t1,job t2,dept t3
WHERE
	t1.`job_id` = t2.`id` AND
	t1.`dept_id` = t3.`id`;
   
-- 3.查询员工姓名，工资，工资等级
SELECT
	t1.`ename`,
	t1.`salary`,
	t2.`grade`
FROM
	emp t1,salarygrade t2
WHERE
	t1.`salary` BETWEEN t2.`losalary` AND t2.`hisalary`;

-- 4.查询员工姓名，工资，职务名称，职务描述，部门名称，部门位置，工资等级
SELECT
	t1.`ename`,
	t1.`salary`,
	t2.`jname`,
	t2.`description`,
	t3.`dname`,
	t3.`loc`,
	t4.`grade`
FROM
	emp t1,job t2,dept t3,salarygrade t4
WHERE
	t1.`job_id` = t2.`id` AND
	t1.`dept_id` = t3.`id` AND
	t1.`salary` BETWEEN t4.`losalary` AND t4.`hisalary`;

-- 5.查询出部门编号、部门名称、部门位置、部门人数
SELECT
	t1.`id`,
	t1.`dname`,
	t1.`loc`,
	t2.total
FROM
	dept t1,
	(SELECT
		dept_id,COUNT(id) total
	FROM
		emp
	GROUP BY dept_id) t2
WHERE
	t1.`id` = t2.dept_id;
 
-- 6.查询所有员工的姓名及其直接上级的姓名,没有领导的员工也需要查询
SELECT
	t1.`ename`,
	t1.`mgr`,
	t2.`id`,
	t2.`ename`
FROM
	emp t1,emp t2
WHERE
	t1.`mgr` = t2.`id`;
	
SELECT
	t1.`ename`,
	t1.`mgr`,
	t2.`id`,
	t2.`ename`
FROM emp t1 
LEFT JOIN emp t2
ON t1.`mgr` = t2.`id`;
```

### 2.7 事务

**事务的基本介绍**

概念

- 如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。

操作

- 开启事务：start transaction;
- 回滚：rollback;
- 提交：commit;

MySQL数据库中事务默认自动提交

- 一条DML(增删改)语句会自动提交一次事务。
- 事务提交的两种方式
  - 自动提交：mysql就是自动提交的。
  - 手动提交：需要先开启事务，再提交。
  - Oracle数据库默认是手动提交事务的。
  - 修改事务的默认提交方式
    - 查看事务的默认提交方式：SELECT @@autocommit; 其中1代表自动提交，0代表手动提交。
    - 修改默认提交方式：SET @@autocommit = 0; 

**事务的四大特征**

原子性：是不可分割的最小操作单位，要么同时成功，要么同时失败。

持久性：当事务提交或回滚后，数据库会持久化的保存数据。

隔离性：多个事务之间。相互独立。

一致性：事务操作前后，数据总量不变。

**事务的隔离级别(了解)**

概念：多个事务之间隔离的，相互独立的。但是如果多个事务操作同一批数据，则会引发一些问题，设置不同的隔离级别就可以解决这些问题。

存在问题

- 脏读：一个事务，读取到另一个事务中没有提交的数据。
- 不可重复读(虚读)：在同一个事务中，两次读取到的数据不一样。
- 幻读：一个事务操作(DML)数据表中所有记录，另一个事务添加了一条数据，则第一个事务查询不到自己的修改。

隔离级别

- read uncommitted：读未提交。
  - 产生的问题：脏读、不可重复读、幻读。
- read committed：读已提交。(Oracle)
  - 产生的问题：不可重复读、幻读。
- repeatable read：可重复读。(MySQL默认)
  - 产生的问题：幻读。
- serializable：串行化。
  - 可以解决所有的问题。
- 注意：隔离级别从小到大安全性越来越高，但是效率越来越低。
- 数据库查询隔离级别：select @@tx_isolation;
- 数据库设置隔离级别：set global transaction isolation level 级别字符串;

## 3. JDBC基础

### 3.1 JDBC基本概念

**概念：**Java DataBase Connectivity，Java数据库连接，Java语言操作数据库。

**JDBC本质：**其实是官方(sun公司)定义的一套操作所有关系型数据库的规则，即接口。各个数据库厂商去实现这套接口，提供数据库驱动jar包。我们可以使用这套接口(JDBC)编程，真正执行的代码是驱动jar包中的实现类。

**快速入门**

步骤

- 导入驱动jar包：mysql-connector-java-5.1.37-bin.jar
  - 复制mysql-connector-java-5.1.37-bin.jar到项目的libs目录下。
  - 右键 --> Add As Library。
- 注册驱动
- 获取数据库连接对象Connection
- 定义sql
- 获取执行sql语句的对象Statement
- 执行sql，接收返回结果
- 处理结果
- 释放资源

案例代码

```Java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

public class JdbcDemo {
    public static void main(String[] args) throws Exception {
        // 注册驱动
        Class.forName("com.mysql.jdbc.Driver");
        // 获取数据库连接对象
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db3", "root", "root");
        // 定义sql语句
        String sql = "update account set balance = 500 where id = 1";
        // 获取执行sql的对象Statement
        Statement stmt = conn.createStatement();
        // 执行sql
        int count = stmt.executeUpdate(sql);
        // 处理结果
        System.out.println(count);
        // 释放资源
        stmt.close();
        conn.close();
    }
}
```

### 3.2 JDBC各个类详解

**DriverManager：驱动管理对象**

功能

- 注册驱动：告诉程序该使用哪一个数据库jar包
  - static void registerDriver(Driver driver)：注册与给定的驱动程序DriverManager。
  - 写代码使用：Class.forName("com.mysql.jdbc.Driver");
  - 通过查看源码发现：在com.mysql.jdbc.Driver类中存在静态代码块使用registerDriver(Driver driver)方法。
  - 注意：mysql5之后的驱动jar包可以省略注册驱动的步骤。
- 获取数据库连接
  - 方法：static Connection getConnection(String url, String user, String password)  
  - 参数
    - url：指定连接的路径
      - jdbc:mysql://ip地址(域名):端口号/数据库名称
      - 例子：jdbc:mysql://localhost:3306/db3
      - 细节：如果连接的是本机mysql服务器，并且mysql服务器端口是3306，则url可以简写为：jdbc:mysql:///数据库名称
    - user：用户名
    - password：密码

**Connection：数据库连接对象**

功能

- 获取执行sql的对象
  - Statement createStatement()  
  - PreparedStatement prepareStatement(String sql)  
- 管理事务
  - 开启事务：setAutoCommit(boolean autoCommit)：调用该方法设置参数为false，即开启事务。
  - 提交事务：void commit()  
  - 回滚事务：rollback() 

**Statement：执行sql的对象**

执行sql

- boolean execute(String sql)：可以执行任意的sql。
- int executeUpdate(String sql)：执行DML(insert、update、delete)语句，DDL(create、alter、drop)语句。
  - 返回值：影响的行数，可以通过这个影响的行数判断DML语句是否执行成功，返回值>0的则执行成功，反之，则失败。
- ResultSet executeQuery(String sql)：执行DQL(select)语句。

练习案例代码

```Java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class JdbcDemo01 {
    public static void main(String[] args) {
        Statement stmt = null;
        Connection conn = null;
        try {
            Class.forName("com.mysql.jdbc.Driver");
            String sql = "insert into account values(null,'王五',3000)";
            conn = DriverManager.getConnection("jdbc:mysql:///db3", "root", "root");
            stmt = conn.createStatement();
            int count = stmt.executeUpdate(sql);
            System.out.println(count);
            if (count > 0) {
                System.out.println("添加成功");
            } else {
                System.out.println("添加失败");
            }
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
            if (stmt != null) {
                try {
                    stmt.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

**ResultSet：结果集对象，封装查询结果**

常用方法

- next()：游标向下移动一行，判断是否是最后一行末尾(是否有数据)，如果无数据，则返回false，反之返回true。
- getXxx(参数)：获取数据。
  - Xxx：代表数据类型。
  - 参数
    - int：代表列的编号，从1开始。如getString(1)
    - String：代表列名称。如：getDouble("balance")
- 使用步骤
  - 游标向下移动一行
  - 判断是否有数据
  - 获取数据

相关代码

```Java
import java.sql.*;

public class JdbcDemo05 {
    public static void main(String[] args) {
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        try {
            Class.forName("com.mysql.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql:///db3", "root", "root");
            String sql = "select  * from account";
            stmt = conn.createStatement();
            rs = stmt.executeQuery(sql);
            while (rs.next()) {
                int id = rs.getInt(1);
                String name = rs.getString("name");
                double balance = rs.getDouble(3);
                System.out.println(id + "---" + name + "---" + balance);
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if (stmt != null) {
                try {
                    stmt.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

练习：定义一个方法，查询emp表的数据将其封装为对象，然后装载集合，返回。

员工类

```Java
import java.util.Date;

public class Emp {
    private int id;
    private String ename;
    private int job_id;
    private int mgr;
    private Date joindate;
    private double salary;
    private double bonus;
    private int dept_id;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getEname() {
        return ename;
    }

    public void setEname(String ename) {
        this.ename = ename;
    }

    public int getJob_id() {
        return job_id;
    }

    public void setJob_id(int job_id) {
        this.job_id = job_id;
    }

    public int getMgr() {
        return mgr;
    }

    public void setMgr(int mgr) {
        this.mgr = mgr;
    }

    public Date getJoindate() {
        return joindate;
    }

    public void setJoindate(Date joindate) {
        this.joindate = joindate;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public double getBonus() {
        return bonus;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    public int getDept_id() {
        return dept_id;
    }

    public void setDept_id(int dept_id) {
        this.dept_id = dept_id;
    }

    @Override
    public String toString() {
        return "Emp{" +
                "id=" + id +
                ", ename='" + ename + '\'' +
                ", job_id=" + job_id +
                ", mgr=" + mgr +
                ", joindate=" + joindate +
                ", salary=" + salary +
                ", bounds=" + bonus +
                ", dept_id=" + dept_id +
                '}';
    }
}
```

实现方法代码

```Java
import com.itahu.domain.Emp;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;

public class JdbcDemo06 {
    public static void main(String[] args) {
        List<Emp> list = new JdbcDemo06().findAll();
        System.out.println(list);
        System.out.println(list.size());
    }

    public List<Emp> findAll() {
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        List<Emp> list = null;
        try {
            Class.forName("com.mysql.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql:///db3", "root", "root");
            String sql = "select * from emp";
            stmt = conn.createStatement();
            rs = stmt.executeQuery(sql);
            Emp emp = null;
            list = new ArrayList<Emp>();
            while (rs.next()) {
                int id = rs.getInt(1);
                String ename = rs.getString("ename");
                int job_id = rs.getInt("job_id");
                int mgr = rs.getInt("mgr");
                Date joindate = rs.getDate("joindate");
                double salary = rs.getDouble("salary");
                double bonus = rs.getDouble("bonus");
                int dept_id = rs.getInt("dept_id");
                emp = new Emp();
                emp.setId(id);
                emp.setEname(ename);
                emp.setJob_id(job_id);
                emp.setMgr(mgr);
                emp.setJoindate(joindate);
                emp.setSalary(salary);
                emp.setBonus(bonus);
                emp.setDept_id(dept_id);
                list.add(emp);
            }
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if (stmt != null) {
                try {
                    stmt.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
        return list;
    }
}
```

**PreparedStatement：执行sql的对象**

SQL注入问题：在拼接sql时，有一些sql的特殊关键字参与字符串的拼接。会造成安全性问题。

- 输入用户名随便，输入密码：a' or 'a' = 'a
- sql：select * from user where username = 'kjhfekjk' and password = 'a' or 'a' = 'a'

解决SQL注入问题：使用PreparedStatement对象来解决。

预编译的SQL：参数使用？作为占位符。

步骤

- 导入驱动jar包：mysql-connector-java-5.1.37-bin.jar
- 注册驱动
- 获取数据库连接对象Connection
- 定义sql
  - 注意：sql的参数使用？作为占位符。如：select * from user where username = ? and password = ?;
- 获取执行sql语句的对象PreparedStatement：Connection.prepareStatement(String sql);
- 给?赋值
  - 方法：setXxx(参数1, 参数2)
    - 参数1：?的位置编号，从1开始。
    - 参数2：?的值。
- 执行sql，接收返回结果，不需要传递sql语句
- 处理结果
- 释放资源

注意：后期都会使用PreparedStatement来完成增删改查的所有操作。

- 可以防止SQL注入
- 效率更高

**抽取JDBC工具类：JDBCUtils**

目的：简化书写

分析

- 注册驱动也抽取

- 抽取一个方法获取连接对象
  - 不想传递参数(麻烦)，还得保证工具类的通用性。
  - 解决：配置文件jdbc.properties。
- 抽取一个方法释放资源

工具类实现

```Java
import java.io.FileReader;
import java.io.IOException;
import java.net.URL;
import java.sql.*;
import java.util.Properties;

public class JDBCUtils {
    private static String url;
    private static String user;
    private static String password;
    private static String driver;

    static {
        try {
            Properties pro = new Properties();
            ClassLoader classLoader = JDBCUtils.class.getClassLoader();
            URL res = classLoader.getResource("jdbc.properties");
            String path = res.getPath();
            pro.load(new FileReader(path));
            url = pro.getProperty("url");
            user = pro.getProperty("user");
            password = pro.getProperty("password");
            driver = pro.getProperty("driver");
            Class.forName(driver);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(url,user,password);
    }

    public static void close(Statement stmt,Connection conn) {
        if (stmt != null) {
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn != null) {
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public static void close(ResultSet rs, Statement stmt, Connection conn) {
        if (rs != null) {
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (stmt != null) {
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn != null) {
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

}
```

练习：通过键盘录入用户名和密码，判断用户是否登录成功。

创建表

```SQL
CREATE TABLE USER(
	id INT PRIMARY KEY AUTO_INCREMENT,
	username VARCHAR(32),
	PASSWORD VARCHAR(32)
);

SELECT * FROM USER;

INSERT INTO USER VALUES(NULL,'zhangsan','123');
INSERT INTO USER VALUES(NULL,'lisi','234');
```

实现代码

```Java
import com.itahu.util.JDBCUtils;

import java.sql.*;
import java.util.Scanner;

public class JDBCDemo08 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入用户名：");
        String username = sc.nextLine();
        System.out.println("请输入密码：");
        String password = sc.nextLine();
        boolean flag = new JDBCDemo08().login(username, password);
        if (flag) {
            System.out.println("登录成功！");
        } else {
            System.out.println("用户名或密码错误！");
        }
    }

    public boolean login(String username, String password) {
        if (username == null || password == null) {
            return false;
        }
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        try {
            conn = JDBCUtils.getConnection();
            String sql = "select * from user where username = ? and password = ?";
            pstmt = conn.prepareStatement(sql);
            pstmt.setString(1,username);
            pstmt.setString(2,password);
            rs = pstmt.executeQuery();
            return rs.next();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.close(rs,pstmt,conn);
        }
        return false;
    }
}
```

**JDBC控制事务**

事务：一个包含多个步骤的业务操作，如果这个业务操作被事务管理，则这多个步骤要么同时成功，要么同时失败。

操作

- 开启事务
- 提交事务
- 回滚事务

使用Connection对象来管理事务

- 开启事务：setAutoCommit(boolean autoCommit)：调用该方法设置参数为false，即开启事务。

  - 在执行sql之前开启事务
- 提交事务：void commit()  

  - 当所有sql都执行完提交事务
- 回滚事务：rollback() 

  - 在catch中回滚事务

案例

```Java
import com.itahu.util.JDBCUtils;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class JDBCDemo09 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement pstmt1 = null;
        PreparedStatement pstmt2 = null;
        try {
            conn = JDBCUtils.getConnection();
            conn.setAutoCommit(false);

            String sql1 = "update account set balance = balance - ? where id = ?";
            String sql2 = "update account set balance = balance + ? where id = ?";
            pstmt1 = conn.prepareStatement(sql1);
            pstmt2 = conn.prepareStatement(sql2);
            pstmt1.setDouble(1,500);
            pstmt1.setInt(2,1);
            pstmt2.setDouble(1,500);
            pstmt2.setInt(2,2);

            pstmt1.executeUpdate();
            int i = 3 / 0;
            pstmt2.executeUpdate();

            conn.commit();
        } catch (SQLException e) {
            try {
                if (conn != null) {
                    conn.rollback();
                }
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
            e.printStackTrace();
        } finally {
            JDBCUtils.close(pstmt1,conn);
            JDBCUtils.close(pstmt2,null);
        }
    }
}
```

### 3.3 数据库连接池

**概念：**其实就是一个容器(集合)，存放数据库连接的容器。

当系统初始化好后，容器被创建，容器中会申请一些连接对象，当用户来访问数据库时，从容器中获取连接对象，用户访问完之后，会将连接对象归还给容器。

**好处**

1.节约资源

2.用户访问高效

**实现**

标准接口：DataSource，javax.sql包下的。

方法

- 获取连接：getConnection() 
- 归还连接：如果连接对象Connection是从连接池中获取的，那么调用Connection.close()方法，则不会再关闭连接了。而是归还连接

一般我们不去实现它，由数据库厂商来实现

- C3P0：数据库连接池技术
- Druid：数据库连接池技术，是由阿里巴巴提供的

**C3P0：数据库连接池技术**

步骤

- 导入jar包(两个)：c3p0-0.9.5.2.jar，mchange-commons-java-0.2.12.jar
  - 不要忘记导入数据库的驱动jar包
- 定义配置文件
  - 名称：c3p0.properties 或 c3p0-config.xml
  - 路径：直接将文件放在src目录下即可
- 创建核心对象，数据库连接池对象：ComboPooledDataSource
- 获取连接：getConnection

配置文件c3p0-config.xml

```XML
<c3p0-config>
  <!-- 使用默认的配置读取连接池对象 -->
  <default-config>
   <!--  连接参数 -->
    <property name="driverClass">com.mysql.jdbc.Driver</property>
    <property name="jdbcUrl">jdbc:mysql://localhost:3306/db4</property>
    <property name="user">root</property>
    <property name="password">root</property>
    
    <!-- 连接池参数 -->
    <!-- 初始化申请的连接数量 -->
    <property name="initialPoolSize">5</property>
    <!-- 最大的连接数量 -->
    <property name="maxPoolSize">10</property>
    <!-- 超时时间 -->
    <property name="checkoutTimeout">3000</property>
  </default-config>

  <named-config name="otherc3p0"> 
    <!--  连接参数 -->
    <property name="driverClass">com.mysql.jdbc.Driver</property>
    <property name="jdbcUrl">jdbc:mysql://localhost:3306/db3</property>
    <property name="user">root</property>
    <property name="password">root</property>
    
    <!-- 连接池参数 -->
    <property name="initialPoolSize">5</property>
    <property name="maxPoolSize">8</property>
    <property name="checkoutTimeout">1000</property>
  </named-config>
</c3p0-config>
```

使用案例

```Java
import com.mchange.v2.c3p0.ComboPooledDataSource;

import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.SQLException;

public class C3P0Demo {
    public static void main(String[] args) throws SQLException {
        // 获取DataSource，使用默认配置
        DataSource ds = new ComboPooledDataSource();

        for (int i = 1; i <= 11; i++) {
            Connection conn = ds.getConnection();
            System.out.println(i + ":" + conn);
            if (i == 5) {
                conn.close();
            }
        }

        //testNameConfig();
    }

    public static void testNameConfig() throws SQLException {
        // 获取DataSource，使用指定名称配置
        DataSource ds = new ComboPooledDataSource("otherc3p0");

        for (int i = 1; i <= 10; i++) {
            Connection conn = ds.getConnection();
            System.out.println(i + ":" + conn);

        }
    }
}
```

**Druid：数据库连接池技术，由阿里巴巴提供**

步骤

- 导入jar包：druid-1.0.9.jar
- 定义配置文件
  - 是properties形式的
  - 可以叫任意名称，可以放在任意目录下
- 加载配置文件。Properties
- 获取数据库连接池对象：通过工厂来获取，DruidDataSourceFactory
- 获取连接：getConnection

配置文件druid.properties

```Properties
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/db3
username=root
password=root
initialSize=5
maxActive=10
maxWait=3000
```

使用案例

```Java
import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.sql.DataSource;
import java.io.InputStream;
import java.sql.Connection;
import java.util.Properties;

public class DruidDemo {
    public static void main(String[] args) throws Exception {
        Properties pro = new Properties();
        InputStream is = DruidDemo.class.getClassLoader().getResourceAsStream("druid.properties");
        pro.load(is);
        DataSource ds = DruidDataSourceFactory.createDataSource(pro);
        Connection conn = ds.getConnection();
        System.out.println(conn);
    }
}
```

**定义Druid连接池工具类**

定义一个类JDBCUtils

提供静态代码块加载配置文件，初始化连接池对象

提供方法

- 获取连接方法：通过数据库连接池获取连接
- 释放资源
- 获取连接池的方法

工具类实现

```Java
import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.sql.DataSource;
import java.io.IOException;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

public class JDBCUtils {
    private static DataSource ds;

    static {
        try {
            Properties pro = new Properties();
            pro.load(JDBCUtils.class.getClassLoader().getResourceAsStream("druid.properties"));
            ds = DruidDataSourceFactory.createDataSource(pro);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }

    public static void close(Statement stmt, Connection conn) {
        close(null,stmt,conn);
    }

    public static void close(ResultSet rs, Statement stmt, Connection conn) {
        if (rs != null) {
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (stmt != null) {
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn != null) {
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public static DataSource getDataSource() {
        return ds;
    }
}
```

练习案例

```Java
import com.itahu.datasource.utils.JDBCUtils;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class DruidDemo01 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement pstmt = null;
        try {
            conn = JDBCUtils.getConnection();
            String sql = "insert into account values(null,?,?)";
            pstmt = conn.prepareStatement(sql);
            pstmt.setString(1,"王五");
            pstmt.setDouble(2,3000);
            int count = pstmt.executeUpdate();
            System.out.println(count);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.close(pstmt,conn);
        }
    }
}
```

### 3.4 JDBCTemplate基础

**String JDBC**

Spring框架对JDBC的简单封装。提供了一个JDBCTemplate对象简化JDBC的开发。

步骤

- 导入jar包
- 创建JdbcTemplate对象。依赖于数据源DataSource
  - JdbcTemplate template = new JdbcTemplate(ds);
- 调用JdbcTemplate的方法来完成CRUD的操作
  - update()：执行DML语句。增、删、改语句。
  - queryForMap()：查询结果将结果集封装为map集合，将列名作为key，将值作为value，将这条记录封装为一个map集合。
    - 注意：这个方法查询的结果集长度只能是1。
  - queryForList()：查询结果将结果集封装为List集合。
    - 将每一条记录封装为一个Map集合，再将Map集合装载到List集合中。
  - query()：查询结果，将结果封装为JavaBean对象。
    - query的参数：RowMapper。
    - 一般我们使用BeanPropertyRowMapper实现类。可以完成数据到JavaBean的自动封装。
    - new BeanPropertyRowMapper<类型>(类型.class)
  - queryForObject()：查询结果，将结果封装为对象。
    - 一般用于聚合函数的查询。

基本入门程序

```Java
import com.itahu.datasource.utils.JDBCUtils;
import org.springframework.jdbc.core.JdbcTemplate;

public class JdbcTemplateDemo {
    public static void main(String[] args) {
        JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
        String sql = "update account set balance = 5000 where id = ?";
        int count = template.update(sql, 4);
        System.out.println(count);
    }
}
```

练习需求

1. 修改1号数据的salary为10000
2. 添加一条记录
3. 删除刚才添加的记录
4. 查询id为1的记录，将其封装为Map集合
5. 查询所有记录，将其封装为List集合
6. 查询所有记录，将其封装为Emp对象的List集合
7. 查询总记录数

实现代码

```Java
import com.itahu.datasource.domain.Emp;
import com.itahu.datasource.utils.JDBCUtils;
import org.junit.Test;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import java.util.List;
import java.util.Map;

public class JdbcTemplateDemo01 {
    private JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
    @Test
    public void  test1() {
        String sql = "update emp set salary = 10000 where id = 1001";
        int count = template.update(sql);
        System.out.println(count);
    }

    @Test
    public void  test2() {
        String sql = "insert into emp(id,ename,dept_id) values(?,?,?)";
        int count = template.update(sql,1015,"郭靖",10);
        System.out.println(count);
    }

    @Test
    public void  test3() {
        String sql = "delete from emp where id = ?";
        int count = template.update(sql,1015);
        System.out.println(count);
    }

    @Test
    public void  test4() {
        String sql = "select * from emp where id = ?";
        Map<String, Object> map = template.queryForMap(sql, 1001);
        System.out.println(map);
    }

    @Test
    public void  test5() {
        String sql = "select * from emp";
        List<Map<String, Object>> list = template.queryForList(sql);
        for (Map<String, Object> stringObjectMap : list) {
            System.out.println(stringObjectMap);
        }
    }

    @Test
    public void  test6() {
        String sql = "select * from emp";
        List<Emp> list = template.query(sql, new BeanPropertyRowMapper<Emp>(Emp.class));
        for (Emp emp : list) {
            System.out.println(emp);
        }
    }

    @Test
    public void  test7() {
        String sql = "select count(id) from emp";
        Long total = template.queryForObject(sql, Long.class);
        System.out.println(total);
    }
}
```

## 4. HTML

### 4.1 Web概念概述

**JavaWeb：**使用Java语言开发基于互联网的项目。

**软件架构**

C/S：Client/Server 客户端/服务器端

- 在用户本地有一个客户端程序，在远程有一个服务器程序
- 如：QQ，迅雷...
- 优点
  - 用户体验好
- 缺点
  - 开发、安装、部署、维护麻烦

B/S：Browser/Server 浏览器/服务器端

- 只需要一个浏览器，用户通过不同的网址(URL)，客户访问不同的服务器端程序
- 优点
  - 开发、安装、部署、维护简单
- 缺点
  - 如果应用过大，用户的体验可能会受到影响
  - 对硬件要求过高

**B/S架构详解**

资源分类

- 静态资源
  - 使用静态网页开发技术发布的资源。
  - 特点
    - 所有用户访问，得到的结果是一样的。
    - 如：文本，图片，音频，视频，HTML，CSS，JavaScript。
    - 如果用户请求的是静态资源，那么服务器会直接将静态资源发送给浏览器。浏览器中内置了静态资源的解析引擎，可以展示静态资源。
- 动态资源
  - 使用动态网页技术发布的资源。
  - 特点
    - 所有用户访问，得到的结果可能不一样。
    - 如：jsp/servlet，php，asp...。
    - 如果用户请求的是动态资源，那么服务器会执行动态资源，转换为静态资源，再发送给浏览器。
- 我们要学习动态资源，必须先学习静态资源
- 静态资源
  - HTML：用于搭建基础网页，展示页面的内容
  - CSS：用于美化页面，布局页面
  - JavaScript：控制页面的元素，让页面有一些动态的效果

### 4.2 HTML标签

**概念：**Hyper Text Markup Language，超文本标记语言。是最基础的网页开发语言。

超文本

- 超文本是用超链接的方法，将各种不同空间的文字信息组织在一起的网状文本。

标记语言

- 由标签构成的语言。<标签名称> 如：html，xml
- 标记语言不是编程语言

**快速入门**

语法

- html文档后缀名为 .html 或者 .htm
- 标签分类
  - 围堵标签：有开始标签和结束标签。如` <html></html>`
  - 自闭和标签：开始标签和结束标签在一起。如`<br/>`
- 标签可以嵌套
  - 需要正确嵌套，不能你中有我，我中有你
  - 错误：`<a><b></a></b>`
  - 正确：`<a><b></b></a>`
- 在开始标签中可以定义属性。属性是由键值对构成，值需要用引号(单双都可)引起来
- html的标签不区分大小写，建议使用小写

入门案例

```HTML
<html>
	<head>
		<title>title</title>
	</head>
	<body>
		<font color='red'>Hello World</font><br/>
		<font color='green'>Hello World</font>
	</body>
</html>
```

**标签学习**

文件标签：构成html最基本的标签

- html：html文档的根标签
- head：头标签。用于指定html文档的一些属性，用于引入外部的资源
- title：标题标签
- body：体标签
- \<!DOCTYPE html>：html5中定义该文档是html文档

文本标签：和文本有关的标签

- 注释：`<!-- 注释内容 -->`

- `<h1> to <h6>`：标题标签，h1~h6字体大小逐渐递减
- `<p>`：段落标签
- `<br>`：换行标签
- `<hr>`：展示一条水平线
  - 属性
    - color：颜色
    - width：宽度
    - size：高度
    - align：对齐方式
      - center：居中
      - left：左对齐
      - right：右对齐
- `<b>`：字体加粗
- `<i>`：字体斜体
- `<font>`：字体标签
- `<center>`：文本居中
  - 属性
    - color：颜色
    - size：大小
    - face：字体
- 属性定义
  - color
    - 英文单词：red，green，blue
    - rgb(值1, 值2, 值3)：值的范围：0~255。如：rgb(0,0,255)
    - #值1值2值3：值的范围在00~FF之间
  - width
    - 数值：width='20'，数值的单位，默认是px(像素)
    - 数值%：占比相对于父元素的比例

图片标签

- img：展示图片
  - 属性
    - src：指定图片的位置
    - 相对路径
      - ./：代表当前目录
      - ../：代表上一级目录

列表标签

- 有序列表
  - ol
  - li
- 无序列表
  - ul
  - li

链接标签

- a：定义一个超链接
  - 属性
    - href：指定访问资源的URL(统一资源定位符)
    - target：指定打开资源的方式
      - _self：默认值，在当前页面打开
      - _blank：在空白页面打开

div和span

- div：每一个div占满一整行。块级标签
- span：文本信息在一行展示，行内标签，内联标签

语义化标签：html5中为了提高程序的可读性，提供了一些标签

- `<header>`
- `<footer>`

表格标签

- table：定义表格
  - width：宽度
  - border：边框
  - cellpadding：定义内容与单元格的距离
  - cellspacing：定义单元格之间的距离，如果指定为0，则单元格之间的线会合为一条
  - bgcolor：背景色
  - align：对齐方式
- tr：定义行
  - bgcolor：背景色
  - align：对齐方式
- td：定义单元格
  - colspan：合并列
  - rowspan：合并行
- th：定义表头单元格
- caption：表格标题
- thead：表示表格的头部分
- tbody：表示表格的体部分
- tfoot：表示表格的脚部分

**表单标签**

概念：用于采集用户输入的数据的。用于和服务器进行交互。

使用的标签：form

form：用于定义表单的。可以定义一个范围，范围代表采集用户数据的范围

form的属性

- action：指定提交数据的URL
- method：指定提交方式
  - 分类：一共7种，2种比较常用
    - get
      - 请求参数会在地址栏中显示，会封装到请求行中(HTTP协议后讲解)
      - 请求参数大小是有限制的
      - 不太安全
    - post
      - 请求参数不会在地址栏中显示，会封装在请求体中(HTTP协议后讲解)
      - 请求参数的大小没有限制
      - 较为安全
- 表单项中的数据要想被提交，必须指定其name属性

表单项标签

- input：可以通过type属性值，改变元素展示的样式
  - type属性
    - text：文本输入框，默认值
      - placeholder：指定输入框的提示信息，当输入框的内容发生变化，会自动清空提示信息
    - password：密码输入框
    - radio：单选框
      - 注意：要想让多个单选框实现单选的效果，则多个单选框的name属性值必须一样
      - 一般会给每一个单选框提供value属性，指定其被选中后提交的值
      - checked属性，可以指定默认值
    - checkbox：复选框
      - 一般会给每一个单选框提供value属性，指定其被选中后提交的值
      - checked属性，可以指定默认值
    - file：文件选择框
    - hidden：隐藏域，用于提交一些信息
    - 按钮
      - submit：提交按钮，可以提交表单
      - button：普通按钮
      - image：图片提交按钮
        - src属性指定图片的路径
  - label：指定输入项的文字描述信息
    - label的for属性一般会和input的id属性值对应。如果对应了，则点击label区域，会让input输入框获取焦点
- select：下拉列表
  - 子元素：option，指定列表项
- textarea：文本域
  - cols：指定列数，每一行有多少个字符
  - rows：默认多少行

基础表单案例

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>注册页面</title>
</head>
<body>
<form action="#" method="post">
    <table border="1" align="center" width="500">
        <tr>
            <td><label for="username">用户名</label></td>
            <td><input type="text" name="username" id="username"></td>
        </tr>
        <tr>
            <td><label for="password">密码</label></td>
            <td><input type="password" name="password" id="password"></td>
        </tr>
        <tr>
            <td><label for="email">Email</label></td>
            <td><input type="email" name="email" id="email"></td>
        </tr>
        <tr>
            <td><label for="name">姓名</label></td>
            <td><input type="text" name="name" id="name"></td>
        </tr>
        <tr>
            <td><label for="tel">手机号</label></td>
            <td><input type="text" name="tel" id="tel"></td>
        </tr>
        <tr>
            <td><label>性别</label></td>
            <td>
                <input type="radio" name="gender" value="male"> 男
                <input type="radio" name="gender" value="female"> 女
            </td>
        </tr>
        <tr>
            <td><label for="birthday">出生日期</label></td>
            <td><input type="date" name="birthday" id="birthday"></td>
        </tr>
        <tr>
            <td><label for="checkcode">验证码</label></td>
            <td>
                <input type="text" name="checkcode" id="checkcode">
                <img src="img/verify_code.jpg">
            </td>
        </tr>
        <tr>
            <td colspan="2" align="center">
                <input type="submit" value="注册">
            </td>
        </tr>
    </table>
</form>
</body>
</html>
```

## 5. CSS

### 5.1 CSS概述

**概念：**Cascading Style Sheets，层叠样式表。

层叠：多个样式可以作用在同一个html的元素上，同时生效。

**好处**

- 功能强大
- 将内容展示和样式控制分离
  - 降低耦合度，解耦
  - 让分工协作更容易
  - 提高开发效率

### 5.2 CSS的基础使用

**CSS的使用：**CSS与HTML结合方式。

1.内联样式

- 在标签内使用style属性指定CSS代码
- 如：`<div style="color: red;">Hello CSS</div>`

2.内部样式

- 在head标签内，定义style标签，style标签的标签体内容就是CSS代码

- ```HTML
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <style>
          div{
              color:blue;
          }
      </style>
  </head>
  <body>
  <div>Hello CSS</div>
  </body>
  </html>
  ```

3.外部样式

- 定义css资源文件
- 在head标签内，定义link标签，引入外部的资源文件
- 如：`<link rel="stylesheet" href="css/a.css">`

注意

- 1，2，3种方式，css作用范围越来越大

- 1方式不常用，后期常用2，3

- 第3种格式可以写为

- ```HTML
  <style>
      @import "css/a.css";
  </style>
  ```

**CSS语法**

格式

```CSS
选择器 {
    属性名1:属性值1;
    属性名2:属性值2;
    ...
}
```

选择器：筛选具有相似特征的元素。

注意：每一对属性需要使用;隔开，最后一对属性可以不加;。

**选择器：**筛选具有相似特征的元素

分类

- 基础选择器

  - id选择器：选择具体的id属性值的元素，建议在一个html页面中id值唯一

    - 语法：#id属性值{}

  - 元素选择器：选择具有相同标签名称的元素

    - 语法：标签名称{}
    - 注意：id选择器优先级高于元素选择器

  - 类选择器：选择具有相同的class属性值的元素

    - 语法：.class属性值{}
    - 注意：类选择器优先级高于元素选择器

  - ```HTML
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>基础选择器</title>
        <style>
            #div1{
                color: red;
            }
    
            div{
                color: green;
            }
    
            .cls1{
                color: blue;
            }
        </style>
    </head>
    <body>
    <div id="div1">传智播客</div>
    <div class="cls1">黑马程序员</div>
    <p class="cls1">传智学院</p>
    </body>
    </html>
    ```

- 扩展选择器

  - 选择所有元素

    - 语法：*{}

  - 并集选择器

    - 选择器1,选择器2{}

  - 子选择器：筛选选择器1元素下的选择器2元素

    - 语法：选择器1 选择器2{}

  - 父选择器：筛选选择器2的父元素选择器1

    - 语法：选择器1 > 选择器2{}

  - 属性选择器：选择元素名称，属性名=属性值的元素

    - 语法：元素名称[属性名="属性值"]{}

  - 伪类选择器：选择一些元素具有的状态

    - 语法：元素:状态{}
    - 如：`<a>`
      - 状态
        - link：初始化的状态
        - visited：被访问的状态
        - active：正在访问的状态
        - hover：鼠标悬浮的状态

  - ```HTML
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>扩展选择器</title>
        <style>
            div p {
                color: red;
            }
    
            div > p {
                border: 1px solid;
            }
    
            input[type='text'] {
                border: 5px solid;
            }
    
            a:link {
                color: pink;
            }
    
            a:hover {
                color: green;
            }
    
            a:active {
                color: yellow;
            }
    
            a:visited {
                color: red;
            }
        </style>
    </head>
    <body>
    <div>
        <p>传智播客</p>
        <p>呵呵</p>
    </div>
    <p>黑马程序员</p>
    <div>aaa</div>
    
    <input type="text">
    <input type="password"><br>
    
    <a href="#">黑马程序员</a>
    </body>
    </html>
    ```

**属性**

1.字体、文本

- font-size：字体大小
- color：文本颜色
- text-align：对齐方式
- line-height：行高

2.背景

- background：背景，复合属性，可设置图片

3.边框

- border：设置边框，复合属性

4.尺寸

- width：宽度
- height：高度

5.盒子模型：控制布局

- margin：外边距
- padding：内边距
  - 默认情况下内边距会影响整个盒子的大小
  - box-sizing: border-box; 设置盒子属性，让width和height就是最终盒子的大小
- float：浮动
  - left
  - right

注册页面CSS版案例

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>注册页面</title>
    <style>
        * {
            margin: 0px;
            padding: 0px;
            box-sizing: border-box;
        }

        body {
            background: url("img/register_bg.png") no-repeat center;
        }

        .rg_layout {
            width: 900px;
            height: 500px;
            border: 8px solid #EEEEEE;
            background-color: white;
            margin: auto;
            margin-top: 15px;
        }

        .rg_left {
            /*border: 1px solid red;*/
            float: left;
            margin: 15px;
        }

        .rg_left > p:first-child {
            color: #FFD026;
            font-size: 20px;
        }

        .rg_left > p:last-child {
            color: #A6A6A6;
            font-size: 20px;
        }

        .rg_center {
            /*border: 1px solid red;*/
            float: left;
            width: 450px;
            margin-left: 30px;
            margin-top: 15px;
        }

        .rg_right {
            /*border: 1px solid red;*/
            float: right;
            margin: 15px;
        }

        .rg_right > p:first-child {
            font-size: 15px;
        }

        .rg_right p a {
            color: pink;
        }

        .td_left {
            width: 100px;
            text-align: right;
            height: 45px;
        }

        .td_right {
            padding-left: 50px;
        }

        #username, #password, #email, #name, #tel, #birthday, #checkcode {
            width: 251px;
            height: 32px;
            border: 1px solid #A6A6A6;
            border-radius: 5px;
            padding-left: 10px;
        }

        #checkcode {
            width: 110px;
        }

        #img_check {
            height: 32px;
            vertical-align: middle;
        }

        #btn_sub {
            width: 120px;
            height: 40px;
            background-color: #FFD026;
            border: 1px solid #FFD026;
        }
    </style>
</head>
<body>
<div class="rg_layout">
    <div class="rg_left">
        <p>新用户注册</p>
        <p>USER REGISTER</p>
    </div>

    <div class="rg_center">
        <div class="rg_form">
            <form action="#" method="post">
                <table>
                    <tr>
                        <td class="td_left"><label for="username">用户名</label></td>
                        <td class="td_right"><input type="text" name="username" id="username" placeholder="请输入用户名"></td>
                    </tr>
                    <tr>
                        <td class="td_left"><label for="password">密码</label></td>
                        <td class="td_right"><input type="password" name="password" id="password" placeholder="请输入密码">
                        </td>
                    </tr>
                    <tr>
                        <td class="td_left"><label for="email">Email</label></td>
                        <td class="td_right"><input type="email" name="email" id="email" placeholder="请输入邮箱"></td>
                    </tr>
                    <tr>
                        <td class="td_left"><label for="name">姓名</label></td>
                        <td class="td_right"><input type="text" name="name" id="name" placeholder="请输入姓名"></td>
                    </tr>
                    <tr>
                        <td class="td_left"><label for="tel">手机号</label></td>
                        <td class="td_right"><input type="text" name="tel" id="tel" placeholder="请输入手机号"></td>
                    </tr>
                    <tr>
                        <td class="td_left"><label>性别</label></td>
                        <td class="td_right">
                            <input type="radio" name="gender" value="male"> 男
                            <input type="radio" name="gender" value="female"> 女
                        </td>
                    </tr>
                    <tr>
                        <td class="td_left"><label for="birthday">出生日期</label></td>
                        <td class="td_right"><input type="date" name="birthday" id="birthday"></td>
                    </tr>
                    <tr>
                        <td class="td_left"><label for="checkcode">验证码</label></td>
                        <td class="td_right">
                            <input type="text" name="checkcode" id="checkcode" placeholder="请输入验证码">
                            <img id="img_check" src="img/verify_code.jpg">
                        </td>
                    </tr>
                    <tr>
                        <td colspan="2" align="center">
                            <input type="submit" id="btn_sub" value="注册">
                        </td>
                    </tr>
                </table>
            </form>
        </div>
    </div>

    <div class="rg_right">
        <p>已有账号?<a href="#">立即登录</a></p>
    </div>
</div>
</body>
</html>
```

## 6. JavaScript

### 6.1 JavaScript概述

**概念：**一门客户端脚本语言。

- 运行在客户端浏览器中的。每一个浏览器都有JavaScript的解析引擎
- 脚本语言：不需要编译，直接就可以被浏览器解析执行了

**功能：**可以来增强用户和html页面的交互过程，可以来控制html元素，让页面有一些动态的效果，增强用户的体验。

**JavaScript发展史**

1. 1992年，Nombase公司，开发出第一门客户端脚本语言，专门用于表单的校验。命名为 ： C--	，后来更名为：ScriptEase。
2. 1995年，Netscape(网景)公司，开发了一门客户端脚本语言：LiveScript。后来，请来SUN公司的专家，修改LiveScript，命名为JavaScript。
3. 1996年，微软抄袭JavaScript开发出JScript语言。
4. 1997年，ECMA(欧洲计算机制造商协会)，制定出客户端脚本语言的标准：ECMAScript，就是统一了所有客户端脚本语言的编码方式。

- JavaScript = ECMAScript + JavaScript自己特有的东西(BOM+DOM)

### 6.2 JavaScript基础语法

**ECMAScript：客户端脚本语言的标准**

1.基本语法

- 与html结合方式
  - 内部JS：定义`<script>`，标签体内容就是js代码
  - 外部JS：定义`<script>`，通过src属性引入外部js文件
  - 注意
    - `<script>`可以定义在html页面的任何地方。但是定义的位置会影响执行顺序。
    - `<script>`可以定义多个。

- 注释

  - 单行注释：//注释内容
  - 多行注释：/\*注释内容*/

- 数据类型

  1. 原始数据类型(基本数据类型)
     - number：数字。 整数/小数/NaN(not a number 一个不是数字的数字类型)
     - string：字符串。 字符串  "abc" "a" 'abc'
     - boolean: true和false
     - null：一个对象为空的占位符
     - undefined：未定义。如果一个变量没有给初始化值，则会被默认赋值为undefined
  2. 引用数据类型：对象

- 变量

  - 变量：一小块存储数据的内存空间

  - Java语言是强类型语言，而JavaScript是弱类型语言。

    - 强类型：在开辟变量存储空间时，定义了空间将来存储的数据的数据类型。只能存储固定类型的数据

     * 弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，可以存放任意类型的数据。

  - 语法：var 变量名 = 初始化值;

  - typeof运算符：获取变量的类型。
    			* 注：null运算后得到的是object

- 运算符

  1. 一元运算符：只有一个运算数的运算符

     - ++，-- ， +(正号)，-(负号)  
     - ++ --: 自增(自减)
     - ++(--) 在前，先自增(自减)，再运算
     - ++(--) 在后，先运算，再自增(自减)
     - +(-)：正负号
     - 注意：在JS中，如果运算数不是运算符所要求的类型，那么js引擎会自动的将运算数进行类型转换
     -  其他类型转number
       - string转number：按照字面值转换。如果字面值不是数字，则转为NaN（不是数字的数字）
       - boolean转number：true转为1，false转为0

  2. 算数运算符

     - `+ - * / % ...`

  3. 赋值运算符

     - `= += -+ ...`

  4. 比较运算符

     - \> < >= <= == ===(全等于)

       * 比较方式
         1. 类型相同：直接比较
            - 字符串：按照字典顺序比较。按位逐一比较，直到得出大小为止。
         2. 类型不同：先进行类型转换，再比较
            - ===：全等于。在比较之前，先判断类型，如果类型不一样，则直接返回false

  5. 逻辑运算符

     - && || !
     - 其他类型转boolean
       - number：0或NaN为假，其他为真
       - string：除了空字符串("")，其他都是true
       - null&undefined：都是false
       - 对象：所有对象都为true

  6. 三元运算符

     - ? : 表达式
     - 语法：表达式? 值1:值2;
       - 判断表达式的值，如果是true则取值1，如果是false则取值2；

- 流程控制语句

  - if...else...
  - switch
    - 在java中，switch语句可以接受的数据类型： byte int shor char,枚举(1.5)，String(1.7)
    - 在JS中,switch语句可以接受任意的原始数据类型
  - while
  - do...while
  - for

- JS特殊语法

  - 语句以;结尾，如果一行只有一条语句则 ;可以省略 (不建议)
  - 变量的定义使用var关键字，也可以不使用
    - 用： 定义的变量是局部变量
    - 不用：定义的变量是全局变量(不建议)

99乘法表案例

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>99乘法表</title>
    <style>
        td {
            border: 1px solid;
        }
    </style>
    <script>
        document.write("<table align='center'>");
        for (var i = 1; i <= 9; i++) {
            document.write("<tr>");
            for (var j = 1; j <= i; j++) {
                document.write("<td>");
                document.write(i + "*" + j + "=" + (i * j) + "&nbsp;&nbsp;&nbsp;");
                document.write("</td>");
            }
            document.write("</tr>");
        }
        document.write("</table>");
    </script>
</head>
<body>

</body>
</html>
```

2.基本对象

- Function：函数(方法)对象

  - 创建

    - var fun = new Function(形式参数列表, 方法体);

    - ```JavaScript
      function 方法名称(形式参数列表){
          方法体
      }
      ```

    - ```JavaScript
      var 方法名 = function(形式参数列表){
          方法体
      }
      ```

  - 方法

  - 属性

    - length：代表形参的个数

  - 特点

    - 方法定义时，形参的类型不用写，返回值类型也不用写
    - 方法是一个对象，如果定义相同名称的方法，会覆盖
    - 在JS中，方法的调用只与方法的名称有关，和参数列表无关
    - 在方法声明中有一个隐藏的内置对象（数组），arguments，封装所有的实际参数

  - 调用

    - 方法名称(实际参数列表);

- Array：数组对象

  - 创建
    - var arr = new Array(元素列表);
    - var arr = new Array(默认长度);
    - var arr = [元素列表];
  - 方法
    - join(参数)：将数组中的元素按照指定的分隔符拼接为字符串
    - push()：向数组的末尾添加一个或更多元素，并返回新的长度
  - 属性
    - length：数组的长度
  - 特点
    - JS中，数组元素的类型可变的
    - JS中，数组长度是可变的

- Boolean

- Date：日期对象

  - 创建
    - var date = new Date();
  - 方法
    - toLocaleString()：返回当前date对象对应的时间本地字符串格式
    - getTime()：获取毫秒值。返回当前如期对象描述的时间到1970年1月1日零点的毫秒值差

- Math：数学对象

  - 创建
    - 特点：Math对象不用创建，直接使用。Math.方法名();
  - 方法
    - random()：返回 0 ~ 1 之间的随机数。含0不含1
    - ceil(x)：对数进行上舍入
    - floor(x)：对数进行下舍入
    - round(x)：把数四舍五入为最接近的整数
  - 属性
    - PI

- Number

- String

- RegExp：正则表达式对象

  - 正则表达式：定义字符串的组成规则。

  - 单个字符：[]

    - 如：[a] [ab] [a-zA-Z0-9_]
    - 特殊符号代表特殊含义的单个字符
      - \d：单个数字字符 [0-9]
      - \w：单个单词字符[a-zA-Z0-9_]

  - 量词符号

    - ?：表示出现0次或1次

    - *：表示出现0次或多次
    - +：出现1次或多次
    - {m,n}：表示 m <= 数量 <= n
      - m如果缺省： {,n}：最多n次
      - n如果缺省：{m,}：最少m次

  - 开始结束符号

    - ^：开始
    - $：结束

  - 正则对象

    - 创建
      - var reg = new RegExp("正则表达式");
      - var reg = /正则表达式/;
    - 方法
      - test(参数)：验证指定的字符串是否符合正则定义的规范

- Global

  - 特点：全局对象，这个Global对象中封装的方法不需要对象就可以直接调用。方法名();
  - 方法
    - encodeURI()：url编码
    - decodeURI()：url解码
    - encodeURIComponent()：url编码，编码的字符更多
    - decodeURIComponent()：url解码
    - parseInt()：将字符串转为数字
      - 逐一判断每一个字符是否是数字，直到不是数字为止，将前边数字部分转为number
    - isNaN()：判断一个值是否是NaN
      - NaN六亲不认，连自己都不认。NaN参与的==比较全部问false
    - eval()：将JavaScript字符串，作为脚本代码来执行
  - URL编码
    - 如：传智播客 =  %E4%BC%A0%E6%99%BA%E6%92%AD%E5%AE%A2

### 6.3 BOM与DOM

**DOM简单学习：为了满足案例要求**

功能：控制html文档的内容。

代码：获取页面标签(元素)对象Element

- document.getElementById("id值")：通过元素的id获取元素对象

操作Element对象

- 修改属性值
  - 明确获取的对象是哪一个
  - 查看API文档，找其中有哪些属性可以设置
- 修改标签体内容
  - 属性：innerHTML
  - 获取元素对象
  - 使用innerHTML属性修改标签体内容

**事件简单学习**

功能：某些组件被执行了某些操作后，触发某些代码的执行。

- 造句：xxx被xxx，我就xxx
  - 我方水晶被摧毁后，我就责备队友
  - 敌方水晶被摧毁后，我就夸奖自己

如何绑定事件

- 直接在html标签上，指定事件的属性(操作)，属性值就是js代码
  - 事件：onclick --- 单击事件
- 通过js获取元素对象，指定事件属性，设置一个函数

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件绑定</title>
</head>
<body>
  <img id="light" src="img/off.gif" onclick="fun()">
  <img id="light2" src="img/off.gif">

  <script>
      function fun() {
          alert('我被点了');
          alert('我又被点了');
      }

      function fun2() {
          alert('咋老点我?');
      }

      var light2 = document.getElementById("light2");
      light2.onclick = fun2;
  </script>
</body>
</html>
```

练习案例：电灯开关

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>电灯开关</title>
</head>
<body>
  <img id="light" src="img/off.gif">

  <script>
      var light = document.getElementById("light");
      var flag = false;
      light.onclick = function () {
          if (flag) {
              light.src = "img/off.gif";
              flag = false;
          } else {
              light.src = "img/on.gif";
              flag = true;
          }
      }
  </script>
</body>
</html>
```

**BOM**

概念：Browser Object Model，浏览器对象模型。

- 将浏览器的各个组成部分封装成对象

组成

- Window：窗口对象
- Navigator：浏览器对象
- Screen：显示器屏幕对象
- History：历史记录对象
- Location：地址栏对象

Window：窗口对象

- 创建
- 方法
  - 与弹出框有关的方法
    - alert()：显示带有一段消息和一个确认按钮的警告框。
    - confirm()：显示带有一段消息以及确认按钮和取消按钮的对话框。
      - 如果用户点击确定按钮，则方法返回true。
      - 如果用户点击取消按钮，则方法返回false。
    - prompt()：显示可提示用户输入的对话框。
      - 返回值：获取用户输入的值。
  - 与打开关闭有关的方法
    - close()：关闭浏览器窗口。
      - 谁调用我 ，我关谁。
    - open()：打开一个新的浏览器窗口。
      - 返回新的Window对象。
  - 与定时器有关的方法
    - setTimeout()：在指定的毫秒数后调用函数或计算表达式。
      - 参数
        - js代码或者方法对象
        - 毫秒值
      - 返回值：唯一标识，用于取消定时器
    - clearTimeout()：取消由setTimeout()方法设置的timeout。
    - setInterval()：按照指定的周期（以毫秒计）来调用函数或计算表达式。
    - clearInterval()：取消由setInterval()设置的 timeout。
- 属性
  - 获取其他BOM对象
    - history
    - location
    - Navigator
    - Screen
  - 获取DOM对象
    - document
- 特点
  - Window对象不需要创建可以直接使用 window使用。window.方法名();
  - window引用可以省略。方法名();

练习案例：轮播图

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>轮播图</title>
</head>
<body>
  <img id="img" src="img/banner_1.jpg" width="100%">

  <script>
      var number = 1;
      function fun() {
          number++;
          if (number > 3) {
              number = 1;
          }
          var img = document.getElementById("img");
          img.src = "img/banner_"+ number + ".jpg";
      }

      setInterval(fun,3000);
  </script>
</body>
</html>
```

Location：地址栏对象

- 创建(获取)
  - window.location
  - location
- 方法
  - reload()：重新加载当前文档。刷新
- 属性
  - href：设置或返回完整的URL

练习案例：自动跳转首页

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自动跳转首页</title>
    <style>
        p {
            text-align: center;
        }

        span {
            color: red;
        }
    </style>
</head>
<body>
<p><span id="time">5</span>秒之后，自动跳转到首页...</p>

<script>
    var second = 5;
    var time = document.getElementById("time");
    function showTime() {
        second--;
        if (second <= 0) {
            location.href = "https://www.baidu.com";
        }
        time.innerHTML = second + "";
    }
    setInterval(showTime,1000);
</script>
</body>
</html>
```

History：历史记录对象

- 创建(获取)
  - window.history
  - history
- 方法
  - back()：加载 history 列表中的前一个 URL
  - forward()：加载 history 列表中的下一个 URL
  - go(参数)：加载 history 列表中的某个具体页面
- 属性
  - length：返回当前窗口历史列表中的URL数量

**DOM**

概念：Document Object Model，文档对象类型。

- 将标记语言文档的各个组成部分，封装为对象。可以使用这些对象，对标记语言文档进行CRUD的动态操作。

W3C DOM 标准被分为 3 个不同的部分

- 核心 DOM - 针对任何结构化文档的标准模型
  - Document：文档对象
  - Element：元素对象
  - Attribute：属性对象
  - Text：文本对象
  - Comment：注释对象
  - Node：节点对象，其他5个的父对象
- XML DOM - 针对 XML 文档的标准模型
- HTML DOM - 针对 HTML 文档的标准模型

核心DOM模型

- Document：文档对象
  - 创建(获取)：在html dom模型中可以使用window对象来获取
    - window.document
    - document
  - 方法
    - 获取Element对象
      - getElementById()：根据id属性值获取元素对象。id属性值一般唯一
      - getElementsByTagName()：根据元素名称获取元素对象们。返回值是一个数组
      - getElementsByClassName()：根据Class属性值获取元素对象们。返回值是一个数组
      - getElementsByName()：根据name属性值获取元素对象们。返回值是一个数组
    - 创建其他DOM对象
      - createAttribute(name)
      - createComment()
      - createElement()
      - createTextNode()
  - 属性
- Element：元素对象
  - 获取/创建：通过document来获取和创建
  - 方法
    - removeAttribute()：删除属性
    - setAttribute()：设置属性
- Node：节点对象，其他5个的父对象
  - 特点：所有dom对象都可以被认为是一个节点
  - 方法
    - CRUD dom树
      - appendChild()：向节点的子节点列表的结尾添加新的子节点
      - removeChild()：删除（并返回）当前节点的指定子节点
      - replaceChild()：用新节点替换一个子节点
  - 属性
    - parentNode：返回节点的父节点

练习案例：动态表格

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>动态表格</title>

    <style>
        table{
            border: 1px solid;
            margin: auto;
            width: 500px;
        }

        td,th{
            text-align: center;
            border: 1px solid;
        }
        div{
            text-align: center;
            margin: 50px;
        }
    </style>

</head>
<body>

<div>
    <input type="text" id="id" placeholder="请输入编号">
    <input type="text" id="name"  placeholder="请输入姓名">
    <input type="text" id="gender"  placeholder="请输入性别">
    <input type="button" value="添加" id="btn_add">

</div>


<table>
    <caption>学生信息表</caption>
    <tr>
        <th>编号</th>
        <th>姓名</th>
        <th>性别</th>
        <th>操作</th>
    </tr>

    <tr>
        <td>1</td>
        <td>令狐冲</td>
        <td>男</td>
        <td><a href="javascript:void(0)" onclick="delTr(this)">删除</a></td>
    </tr>

    <tr>
        <td>2</td>
        <td>任我行</td>
        <td>男</td>
        <td><a href="javascript:void(0)" onclick="delTr(this)">删除</a></td>
    </tr>

    <tr>
        <td>3</td>
        <td>岳不群</td>
        <td>?</td>
        <td><a href="javascript:void(0)" onclick="delTr(this)">删除</a></td>
    </tr>


</table>

<script>
    document.getElementById("btn_add").onclick = function () {
        var id = document.getElementById("id").value;
        var name = document.getElementById("name").value;
        var gender = document.getElementById("gender").value;

        var td_id = document.createElement("td");
        var text_id = document.createTextNode(id);
        td_id.appendChild(text_id);
        var td_name = document.createElement("td");
        var text_id = document.createTextNode(name);
        td_name.appendChild(text_id);
        var td_gender = document.createElement("td");
        var text_id = document.createTextNode(gender);
        td_gender.appendChild(text_id);
        var td_a = document.createElement("td");
        var ele_a = document.createElement("a");
        ele_a.setAttribute("href","javascript:void(0)")
        ele_a.setAttribute("onclick","delTr(this)")
        var text_a = document.createTextNode("删除");
        ele_a.appendChild(text_a);
        td_a.appendChild(ele_a);

        var tr = document.createElement("tr");
        tr.appendChild(td_id);
        tr.appendChild(td_name);
        tr.appendChild(td_gender);
        tr.appendChild(td_a);

        var table = document.getElementsByTagName("table")[0];
        table.appendChild(tr);
    }

    function delTr(obj) {
        var table = obj.parentNode.parentNode.parentNode;
        var tr = obj.parentNode.parentNode;
        table.removeChild(tr);
    }
</script>
</body>
</html>
```

HTML DOM

- 标签体的设置和获取：innerHTML
- 使用html元素对象的属性
- 控制元素样式
  - 使用元素的style属性来设置
    - div1.style.border = "1px solid red";
    - div1.style.width = "200px";
    - div1.style.fontSize = "20px";
  - 提前定义好类选择器的样式，通过元素的className属性来设置其class属性值

动态表格改进版

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>动态表格</title>

    <style>
        table {
            border: 1px solid;
            margin: auto;
            width: 500px;
        }

        td, th {
            text-align: center;
            border: 1px solid;
        }

        div {
            text-align: center;
            margin: 50px;
        }
    </style>

</head>
<body>

<div>
    <input type="text" id="id" placeholder="请输入编号">
    <input type="text" id="name" placeholder="请输入姓名">
    <input type="text" id="gender" placeholder="请输入性别">
    <input type="button" value="添加" id="btn_add">

</div>


<table>
    <caption>学生信息表</caption>
    <tr>
        <th>编号</th>
        <th>姓名</th>
        <th>性别</th>
        <th>操作</th>
    </tr>

    <tr>
        <td>1</td>
        <td>令狐冲</td>
        <td>男</td>
        <td><a href="javascript:void(0)" onclick="delTr(this)">删除</a></td>
    </tr>

    <tr>
        <td>2</td>
        <td>任我行</td>
        <td>男</td>
        <td><a href="javascript:void(0)" onclick="delTr(this)">删除</a></td>
    </tr>

    <tr>
        <td>3</td>
        <td>岳不群</td>
        <td>?</td>
        <td><a href="javascript:void(0)" onclick="delTr(this)">删除</a></td>
    </tr>


</table>

<script>
    document.getElementById("btn_add").onclick = function () {
        var id = document.getElementById("id").value;
        var name = document.getElementById("name").value;
        var gender = document.getElementById("gender").value;

        var table = document.getElementsByTagName("table")[0];
        table.innerHTML += "<tr>\n" +
            "        <td>" + id + "</td>\n" +
            "        <td>" + name + "</td>\n" +
            "        <td>" + gender + "</td>\n" +
            "        <td><a href=\"javascript:void(0)\" onclick=\"delTr(this)\">删除</a></td>\n" +
            "    </tr>"
    }

    function delTr(obj) {
        var table = obj.parentNode.parentNode.parentNode;
        var tr = obj.parentNode.parentNode;
        table.removeChild(tr);
    }
</script>
</body>
</html>
```

### 6.4 事件

**事件监听机制**

概念：某些组件被执行了某些操作后，触发某些代码的执行。

- 事件：某些操作。如： 单击，双击，键盘按下了，鼠标移动了
- 事件源：组件。如： 按钮 文本输入框...
- 监听器：代码。
- 注册监听：将事件，事件源，监听器结合在一起。 当事件源上发生了某个事件，则触发执行某个监听器代码。

常见的事件

- 点击事件
  - onclick：单击事件
  - ondblclick：双击事件
- 焦点事件
  - onblur：失去焦点
    - 一般用于表单验证
  - onfocus：元素获得焦点
- 加载事件
  - onload：一张页面或一幅图像完成加载
- 鼠标事件
  - onmousedown：鼠标按钮被按下
    - 定义方法时，定义一个形参，接受event对象
    - event对象的button属性可以获取鼠标按钮哪个键被点击了
  - onmouseup：鼠标按键被松开
  - onmousemove：鼠标被移动
  - onmouseover：鼠标移到某元素之上
  - onmouseout：鼠标从某元素移开
- 键盘事件
  - onkeydown：某个键盘按键被按下
  - onkeyup：某个键盘按键被松开
  - onkeypress：某个键盘按键被按下并松开
- 选择和改变
  - onchange：域的内容被改变
  - onselect：文本被选中
- 表单事件
  - onsubmit：确认按钮被点击
    - 可以阻止表单提交，方法返回false则表单被阻止提交
  - onreset：重置按钮被点击

练习案例：表格全选

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表格全选</title>
    <style>
        table{
            border: 1px solid;
            width: 500px;
            margin-left: 30%;
        }

        td,th{
            text-align: center;
            border: 1px solid;
        }
        div{
            margin-top: 10px;
            margin-left: 30%;
        }
        .out{
            background-color: white;
        }
        .over{
            background-color: pink;
        }
    </style>

    <script>
        window.onload = function () {
            document.getElementById("selectAll").onclick = function () {
                var cbs = document.getElementsByName("cb");
                for (let i = 0; i < cbs.length; i++) {
                    cbs[i].checked = true;
                }
            }

            document.getElementById("unSelectAll").onclick = function () {
                var cbs = document.getElementsByName("cb");
                for (let i = 0; i < cbs.length; i++) {
                    cbs[i].checked = false;
                }
            }

            document.getElementById("selectRev").onclick = function () {
                var cbs = document.getElementsByName("cb");
                for (let i = 0; i < cbs.length; i++) {
                    cbs[i].checked = !cbs[i].checked;
                }
            }

            document.getElementById("firstCb").onclick = function () {
                var cbs = document.getElementsByName("cb");
                for (let i = 0; i < cbs.length; i++) {
                    cbs[i].checked = this.checked;
                }
            }

            var trs = document.getElementsByTagName("tr");
            for (let i = 0; i < trs.length; i++) {
                trs[i].onmouseover = function () {
                    this.className = "over";
                }

                trs[i].onmouseout = function () {
                    this.className = "out"
                }
            }
        }
    </script>
</head>
<body>

<table>
    <caption>学生信息表</caption>
    <tr>
        <th><input type="checkbox" name="cb" id="firstCb"></th>
        <th>编号</th>
        <th>姓名</th>
        <th>性别</th>
        <th>操作</th>
    </tr>

    <tr>
        <td><input type="checkbox" name="cb"></td>
        <td>1</td>
        <td>令狐冲</td>
        <td>男</td>
        <td><a href="javascript:void(0);">删除</a></td>
    </tr>

    <tr>
        <td><input type="checkbox" name="cb"></td>
        <td>2</td>
        <td>任我行</td>
        <td>男</td>
        <td><a href="javascript:void(0);">删除</a></td>
    </tr>

    <tr>
        <td><input type="checkbox" name="cb"></td>
        <td>3</td>
        <td>岳不群</td>
        <td>?</td>
        <td><a href="javascript:void(0);">删除</a></td>
    </tr>

</table>
<div>
    <input type="button" id="selectAll" value="全选">
    <input type="button" id="unSelectAll" value="全不选">
    <input type="button" id="selectRev" value="反选">
</div>
</body>
</html>
```

练习案例：表单校验

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>注册页面</title>
<style>
    *{
        margin: 0px;
        padding: 0px;
        box-sizing: border-box;
    }
    body{
        background: url("img/register_bg.png") no-repeat center;
        padding-top: 25px;
    }

    .rg_layout{
        width: 900px;
        height: 500px;
        border: 8px solid #EEEEEE;
        background-color: white;
        /*让div水平居中*/
        margin: auto;
    }

    .rg_left{
        /*border: 1px solid red;*/
        float: left;
        margin: 15px;
    }
    .rg_left > p:first-child{
        color:#FFD026;
        font-size: 20px;
    }

    .rg_left > p:last-child{
        color:#A6A6A6;
        font-size: 20px;

    }


    .rg_center{
        float: left;
       /* border: 1px solid red;*/

    }

    .rg_right{
        /*border: 1px solid red;*/
        float: right;
        margin: 15px;
    }

    .rg_right > p:first-child{
        font-size: 15px;

    }
    .rg_right p a {
        color:pink;
    }

    .td_left{
        width: 100px;
        text-align: right;
        height: 45px;
    }
    .td_right{
        padding-left: 50px ;
    }

    #username,#password,#email,#name,#tel,#birthday,#checkcode{
        width: 251px;
        height: 32px;
        border: 1px solid #A6A6A6 ;
        /*设置边框圆角*/
        border-radius: 5px;
        padding-left: 10px;
    }
    #checkcode{
        width: 110px;
    }

    #img_check{
        height: 32px;
        vertical-align: middle;
    }

    #btn_sub{
        width: 150px;
        height: 40px;
        background-color: #FFD026;
        border: 1px solid #FFD026 ;
    }

    .error {
        color: red;
    }

    #td_sub {
        padding-left: 150px;
    }
</style>
<script>
    window.onload = function () {
        document.getElementById("form").onsubmit = function () {
            return checkUsername() && checkPassword();
        }

        document.getElementById("username").onblur = checkUsername;
        document.getElementById("password").onblur = checkPassword;
    }

    function checkUsername() {
        var username = document.getElementById("username").value;
        var reg_username = /^\w{6,12}$/;
        var flag = reg_username.test(username);
        var s_username = document.getElementById("s_username");
        if (flag) {
            s_username.innerHTML = "<img width='35px' height='25px' src='img/gou.png'>";
        } else {
            s_username.innerHTML = "用户名格式有误";
        }
        return flag;
    }

    function checkPassword() {
        var password = document.getElementById("password").value;
        var reg_password = /^\w{6,12}$/;
        var flag = reg_password.test(password);
        var s_password = document.getElementById("s_password");
        if (flag) {
            s_password.innerHTML = "<img width='35px' height='25px' src='img/gou.png'>";
        } else {
            s_password.innerHTML = "密码格式有误";
        }
        return flag;
    }
</script>

</head>
<body>

<div class="rg_layout">
    <div class="rg_left">
        <p>新用户注册</p>
        <p>USER REGISTER</p>

    </div>

    <div class="rg_center">
        <div class="rg_form">
            <!--定义表单 form-->
            <form action="#" id="form" method="get">
                <table>
                    <tr>
                        <td class="td_left"><label for="username">用户名</label></td>
                        <td class="td_right">
                            <input type="text" name="username" id="username" placeholder="请输入用户名">
                            <span id="s_username" class="error"></span>
                        </td>
                    </tr>

                    <tr>
                        <td class="td_left"><label for="password">密码</label></td>
                        <td class="td_right">
                            <input type="password" name="password" id="password" placeholder="请输入密码">
                            <span id="s_password" class="error"></span>
                        </td>
                    </tr>

                    <tr>
                        <td class="td_left"><label for="email">Email</label></td>
                        <td class="td_right"><input type="email" name="email" id="email" placeholder="请输入邮箱"></td>
                    </tr>

                    <tr>
                        <td class="td_left"><label for="name">姓名</label></td>
                        <td class="td_right"><input type="text" name="name" id="name" placeholder="请输入姓名"></td>
                    </tr>

                    <tr>
                        <td class="td_left"><label for="tel">手机号</label></td>
                        <td class="td_right"><input type="text" name="tel" id="tel" placeholder="请输入手机号"></td>
                    </tr>

                    <tr>
                        <td class="td_left"><label>性别</label></td>
                        <td class="td_right">
                            <input type="radio" name="gender" value="male"> 男
                            <input type="radio" name="gender" value="female"> 女
                        </td>
                    </tr>

                    <tr>
                        <td class="td_left"><label for="birthday">出生日期</label></td>
                        <td class="td_right"><input type="date" name="birthday" id="birthday" placeholder="请输入出生日期"></td>
                    </tr>

                    <tr>
                        <td class="td_left"><label for="checkcode" >验证码</label></td>
                        <td class="td_right"><input type="text" name="checkcode" id="checkcode" placeholder="请输入验证码">
                            <img id="img_check" src="img/verify_code.jpg">
                        </td>
                    </tr>


                    <tr>
                        <td colspan="2" id="td_sub"><input type="submit" id="btn_sub" value="注册"></td>
                    </tr>
                </table>

            </form>


        </div>

    </div>

    <div class="rg_right">
        <p>已有账号?<a href="#">立即登录</a></p>
    </div>


</div>

</body>
</html>
```

## 7. Bootstrap

### 7.1 Bootstrap概述

**概念：**一个前端开发的框架，Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基于 HTML、CSS、JavaScript 的，它简洁灵活，使得 Web 开发更加快捷。

框架：一个半成品软件，开发人员可以在框架基础上，再进行开发，简化编码。

**好处**

- 定义了很多的css样式和js插件。我们开发人员直接可以使用这些样式和插件得到丰富的页面效果。
- 响应式布局。
  - 同一套页面可以兼容不同分辨率的设备。

### 7.2 Bootstrap基础

**快速入门**

- 下载Bootstrap
- 在项目中将这三个文件夹复制(css，fonts，js)
- 创建html页面，引入必要的资源文件

模板代码

```HTML
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap HelloWorld</title>

    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet">


    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="js/jquery-3.2.1.min.js"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="js/bootstrap.min.js"></script>
</head>
<body>
<h1>你好，世界！</h1>

</body>
</html>
```

**响应式布局**

同一套页面可以兼容不同分辨率的设备。

实现：依赖于栅格系统，将一行平均分成12个格子，可以指定元素占几个格子。

步骤

- 定义容器。相当于之前的table
  - 容器分类
    - container：两边留白
    - container-fluid：每一种设备都是100%宽度
- 定义行。相当于之前的tr。样式：row
- 定义元素。指定该元素在不同的设备上，所占的格子数目。样式：col-设备代号-格子数目
  - 设备代号
    - xs：超小屏幕 手机 (<768px)：col-xs-12
    - sm：小屏幕 平板 (≥768px)
    - md：中等屏幕 桌面显示器 (≥992px)
    - lg：大屏幕 大桌面显示器 (≥1200px)
- 注意
  - 一行中如果格子数目超过12，则超出部分自动换行。
  - 栅格类属性可以向上兼容。栅格类适用于与屏幕宽度大于或等于分界点大小的设备。
  - 如果真实设备宽度小于了设置栅格类属性的设备代码的最小值，会一个元素占满一整行。

**CSS样式和JS插件**

全局CSS样式

- 按钮：class="btn btn-default"
- 图片
  - class="img-responsive"：图片在任意尺寸都占100%
  - img-rounded：方形
  - img-circle：圆形
  - img-thumbnail：相框
- 表格
  - table
  - table-bordered
  - table-hover
- 表单
  - 给表单项添加：class="form-control" 

组件

- 导航条
- 分页条

插件

- 轮播图

旅游网站案例改进版

```HTML
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap HelloWorld</title>

    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet">


    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="js/jquery-3.2.1.min.js"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="js/bootstrap.min.js"></script>
    <style>
        .paddtop {
            padding-top: 10px;
        }
        .search-btn {
            float: left;
            border: 2px solid #ffc900;
            width: 90px;
            height: 35px;
            background-color: #ffc900;
            text-align: center;
            line-height: 35px;
            margin-top: 15px;
        }
        .search-input {
            float: left;
            border: 2px solid #ffc900;
            width: 400px;
            height: 35px;
            padding-left: 5px;
            margin-top: 15px;
        }
        .jx {
            border-bottom: 2px solid #ffc900;
            padding: 5px;
        }
        .company {
            height: 40px;
            background-color: #ffc900;
            text-align: center;
            line-height: 40px;
            font-size: 8px;
        }
    </style>
</head>
<body>
<!--1.页眉部分-->
<header class="container-fluid">
    <div class="row">
        <img src="img/top_banner.jpg" class="img-responsive" width="100%">
    </div>
    <div class="row paddtop">
        <div class="col-md-3">
            <img src="img/logo.jpg" class="img-responsive">
        </div>
        <div class="col-md-5">
            <input class="search-input" placeholder="请输入线路名称">
            <a class="search-btn" href="#">搜索</a>
        </div>
        <div class="col-md-4">
            <img src="img/hotel_tel.png" class="img-responsive">
        </div>
    </div>
    <div class="row">
        <nav class="navbar navbar-default">
            <div class="container-fluid">
                <!-- Brand and toggle get grouped for better mobile display -->
                <div class="navbar-header">
                    <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
                        <span class="sr-only">Toggle navigation</span>
                        <span class="icon-bar"></span>
                        <span class="icon-bar"></span>
                        <span class="icon-bar"></span>
                    </button>
                    <a class="navbar-brand" href="#">首页</a>
                </div>

                <!-- Collect the nav links, forms, and other content for toggling -->
                <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                    <ul class="nav navbar-nav">
                        <li class="active"><a href="#">Link <span class="sr-only">(current)</span></a></li>
                        <li><a href="#">Link</a></li>
                        <li><a href="#">Link</a></li>
                        <li><a href="#">Link</a></li>
                        <li><a href="#">Link</a></li>
                        <li><a href="#">Link</a></li>
                        <li><a href="#">Link</a></li>
                    </ul>
                </div><!-- /.navbar-collapse -->
            </div><!-- /.container-fluid -->
        </nav>
    </div>
    <div class="row">
        <div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
            <!-- Indicators -->
            <ol class="carousel-indicators">
                <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
                <li data-target="#carousel-example-generic" data-slide-to="1"></li>
                <li data-target="#carousel-example-generic" data-slide-to="2"></li>
            </ol>

            <!-- Wrapper for slides -->
            <div class="carousel-inner" role="listbox">
                <div class="item active">
                    <img src="img/banner_1.jpg" width="100%" alt="...">
                </div>
                <div class="item">
                    <img src="img/banner_2.jpg" width="100%" alt="...">
                </div>
                <div class="item">
                    <img src="img/banner_3.jpg" width="100%" alt="...">
                </div>
            </div>

            <!-- Controls -->
            <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
                <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
                <span class="sr-only">Previous</span>
            </a>
            <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
                <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
                <span class="sr-only">Next</span>
            </a>
        </div>
    </div>
</header>
<!--2.主体部分-->
<div class="container">
    <div class="row jx">
        <img src="img/icon_5.jpg">
        <span>黑马精选</span>
    </div>
    <div class="row paddtop">
        <div class="col-md-3">
            <div class="img-thumbnail">
                <img src="img/jiangxuan_1.jpg" width="100%" alt="">
                <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                <font color="red">&yen; 899</font>
            </div>
        </div>
        <div class="col-md-3">
            <div class="img-thumbnail">
                <img src="img/jiangxuan_1.jpg" width="100%" alt="">
                <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                <font color="red">&yen; 899</font>
            </div>
        </div>
        <div class="col-md-3">
            <div class="img-thumbnail">
                <img src="img/jiangxuan_1.jpg" width="100%" alt="">
                <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                <font color="red">&yen; 899</font>
            </div>
        </div>
        <div class="col-md-3">
            <div class="img-thumbnail">
                <img src="img/jiangxuan_1.jpg" width="100%" alt="">
                <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                <font color="red">&yen; 899</font>
            </div>
        </div>
    </div>

    <div class="row jx">
        <img src="img/icon_6.jpg">
        <span>国内游</span>
    </div>
    <div class="row paddtop">
        <div class="col-md-4">
            <img src="img/guonei_1.jpg">
        </div>
        <div class="col-md-8">
            <div class="row">
                <div class="col-md-4">
                    <div class="img-thumbnail">
                        <img src="img/jiangxuan_2.jpg" width="100%" alt="">
                        <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                        <font color="red">&yen; 899</font>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="img-thumbnail">
                        <img src="img/jiangxuan_2.jpg" width="100%" alt="">
                        <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                        <font color="red">&yen; 899</font>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="img-thumbnail">
                        <img src="img/jiangxuan_2.jpg" width="100%" alt="">
                        <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                        <font color="red">&yen; 899</font>
                    </div>
                </div>
            </div>
            <div class="row" style="padding-top: 30px">
                <div class="col-md-4">
                    <div class="img-thumbnail">
                        <img src="img/jiangxuan_2.jpg" width="100%" alt="">
                        <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                        <font color="red">&yen; 899</font>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="img-thumbnail">
                        <img src="img/jiangxuan_2.jpg" width="100%" alt="">
                        <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                        <font color="red">&yen; 899</font>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="img-thumbnail">
                        <img src="img/jiangxuan_2.jpg" width="100%" alt="">
                        <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店任选+接送机)</p>
                        <font color="red">&yen; 899</font>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<!--3.页脚部分-->
<footer class="container-fluid">
    <div class="row paddtop">
        <img src="img/footer_service.png" width="100%" class="img-responsive">
    </div>
    <div class="row company">
        江苏传智播客教育科技股份有限公司 版权所有Copyright 2006-2018, All Rights Reserved 苏ICP备16007882
    </div>
</footer>

</body>
</html>
```

## 8. XML

### 8.1 XML概述

**概念：**Extensible Markup Language，可扩展标记语言。

- 可扩展：标签都是自定义的。`<user> <student>`

**功能**

- 存储数据
  - 配置文件
  - 在网络中传输

**xml与html区别**

- xml标签都是自定义的，html标签是预定义
- xml的语法严格，html语法松散
- xml是存储数据的，html是展示数据

**w3c：**万维网联盟

**语法**

基本语法

- xml文档的后缀名为 .xml
- xml第一行必须定义为文档声明
- xml文档中有且仅有一个根标签
- 属性值必须使用引号(单双都可)引起来
- 标签必须正确关闭
- xml标签名称区分大小写

快速入门

```XML
<?xml version='1.0' ?>
<users>
    <user id='1'>
        <name>zhangsan</name>
        <age>23</age>
        <gender>male</gender>
        <br/>
    </user>

    <user id='2'>
        <name>lisi</name>
        <age>24</age>
        <gender>female</gender>
    </user>
</users>
```

组成部分

- 文档声明
  - 格式：`<?xml 属性列表 ?>`
  - 属性列表
    - version：版本号，必须的属性
    - encoding：编码方式。告知解析引擎当前文档使用的字符集，默认值：ISO-8859-1
    - standalone：是否独立
      - 取值
        - yes：不依赖其他文件
        - no：依赖其他文件
- 指令(了解)：结合css的
  - `<?xml-stylesheet type="text/css" href="a.css" ?>`
- 标签：标签名称自定义的
  - 规则
    - 名称可以包含字母、数字以及其他的字符 
    - 名称不能以数字或者标点符号开始 
    - 名称不能以字母 xml（或者 XML、Xml 等等）开始 
    - 名称不能包含空格 
- 属性：id属性值唯一
- 文本
  - CDATA区：在该区域中的数据会被原样展示
    - 格式：`<![CDATA[ 数据 ]]>`

约束：规定xml文档的书写规则

- 作为框架的使用者(程序员)
  - 能够在xml中引入约束文档
  - 能够简单的读懂约束文档
- 分类
  - DTD：一种简单的约束技术
  - Schema：一种复杂的约束技术

DTD

- 引入dtd文档到xml文档中
  - 内部dtd：将约束规则定义在xml文档中
  - 外部dtd：将约束的规则定义在外部的dtd文件中
    - 本地：`<!DOCTYPE 根标签名 SYSTEM "dtd文件的位置">`
    - 网络：`<!DOCTYPE 根标签名 PUBLIC "dtd文件的名字" "dtd文件的位置URL">`

Schema

- 引入
  - 填写xml文档的根元素
  - 引入xsi前缀。xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  - 引入xsd文件命名空间。xsi:schemaLocation="http://www.itcast.cn/xml
  - 为每一个xsd约束声明一个前缀,作为标识 。xmlns="http://www.itcast.cn/xml"

```XML
<students  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns="http://www.itcast.cn/xml" 
           xsi:schemaLocation="http://www.itcast.cn/xml  student.xsd">
```

### 8.2 XML解析

**解析：**操作xml文档，将文档中的数据读取到内存中。

操作xml文档

- 解析(读取)：将文档中的数据读取到内存中。
- 写入：将内存中的数据保存到xml文档中。持久化存储。

解析xml的方式

- DOM：将标记语言文档一次性加载进内存，在内存中形成一颗dom树。
  - 优点：操作方便，可以对文档进行CRUD的所有操作。
  - 缺点：占内存。
- SAX：逐行读取，基于事件驱动的。
  - 优点：不占内存。
  - 缺点：只能读取，不能增删改。

xml常见的解析器

- JAXP：sun公司提供的解析器，支持dom和sax两种思想
- DOM4J：一款非常优秀的解析器
- Jsoup：jsoup是一款Java的HTML解析器，可直接解析某个URL地址、HTML文本内容
- PULL：Android操作系统内置的解析器，sax方式的

Jsoup：jsoup是一款Java的HTML解析器，可直接解析某个URL地址、HTML文本内容

- 快速入门
  - 步骤
    - 导入jar包
    - 获取Document对象
    - 获取对应的标签Element对象
    - 获取数据

```Java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;

public class JsoupDemo {
    public static void main(String[] args) throws Exception {
        // 获取Document对象，根据xml文档获取
        // 获取student.xml的path
        String path = JsoupDemo.class.getClassLoader().getResource("student.xml").getPath();
        // 解析xml文档，加载文档进内存，获取dom树--->Document
        Document document = Jsoup.parse(new File(path), "utf-8");
        // 获取元素对象 Element
        Elements elements = document.getElementsByTag("name");
        System.out.println(elements.size());
        // 获取第一个name的Element对象
        Element element = elements.get(0);
        String name = element.text();
        System.out.println(name);
    }
}
```

- 对象的使用
  - Jsoup：工具类，可以解析html或xml文档，返回Document
    - parse：解析html或xml文档，返回Document
      - parse(File in, String charsetName)：解析xml或html文件的
      - parse(String html)：解析xml或html字符串
      - parse(URL url, int timeoutMillis)：通过网络路径获取指定的html或xml的文档对象
  - Document：文档对象。代表内存中的dom树
    - 获取Element对象
      - getElementById(String id)：根据id属性值获取唯一的element对象
      - getElementsByTag(String tagName)：根据标签名称获取元素对象集合
      - getElementsByAttribute(String key)：根据属性名称获取元素对象集合
      - getElementsByAttributeValue(String key, String value)：根据对应的属性名和属性值获取元素对象集合
  - Elements：元素Element对象的集合。可以当做 ArrayList\<Element>来使用
  - Element：元素对象
    - 获取子元素对象
      - getElementById(String id)：根据id属性值获取唯一的element对象
      - getElementsByTag(String tagName)：根据标签名称获取元素对象集合
      - getElementsByAttribute(String key)：根据属性名称获取元素对象集合
      - getElementsByAttributeValue(String key, String value)：根据对应的属性名和属性值获取元素对象集合
    - 获取属性值
      - String attr(String key)：根据属性名称获取属性值
    - 获取文本内容
      - String text()：获取所有子标签的纯文本内容
      - String html()：获取标签体的所有内容(包括子标签的标签和文本内容)
  - Node：节点对象
    - 是Document和Element的父类
- 快捷查询方式
  - selector：选择器
    - 使用的方法：Elements select(String cssQuery)
      - 语法：参考Selector类中定义的语法
  - XPath：XPath即为XML路径语言，它是一种用来确定XML（标准通用标记语言的子集）文档中某部分位置的语言
    - 使用Jsoup的Xpath需要额外导入jar包
    - 查询w3cshool参考手册，使用xpath的语法完成查询

选择器查询案例

```Java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

import java.io.File;

public class JsoupDemo4 {
    public static void main(String[] args) throws Exception {
        String path = JsoupDemo4.class.getClassLoader().getResource("student.xml").getPath();
        Document document = Jsoup.parse(new File(path), "utf-8");
        Elements elements = document.select("name");
        System.out.println(elements);
        System.out.println("--------------------------------");
        Elements elements1 = document.select("#itahu");
        System.out.println(elements1);
        System.out.println("--------------------------------");
        Elements elements2 = document.select("student[number='heima_0001']");
        System.out.println(elements2);
        System.out.println("--------------------------------");
        Elements elements3 = document.select("student[number='heima_0001'] > age");
        System.out.println(elements3);
    }
}
```

Xpath练习案例

```Java
import cn.wanghaomiao.xpath.model.JXDocument;
import cn.wanghaomiao.xpath.model.JXNode;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

import java.io.File;
import java.util.List;

public class JsoupDemo5 {
    public static void main(String[] args) throws Exception {
        String path = JsoupDemo5.class.getClassLoader().getResource("student.xml").getPath();
        Document document = Jsoup.parse(new File(path), "utf-8");
        // 根据document对象，创建JXDocument对象
        JXDocument jxDocument = new JXDocument(document);
        // 结合xpath语法查询
        // 查询所有student标签
        List<JXNode> jxNodes = jxDocument.selN("//student");
        for (JXNode jxNode : jxNodes) {
            System.out.println(jxNode);
        }
        System.out.println("------------------------------------");
        // 查询所有student标签下的name标签
        List<JXNode> jxNodes1 = jxDocument.selN("//student/name");
        for (JXNode jxNode : jxNodes1) {
            System.out.println(jxNode);
        }
        System.out.println("------------------------------------");
        // 查询student标签下带有id属性的name标签
        List<JXNode> jxNodes2 = jxDocument.selN("//student/name[@id]");
        for (JXNode jxNode : jxNodes2) {
            System.out.println(jxNode);
        }
        System.out.println("------------------------------------");
        // 查询student标签下带有id属性的name标签，并且id属性值为itahu
        List<JXNode> jxNodes3 = jxDocument.selN("//student/name[@id='itahu']");
        for (JXNode jxNode : jxNodes3) {
            System.out.println(jxNode);
        }
        System.out.println("------------------------------------");
    }
}
```

