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

## 9. Tomcat

### 9.1 Web相关概念

**软件架构**

- C/S：客户端/服务器端
- B/S：浏览器/服务器端

**资源分类**

- 静态资源：所有用户访问后，得到的结果都是一样的，称为静态资源。静态资源可以直接被浏览器解析
  - 如：html，css，JavaScript
- 动态资源：每个用户访问相同资源后，得到的结果可能不一样。称为动态资源。动态资源被访问后，需要先转换为静态资源，再返回给浏览器
  - servlet/jsp，php，asp....

**网络通信三要素**

- IP：电子设备(计算机)在网络中的唯一标识
- 端口：应用程序在计算机中的唯一标识，0~65536
- 传输协议：规定了数据传输的规则
  - 基础协议
    - tcp：安全协议，三次握手。 速度稍慢
    - udp：不安全协议。 速度快

**Web服务器软件**

服务器：安装了服务器软件的计算机。

服务器软件：接收用户的请求，处理请求，做出响应。

Web服务器软件：接收用户的请求，处理请求，做出响应。

- 在Web服务器软件中，可以部署Web项目，让用户通过浏览器来访问这些项目
- Web容器

常见的Java相关的Web服务器软件

- webLogic：oracle公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
- webSphere：IBM公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
- JBOSS：JBOSS公司的，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
- Tomcat：Apache基金组织，中小型的JavaEE服务器，仅仅支持少量的JavaEE规范servlet/jsp。开源的，免费的。

JavaEE：Java语言在企业级开发中使用的技术规范的总和，一共规定了13项大的规范。

Tomcat：Web服务器软件。

1. 下载：http://tomcat.apache.org/

2. 安装：解压压缩包即可

   - 注意：安装目录建议不要有中文和空格

3. 卸载：删除目录就行了

4. 启动

   - bin/startup.bat，双击运行该文件即可

   - 访问：浏览器输入：http://localhost:8080 回车访问自己

   - http://别人的ip:8080 访问别人

   - 可能遇到的问题

     - 黑窗口一闪而过

       - 原因：没有正确配置JAVA_HOME环境变量
       - 解决方案：正确配置JAVA_HOME环境变量

     - 启动报错

       - 暴力：找到占用的端口号，并且找到对应的进程，杀死该进程

         - netstat -ano

       - 温柔：修改自身的端口号

         - conf/server.xml

         - ```XML
           <Connector port="8888" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8445" />
           ```

         - 一般会将tomcat的默认端口号修改为80。80端口号是http协议的默认端口号

           - 好处：在访问时，就不用输入端口号

5. 关闭

   - 正常关闭
     - bin/shutdown.bat
     - ctrl+c
   - 强制关闭
     - 点击启动窗口的x

6. 配置

   - 部署项目的方式
     1. 直接将项目放到webapps目录下即可
        - /hello：项目的访问路径-->虚拟目录
        - 简化部署：将项目打成一个war包，再将war包放置到webapps目录下
          - war包会自动解压缩
     2. 配置conf/server.xml文件
        - 在\<Host>标签体中配置
        - `<Context docBase="D:\hello" path="/hehe" />`
        - docBase：项目存放的路径
        - path：虚拟目录
     3. 在conf\Catalina\localhost创建任意名称的xml文件。在文件中编写`<Context docBase="D:\hello" />`
        - 虚拟目录：xml文件的名称
   - 静态项目和动态项目
     - 目录结构
     - java动态项目的目录结构
       - 项目的根目录
         - WEB-INF目录
           - web.xml：web项目的核心配置文件
           - classes目录：放置字节码文件的目录
           - lib目录：放置依赖的jar包
   - 将Tomcat集成到IDEA中，并且创建JavaEE的项目，部署项目

### 9.2 Servlet入门

**Servlet：server applet**

概念：运行在服务器端的小程序。

- Servlet就是一个接口，定义了Java类被浏览器访问到(tomcat识别)的规则。
- 将来我们自定义一个类，实现Servlet接口，复写方法。

**快速入门**

1. 创建JavaEE项目

2. 定义一个类，实现Servlet接口

   - public class ServletDemo implements Servlet

3. 实现接口中的抽象方法

4. 配置Servlet

   - 在web.xml中配置

   - ```XML
     <!--配置Servlet-->
     <servlet>
         <servlet-name>demo1</servlet-name>
         <servlet-class>com.itahu.web.servlet.ServletDemo</servlet-class>
     </servlet>
     
     <servlet-mapping>
         <servlet-name>demo1</servlet-name>
         <url-pattern>/demo1</url-pattern>
     </servlet-mapping>
     ```

**执行原理**

1. 当服务器接受到客户端浏览器的请求后，会解析请求URL路径，获取访问的Servlet的资源路径
2. 查找web.xml文件，是否有对应的\<url-pattern>标签体内容
3. 如果有，则再找到对应的\<servlet-class>全类名
4. tomcat会将字节码文件加载进内存，并且创建其对象
5. 调用其方法

**Servlet中的生命周期方法**

1.被创建：执行init方法，只执行一次

- Servlet什么时候被创建？
  - 默认情况下，第一次被访问时，Servlet被创建
  - 可以配置执行Servlet的创建时机
    - 在\<servlet>标签下配置
      1. 第一次被访问时，创建
         - \<load-on-startup>的值为负数
      2. 在服务器启动时，创建
         - \<load-on-startup>的值为0或正整数
- Servlet的init方法，只执行一次，说明一个Servlet在内存中只存在一个对象，Servlet是单例的
  - 多个用户同时访问时，可能存在线程安全问题
  - 解决：尽量不要在Servlet中定义成员变量。即使定义了成员变量，也不要对其修改值

2.提供服务：执行service方法，执行多次

- 每次访问Servlet时，Service方法都会被调用一次

3.被销毁：执行destroy方法，只执行一次

- Servlet被销毁时执行。服务器关闭时，Servlet被销毁
- 只有服务器正常关闭时，才会执行destroy方法
- destroy方法在Servlet被销毁之前执行，一般用于释放资源

**Servlet3.0**

好处：支持注解配置。可以不需要web.xml了。

步骤

1. 创建JavaEE项目，选择Servlet的版本3.0以上，可以不创建web.xml
2. 定义一个类，实现Servlet接口
3. 复写方法
4. 在类上使用@WebServlet注解，进行配置
   - @WebServlet("资源路径")

**IDEA与tomcat的相关配置**

1.IDEA会为每一个tomcat部署的项目单独建立一份配置文件

- Using CATALINA_BASE:   "C:\Users\Administrator\AppData\Local\JetBrains\IntelliJIdea2021.2\tomcat\767c7c00-8189-417c-b629-a822e72a7603"

2.工作空间项目和tomcat部署的web项目

- tomcat真正访问的是“tomcat部署的web项目”，"tomcat部署的web项目"对应着"工作空间项目"的web目录下的所有资源
- WEB-INF目录下的资源不能被浏览器直接访问

3.断点调试：使用"小虫子"启动 debug 启动

### 9.3 Servlet体系结构

**Servlet**

1.概念

2.步骤

3.执行原理

4.生命周期

5.Servlet3.0注解配置

6.Servlet的体系结构

- Servlet -- 接口
- GenericServlet -- 抽象类
- HttpServlet -- 抽象类
- GenericServlet：将Servlet接口中其他的方法做了默认空实现，只将service()方法作为抽象
  - 将来定义Servlet类时，可以继承GenericServlet，实现service()方法即可
- HttpServlet：对http协议的一种封装，简化操作
  - 定义类继承HttpServlet
  - 复写doGet/doPost方法

7.Servlet相关配置

- urlpartten：Servlet访问路径
  - 一个Servlet可以定义多个访问路径：@WebServlet({"/d4","/dd4","/ddd4"})
  - 路径定义规则
    - /xxx：路径匹配
    - /xxx/xxx：多层路径，目录结构
    - *.do：扩展名匹配

## 10. HTTP请求与Request

### 10.1 HTTP概述

**概念：**Hyper Text Transfer Protocol，超文本传输协议。

- 传输协议：定义了客户端和服务器端通信时，发送数据的格式
- 特点
  - 基于TCP/IP的高级协议
  - 默认端口号：80
  - 基于请求/响应模型的：一次请求对应一次响应
  - 无状态的：每次请求之间相互独立，不能交互数据
- 历史版本
  - 1.0：每一次请求响应都会建立新的连接
  - 1.1：复用连接

请求消息数据格式

1. 请求行
   - 请求方式 请求url 请求协议/版本
   - GET       /login.html	 HTTP/1.1
   - 请求方式
     - HTTP协议有7种请求方式，常用的有2种
       - GET
         1. 请求参数在请求行中，在url后
         2. 请求的url长度是有限制的
         3. 不太安全
       - POST
         1. 请求参数在请求体中
         2. 请求的url长度是没有限制的
         3. 相对安全
2. 请求头：客户端浏览器告诉服务器一些信息
   - 请求头名称：请求头值
   - 常见的请求头
     1. User-Agent：浏览器告诉服务器，我访问你使用的浏览器版本信息
        - 可以在服务器端获取该头的信息，解决浏览器的兼容性问题
     2. Referer：http://localhost/login.html
        - 告诉服务器，我(当前请求)从哪里来？
          - 作用
            1. 防盗链
            2. 统计工作
3. 请求空行
   - 空行，就是用于分割POST请求的请求头，和请求体的
4. 请求体(正文)
   - 封装POST请求消息的请求参数的

- 字符串格式

- ```Text
  POST /login.html	HTTP/1.1
  Host: localhost
  User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:60.0) Gecko/20100101 Firefox/60.0
  Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
  Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
  Accept-Encoding: gzip, deflate
  Referer: http://localhost/login.html
  Connection: keep-alive
  Upgrade-Insecure-Requests: 1
  
  username=zhangsan
  ```

响应消息数据格式

### 10.2 Request

**request对象和response对象的原理**

- request和response对象是由服务器创建的。我们来使用它们
- request对象是来获取请求消息，response对象是来设置响应消息

**request对象继承体系结构**

- ServletRequest	--	接口
- ​	|	继承
- HttpServletRequest	--	接口
- ​	|	实现
- org.apache.catalina.connector.RequestFacade 类(tomcat)

**request功能**

1.获取请求消息数据

1. 获取请求行数据
   - GET /Day11/demo01?name=zhangsan HTTP/1.1
   - 方法
     1. 获取请求方式：GET
        - String getMethod()
     2. (*)获取虚拟目录：/Day11
        - String getContextPath()
     3. 获取Servlet路径:：/demo01
        - String getServletPath()
     4. 获取get方式请求参数：name=zhangsan
        - String getQueryString()
     5. (*)获取请求URI：/Day11/demo01
        - String getRequestURI()：	/Day11/demo01
        - StringBuffer getRequestURL()：	http://localhost/Day11/demo01
        - URL：统一资源定位符：http://localhost/Day11/demo01	中华人民共和国
        - URI：统一资源标识符：/Day11/demo01	共和国
     6. 获取协议及版本：HTTP/1.1
        - String getProtocol()
     7. 获取客户机的IP地址
        - String getRemoteAddr()
2. 获取请求头数据
   - 方法
     - (*)String getHeader(String name)：通过请求头的名称获取请求头的值
     - Enumeration\<String> getHeaderNames()：获取所有的请求头名称
3. 获取请求体数据
   - 请求体：只有POST请求方式，才有请求体，在请求体中封装了POST请求的请求参数
   - 步骤
     1. 获取流对象
        - BufferedReader getReader()：获取字符输入流，只能操作字符数据
        - ServletInputStream getInputStream()：获取字节输入流，可以操作所有类型数据
          - 在文件上传知识点后讲解
     2. 再从流对象中拿数据

2.其他功能

1. 获取请求参数通用方式：不论get还是post请求方式都可以使用下列方法来获取请求参数
   - String getParameter(String name)：根据参数名称获取参数值    username=zs&password=123
   - String[] getParameterValues(String name)：根据参数名称获取参数值的数组  hobby=xx&hobby=game
   - Enumeration\<String> getParameterNames()：获取所有请求的参数名称
   - Map<String,String[]> getParameterMap()：获取所有参数的map集合
   - 中文乱码问题
     - get方式：tomcat8已经将get方式乱码问题解决了
     - post方式：会乱码
       - 解决：在获取参数前，设置request的编码request.setCharacterEncoding("utf-8");
2. 请求转发：一种在服务器内部的资源跳转方式
   - 步骤
     1. 通过request对象获取请求转发器对象：RequestDispatcher getRequestDispatcher(String path)
     2. 使用RequestDispatcher对象来进行转发：forward(ServletRequest request, ServletResponse response)
   - 特点
     1. 浏览器地址栏路径不发生变化
     2. 只能转发到当前服务器内部资源中
     3. 转发是一次请求
3. 共享数据
   - 域对象：一个有作用范围的对象，可以在范围内共享数据
   - request域：代表一次请求的范围，一般用于请求转发的多个资源中共享数据
   - 方法
     1. void setAttribute(String name,Object obj)：存储数据
     2. Object getAttitude(String name)：通过键获取值
     3. void removeAttribute(String name)：通过键移除键值对
4. 获取ServletContext
   - ServletContext getServletContext()

### 10.3 用户登录案例

**用户登录案例需求**

1. 编写login.html登录页面，username & password 两个输入
2. 使用Druid数据库连接池技术，操作mysql，day14数据库中user表
3. 使用JdbcTemplate技术封装JDBC
4. 登录成功跳转到SuccessServlet展示：登录成功！用户名，欢迎您
5. 登录失败跳转到FailServlet展示：登录失败，用户名或密码错误

**分析**

**开发步骤**

1. 创建项目，导入html页面，配置文件，jar包
2. 创建数据库环境

```SQL
CREATE DATABASE day12;
USE day12;
CREATE TABLE USER(
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(32) UNIQUE NOT NULL,
    PASSWORD VARCHAR(32) NOT NULL
);
```

3. 创建包cn.itahu.domain，创建类User

```Java
/**
 * 用户实体类
 */
public class User {
    private int id;
    private String username;
    private String password;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}
```

4. 创建包cn.itahu.util，编写工具类JDBCUtils

```Java
import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.sql.DataSource;
import java.io.IOException;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Properties;

/**
 * JDBC工具类，使用Druid连接池
 */
public class JDBCUtils {
    private static DataSource ds;

    static {
        try {
            Properties pro = new Properties();
            InputStream is = JDBCUtils.class.getClassLoader().getResourceAsStream("druid.properties");
            pro.load(is);

            ds = DruidDataSourceFactory.createDataSource(pro);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static DataSource getDataSource() {
        return ds;
    }

    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }
}
```

5. 创建包cn.itahu.dao，创建类UserDao，提供login方法

```Java
import cn.itahu.domain.User;
import cn.itahu.util.JDBCUtils;
import org.springframework.dao.DataAccessException;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;

/**
 * 操作数据库中user表的类
 */
public class UserDao {
    private JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());

    public User login(User loginUser) {
        try {
            String sql = "select * from user where username = ? and password = ?";
            User user = template.queryForObject(sql, new BeanPropertyRowMapper<User>(User.class), loginUser.getUsername(), loginUser.getPassword());
            return user;
        } catch (DataAccessException e) {
            e.printStackTrace();
            return null;
        }
    }
}
```

6. 编写cn.itahu.web.servlet.LoginServlet类

```Java
import cn.itahu.dao.UserDao;
import cn.itahu.domain.User;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("utf-8");
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        User loginUser = new User();
        loginUser.setUsername(username);
        loginUser.setPassword(password);

        UserDao dao = new UserDao();
        User user = dao.login(loginUser);

        if (user == null) {
            req.getRequestDispatcher("/failServlet").forward(req,resp);
        } else {
            req.setAttribute("user",user);
            req.getRequestDispatcher("/successServlet").forward(req,resp);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req,resp);
    }
}
```

7. 编写failServlet和successServlet类

```Java
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

@WebServlet("/failServlet")
public class failServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().write("登录失败，用户名或密码错误");
    }
}
```

```Java
import cn.itahu.domain.User;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/successServlet")
public class successServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        User user = (User) request.getAttribute("user");
        if (user != null) {
            response.setContentType("text/html;charset=utf-8");
            response.getWriter().write("登录成功！" + user.getUsername() + "，欢迎您");
        }
    }
}
```

8. login.html中form表单的action路径的写法
   - 虚拟目录+Servlet的资源路径
9. BeanUtils工具类，简化数据封装
   - 用于封装JavaBean的
   - JavaBean：标准的Java类
     - 要求
       1. 类必须被public修饰
       2. 必须提供空参的构造器
       3. 成员变量必须使用private修饰
       4. 提供公共setter和getter方法
     - 功能：封装数据
   - 概念
     1. 成员变量
     2. 属性：setter和getter方法截取后的产物
        - 例如：getUsername() --> Username --> username
   - 方法
     - setProperty()
     - getProperty()
     - populate(Object obj , Map map)：将map集合的键值对信息，封装到对应的JavaBean对象中

## 11. HTTP响应与Response

### 11.1 HTTP响应消息

**请求消息：**客户端发送给服务器端的数据。

数据格式

1. 请求行
2. 请求头
3. 请求空行
4. 请求体

**响应消息：**服务器端发送给客户端的数据。

数据格式

1. 响应行
   - 组成：协议/版本 响应状态码 状态码描述
   - 响应状态码：服务器告诉客户端浏览器本次请求和响应的一个状态
     - 状态码都是3位数字
     - 分类
       1. 1xx：服务器就收客户端消息，但没有接收完成，等待一段时间后，发送1xx多状态码
       2. 2xx：成功。代表：200
       3. 3xx：重定向。代表：302(重定向)，304(访问缓存)
       4. 4xx：客户端错误。
          - 代表
            - 404：请求路径没有对应的资源
            - 405：请求方式没有对应的doXxx方法
       5. 5xx：服务器端错误。代表：500(服务器内部出现异常)
2. 响应头
   - 格式：头名称：值
   - 常见的响应头
     1. Content-Type：服务器告诉客户端本次响应体数据格式以及编码格式
     2. Content-disposition：服务器告诉客户端以什么格式打开响应体数据
        - 值
          - in-line：默认值，在当前页面内打开
          - attachment;filename=xxx：以附件形式打开响应体。文件下载
3. 响应空行
4. 响应体：传输的数据

响应字符串格式

```Text
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 100
Date: Wed, 29 Dec 2021 00:55:43 GMT
```

```HTML
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
  hello, response
  </body>
</html>
```

### 11.2 Response

**功能：**设置响应消息

1.设置响应行

- 格式：HTTP/1.1 200 OK
- 设置状态码：setStatus(int sc) 

2.设置响应头：setHeader(String name, String value) 

3.设置响应体

- 使用步骤
  - 获取输出流
    - 字符输出流：PrintWriter getWriter()
    - 字节输出流：ServletOutputStream getOutputStream()
  - 使用输出流，将数据输出到客户端浏览器

**案例**

1.完成重定向

- 重定向：资源跳转的方式
- 代码实现
  - 设置状态码为302
  - response.setStatus(302);
  - 设置响应头location
  - response.setHeader("location","/Day13/responseDemo2");
  - 简单的重定向方法
  - response.sendRedirect("/Day13/responseDemo2");
- 重定向的特点：redirect
  1. 地址栏发生变化
  2. 重定向可以访问其他站点(服务器)的资源
  3. 重定向是两次请求，不能使用request对象来共享数据
- 转发的特点：forward
  1. 转发地址栏路径不变
  2. 转发只能访问当前服务器下的资源
  3. 转发是一次请求，可以使用request对象来共享数据
- forward 和 redirect 区别
- 路径写法
  - 路径分类
    1. 相对路径：通过相对路径不可以确定唯一资源
       - 如：./index.html
       - 不以/开头，以.开头路径
       - 规则：找到当前资源和目标资源之间的相对位置关系
         - ./：当前目录
         - ../：后退一级目录
    2. 绝对路径：通过绝对路径可以确定唯一资源
       - 如：http://localhost/Day13/responseDemo2  /Day13/responseDemo2
       - 以/开头的路径
       - 规则：判断定义的路径是给谁用的？判断请求将来从哪儿发出
         - 给客户端浏览器使用：需要加虚拟目录(项目的访问路径)
           - 建议虚拟目录动态获取：request.getContextPath()
           - \<a> , \<form> 重定向...
         - 给服务器使用：不需要加虚拟目录
           - 转发路径

2.服务器输出字符数据到浏览器

- 步骤
  - 获取字符输出流
  - 输出数据
- 注意
  - 乱码问题
    1. PrintWriter pw = response.getWriter(); 获取的流的默认编码是ISO-8859-1
    2. 设置该流的默认编码
    3. 告诉浏览器响应体使用的编码
  - response.setContentType("text/html;charset=utf-8");

3.服务器输出字节数据到浏览器

- 步骤
  - 获取字节输出流
  - 输出数据

4.验证码

- 本质：图片
- 目的：防止恶意表单注册

画验证码代码

```Java
import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

@WebServlet("/checkCodeServlet")
public class CheckCodeServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        int width = 100;
        int height = 50;
        BufferedImage image = new BufferedImage(width,height,BufferedImage.TYPE_INT_RGB);

        Graphics g = image.getGraphics();
        g.setColor(Color.PINK);
        g.fillRect(0,0,width,height);

        g.setColor(Color.blue);
        g.drawRect(0,0,width - 1,height - 1);

        String str = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
        Random ran = new Random();
        for (int i = 1; i <= 4; i++) {
            int index = ran.nextInt(str.length());
            char ch = str.charAt(index);
            g.drawString(ch + "",width/5*i,height/2);
        }

        g.setColor(Color.GREEN);
        for (int i = 0; i < 10; i++) {
            int x1 = ran.nextInt(width);
            int x2 = ran.nextInt(width);
            int y1 = ran.nextInt(height);
            int y2 = ran.nextInt(height);
            g.drawLine(x1,y1,x2,y2);
        }

        ImageIO.write(image,"jpg",response.getOutputStream());
    }
}
```

点击切换验证码

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        window.onload = function () {
            document.getElementById("checkCode").onclick = function () {
                var date = new Date().getTime();
                this.src = "/Day13/checkCodeServlet?" + date;
            }

            document.getElementById("change").onclick = function () {
                var date = new Date().getTime();
                document.getElementById("checkCode").src = "/Day13/checkCodeServlet?" + date;
            }
        }
    </script>
</head>
<body>
    <img id="checkCode" src="/Day13/checkCodeServlet"/>
    <a id="change" href="">看不清换一张？</a>
</body>
</html>
```

### 11.3 ServletContext

**概念：**代表整个web应用，可以和程序的容器(服务器)来通信。

**获取**

1.通过request对象获取

- request.getServletContext();

2.通过HttpServlet获取

- this.getServletContext();

**功能**

1.获取MIME类型

- MIME类型：在互联网通信过程中定义的一种文件数据类型
  - 格式：大类型/小类型   text/html   image/jpeg
- 获取：String getMimeType(String file)

2.域对象：共享数据

- setAttribute(String name,Object value)
- getAttribute(String name)
- removeAttribute(String name)
- ServletContext对象范围：所有用户所有请求的数据

3.获取文件的真实(服务器)路径

- 方法
  - String getRealPath(String path)
  - String b = context.getRealPath("/b.txt"); //web目录下资源访问
  - String c = context.getRealPath("/WEB-INF/c.txt"); //WEB-INF目录下的资源访问
  - String a = context.getRealPath("/WEB-INF/classes/a.txt"); //src目录下的资源访问

**案例**

文件下载需求

1. 页面显示超链接
2. 点击超链接后弹出下载提示框
3. 完成图片文件下载

分析

1. 超链接指向的资源如果能够被浏览器解析，则在浏览器中展示，如果不能解析，则弹出下载提示框。不满足需求
2. 任何资源都必须弹出下载提示框
3. 使用响应头设置资源的打开方式
   - content-disposition:attachment;filename=xxx

步骤

1. 定义页面，编辑超链接href属性，指向Servlet，传递资源名称filename
2. 定义Servlet
   - 获取文件名称
   - 使用字节输入流加载文件进内存
   - 指定response的响应头：content-disposition:attachment;filename=xxx
   - 将数据写出到response输出流

问题

- 中文文件问题
  - 解决思路
    1. 获取客户端使用的浏览器版本信息
    2. 根据不同的版本信息，设置filename的编码方式不同

前端页面

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
  <a href="/Day13/img/九尾.jpg">图片1</a>
  <a href="/Day13/img/1.mp4">视频</a>
  <hr>
  <a href="/Day13/downLoadServlet?filename=九尾.jpg">图片1</a>
  <a href="/Day13/downLoadServlet?filename=1.mp4">视频</a>
</body>
</html>
```

中文文件名乱码解决工具类

```Java
import sun.misc.BASE64Encoder;
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;


public class DownLoadUtils {

    public static String getFileName(String agent, String filename) throws UnsupportedEncodingException {
        if (agent.contains("MSIE")) {
            // IE浏览器
            filename = URLEncoder.encode(filename, "utf-8");
            filename = filename.replace("+", " ");
        } else if (agent.contains("Firefox")) {
            // 火狐浏览器
            BASE64Encoder base64Encoder = new BASE64Encoder();
            filename = "=?utf-8?B?" + base64Encoder.encode(filename.getBytes("utf-8")) + "?=";
        } else {
            // 其它浏览器
            filename = URLEncoder.encode(filename, "utf-8");
        }
        return filename;
    }
}
```

文件下载代码

```Java
import com.itahu.web.utils.DownLoadUtils;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.FileInputStream;
import java.io.IOException;

@WebServlet(value = "/downLoadServlet")
public class DownloadServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String filename = request.getParameter("filename");
        ServletContext servletContext = this.getServletContext();
        String realPath = servletContext.getRealPath("/img/" + filename);
        FileInputStream fis = new FileInputStream(realPath);

        String mimeType = servletContext.getMimeType(filename);
        response.setHeader("content-type",mimeType);

        String agent = request.getHeader("user-agent");
        filename = DownLoadUtils.getFileName(agent, filename);

        response.setHeader("content-disposition","attachment;filename=" + filename);

        ServletOutputStream sos = response.getOutputStream();
        byte[] buff = new byte[1024 * 8];
        int len = 0;
        while ((len = fis.read(buff)) != -1) {
            sos.write(buff,0,len);
        }
        fis.close();
    }
}
```

## 12. 会话技术

**会话：**一次会话中包含多次请求和响应。

- 一次会话：浏览器第一次给服务器资源发送请求，会话建立，直到有一方断开为止。

**功能：**在一次会话的范围内的多次请求间，共享数据。

**方式**

- 客户端会话技术：Cookie
- 服务器端会话技术：Session

### 12.1 Cookie

**概念：**客户端会话技术，将数据保存到客户端。

**快速入门**

- 使用步骤
  1. 创建Cookie对象，绑定数据
     - new Cookie(String name, String value) 
  2. 发送Cookie对象
     - response.addCookie(Cookie cookie)
  3. 获取Cookie，拿到数据
     - Cookie[]  request.getCookies()

**实现原理：**基于响应头set-cookie和请求头cookie实现。

**Cookie的细节**

1.一次可不可以发送多个cookie？

- 可以。
- 可以创建多个Cookie对象，使用response调用多次addCookie方法发送cookie即可。

2.cookie在浏览器中保存多长时间？

- 默认情况下，当浏览器关闭后，Cookie数据被销毁。
- 持久化存储
  - setMaxAge(int seconds)
    1. 正数：将Cookie数据写到硬盘的文件中。持久化存储。并指定cookie存活时间，时间到后，cookie文件自动失效。
    2. 负数：默认值。
    3. 零：删除cookie信息。

3.cookie能不能存中文？

- 在tomcat 8 之前 cookie中不能直接存储中文数据。
  - 需要将中文数据转码：一般采用URL编码(%E3)。
- 在tomcat 8 之后，cookie支持中文数据。特殊字符还是不支持，建议使用URL编码存储，URL解码解析。

4.cookie共享问题？

1. 假设在一个tomcat服务器中，部署了多个web项目，那么在这些web项目中cookie能不能共享？
   - 默认情况下cookie不能共享。
   - setPath(String path):设置cookie的获取范围。默认情况下，设置当前的虚拟目录。
     - 如果要共享，则可以将path设置为"/"。
2. 不同的tomcat服务器间cookie共享问题？
   - setDomain(String path)：如果设置一级域名相同，那么多个服务器之间cookie可以共享。
   - setDomain(".baidu.com")，那么tieba.baidu.com和news.baidu.com中cookie可以共享。

5.Cookie的特点和作用

1. cookie存储数据在客户端浏览器。
2. 浏览器对于单个cookie的大小有限制(4kb)以及对同一个域名下的总cookie数量也有限制(20个)

- 作用
  - cookie一般用于存出少量的不太敏感的数据
  - 在不登录的情况下，完成服务器对客户端的身份识别

6.案例：记住上一次访问时间

1. 需求
   - 访问一个Servlet，如果是第一次访问，则提示：您好，欢迎您首次访问。
   - 如果不是第一次访问，则提示：欢迎回来，您上次访问时间为：显示时间字符串。
2. 分析
   - 可以采用Cookie来完成
   - 在服务器中的Servlet判断是否有一个名为lastTime的cookie
     - 有：不是第一次访问
       1. 响应数据：欢迎回来，您上次访问时间为：2018年6月10日11:50:20
       2. 写回Cookie：lastTime=2018年6月10日11:50:01
     - 没有：是第一次访问
       1. 响应数据：您好，欢迎您首次访问
       2. 写回Cookie：lastTime=2018年6月10日11:50:01

```Java
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.net.URLDecoder;
import java.net.URLEncoder;
import java.text.SimpleDateFormat;
import java.util.Date;

@WebServlet("/CookieTest")
public class CookieTest extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        Cookie[] cookies = request.getCookies();
        boolean flag = false;
        if (cookies != null && cookies.length > 0) {
            for (Cookie cookie : cookies) {
                String name = cookie.getName();
                if ("lastTime".equals(name)) {
                    flag = true;
                    String value = cookie.getValue();
                    System.out.println(value);
                    value = URLDecoder.decode(value,"utf-8");
                    System.out.println(value);
                    response.getWriter().write("<h1>欢迎回来，您上次访问时间为：" + value + "</h1>");

                    Date date = new Date();
                    SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
                    String str_date = sdf.format(date);
                    System.out.println(str_date);
                    str_date = URLEncoder.encode(str_date,"utf-8");
                    System.out.println(str_date);
                    cookie.setValue(str_date);
                    cookie.setMaxAge(60 * 60 * 24 * 30);
                    response.addCookie(cookie);
                    break;
                }
            }
        }
        if (cookies == null || cookies.length == 0 || flag == false) {
            Date date = new Date();
            SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
            String str_date = sdf.format(date);
            System.out.println(str_date);
            str_date = URLEncoder.encode(str_date,"utf-8");
            System.out.println(str_date);
            Cookie cookie = new Cookie("lastTime",str_date);
            cookie.setMaxAge(60 * 60 * 24 * 30);
            response.addCookie(cookie);
            response.getWriter().write("<h1>您好，欢迎您首次访问</h1>");
        }
    }
}
```

### 12.2 JSP入门与Session

**JSP：入门学习**

概念：Java Server Pages，java服务器端页面。

- 可以理解为：一个特殊的页面，其中既可以指定定义html标签，又可以定义java代码。
- 用于简化书写！！！

原理：JSP本质上就是一个Servlet。

JSP的脚本：JSP定义Java代码的方式。

1. <% 代码 %>：定义的java代码，在service方法中。service方法中可以定义什么，该脚本中就可以定义什么。
2. <%! 代码 %>：定义的java代码，在jsp转换后的java类的成员位置。
3. <%= 代码 %>：定义的java代码，会输出到页面上。输出语句中可以定义什么，该脚本中就可以定义什么。

JSP的内置对象

- 在jsp页面中不需要获取和创建，可以直接使用的对象
- jsp一共有9个内置对象
- 今天学习3个
  - request
  - response
  - out：字符输出流对象。可以将数据输出到页面上。和response.getWriter()类似
    - response.getWriter()和out.write()的区别
      - 在tomcat服务器真正给客户端做出响应之前，会先找response缓冲区数据，再找out缓冲区数据
      - response.getWriter()数据输出永远在out.write()之前

案例：改造Cookie案例

```JSP
<%@ page import="java.net.URLDecoder" %>
<%@ page import="java.util.Date" %>
<%@ page import="java.text.SimpleDateFormat" %>
<%@ page import="java.net.URLEncoder" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Hello</title>
</head>
<body>
<%
    Cookie[] cookies = request.getCookies();
    boolean flag = false;
    if (cookies != null && cookies.length > 0) {
        for (Cookie cookie : cookies) {
            String name = cookie.getName();
            if ("lastTime".equals(name)) {
                flag = true;
                String value = cookie.getValue();
                System.out.println(value);
                value = URLDecoder.decode(value, "utf-8");
                System.out.println(value);
%>
<h1>欢迎回来，您上次访问时间为：<%=value%>
</h1>
<%
                Date date = new Date();
                SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
                String str_date = sdf.format(date);
                System.out.println(str_date);
                str_date = URLEncoder.encode(str_date, "utf-8");
                System.out.println(str_date);
                cookie.setValue(str_date);
                cookie.setMaxAge(60 * 60 * 24 * 30);
                response.addCookie(cookie);
                break;
            }
        }
    }
    if (cookies == null || cookies.length == 0 || flag == false) {
        Date date = new Date();
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
        String str_date = sdf.format(date);
        System.out.println(str_date);
        str_date = URLEncoder.encode(str_date, "utf-8");
        System.out.println(str_date);
        Cookie cookie = new Cookie("lastTime", str_date);
        cookie.setMaxAge(60 * 60 * 24 * 30);
        response.addCookie(cookie);
%>
<h1>您好，欢迎您首次访问</h1>
<span></span>
<%
    }
%>
</body>
</html>
```

**Session**

概念：服务器端会话技术，在一次会话的多次请求间共享数据，将数据保存在服务器端的对象中。HttpSession

快速入门

1. 获取HttpSession对象
   - HttpSession session = request.getSession();
2. 使用HttpSession对象
   - Object getAttribute(String name)  
   - void setAttribute(String name, Object value)
   - void removeAttribute(String name)

原理：Session的实现是依赖于Cookie的

细节

1. 当客户端关闭后，服务器不关闭，两次获取session是否为同一个？

   - 默认情况下。不是。

   - 如果需要相同，则可以创建Cookie，键为JSESSIONID，设置最大存活时间，让cookie持久化保存。

   - ```Java
     Cookie c = new Cookie("JSESSIONID",session.getId());
     c.setMaxAge(60 * 60);
     response.addCookie(c);
     ```

2. 客户端不关闭，服务器关闭后，两次获取的session是同一个吗？

   - 不是同一个，但是要确保数据不丢失。tomcat自动完成以下工作。
     - session的钝化
       - 在服务器正常关闭之前，将session对象序列化到硬盘上
     - session的活化
       - 在服务器启动后，将session文件转化为内存中的session对象即可 

3. session什么时候被销毁？

   - 服务器关闭

   - session对象调用invalidate()

   - session默认失效时间：30分钟

     - 选择性配置修改

     - ```XML
       <session-config>
           <session-timeout>30</session-timeout>
       </session-config>
       ```

session的特点

1. session用于存储一次会话的多次请求的数据，存在服务器端
2. session可以存储任意类型，任意大小的数据

- session与Cookie的区别
  - session存储数据在服务器端，Cookie在客户端
  - session没有数据大小限制，Cookie有
  - session数据安全，Cookie相对于不安全

**案例：验证码**

案例需求

1. 访问带有验证码的登录页面login.jsp
2. 用户输入用户名，密码以及验证码
   - 如果用户名和密码输入有误，跳转登录页面，提示：用户名或密码错误
   - 如果验证码输入有误，跳转登录页面，提示：验证码错误
   - 如果全部输入正确，则跳转到主页success.jsp，显示：用户名，欢迎您

验证码生成

```Java
import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

@WebServlet("/checkCodeServlet")
public class CheckCodeServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        int width = 100;
        int height = 50;
        BufferedImage image = new BufferedImage(width,height,BufferedImage.TYPE_INT_RGB);

        Graphics g = image.getGraphics();
        g.setColor(Color.PINK);
        g.fillRect(0,0,width,height);

        g.setColor(Color.blue);
        g.drawRect(0,0,width - 1,height - 1);

        String str = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
        Random ran = new Random();
        StringBuilder sb = new StringBuilder();
        for (int i = 1; i <= 4; i++) {
            int index = ran.nextInt(str.length());
            char ch = str.charAt(index);
            sb.append(ch);
            g.drawString(ch + "",width/5*i,height/2);
        }
        String checkCode_session = sb.toString();
        request.getSession().setAttribute("checkCode_session",checkCode_session);

        g.setColor(Color.GREEN);
        for (int i = 0; i < 10; i++) {
            int x1 = ran.nextInt(width);
            int x2 = ran.nextInt(width);
            int y1 = ran.nextInt(height);
            int y2 = ran.nextInt(height);
            g.drawLine(x1,y1,x2,y2);
        }

        ImageIO.write(image,"jpg",response.getOutputStream());
    }
}
```

登录逻辑

```Java
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        String checkCode = request.getParameter("checkCode");

        HttpSession session = request.getSession();
        String checkCode_session = (String) session.getAttribute("checkCode_session");
        session.removeAttribute("checkCode_session");
        if (checkCode_session != null && checkCode_session.equalsIgnoreCase(checkCode)) {
            if ("zhangsan".equals(username) && "123".equals(password)) {
                session.setAttribute("user",username);
                response.sendRedirect(request.getContextPath() + "/success.jsp");
            } else {
                request.setAttribute("login_error","用户名或密码错误");
                request.getRequestDispatcher("/login.jsp").forward(request,response);
            }
        } else {
            request.setAttribute("cc_error","验证码错误");
            request.getRequestDispatcher("/login.jsp").forward(request,response);
        }
    }
}
```

登录页面

```JSP
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>login</title>
    <script>
        window.onload = function () {
            document.getElementById("img").onclick = function () {
                this.src = "/Day14/checkCodeServlet?time=" + new Date().getTime();
            }
        }
    </script>
    <style>
        div {
            color: red;
        }
    </style>
</head>
<body>
    <form action="/Day14/loginServlet" method="post">
        <table>
            <tr>
                <td>用户名</td>
                <td><input type="text" name="username"></td>
            </tr>
            <tr>
                <td>密码</td>
                <td><input type="password" name="password"></td>
            </tr>
            <tr>
                <td>验证码</td>
                <td><input type="text" name="checkCode"></td>
            </tr>
            <tr>
                <td colspan="2"><img id="img" src="/Day14/checkCodeServlet"></td>
            </tr>
            <tr>
                <td colspan="2"><input type="submit" value="登录"></td>
            </tr>
        </table>
    </form>
    <div><%=request.getAttribute("cc_error") == null ? "" : request.getAttribute("cc_error")%></div>
    <div><%=request.getAttribute("login_error") == null ? "" : request.getAttribute("login_error")%></div>
</body>
</html>
```

登录成功页面

```JSP
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title><%=request.getSession().getAttribute("user")%>，欢迎您</title>
</head>
<body>
    <h1><%=request.getSession().getAttribute("user")%>，欢迎您</h1>
</body>
</html>
```

## 13. JSP、MVC、EL、JSTL

### 13.1 JSP

**指令**

作用：用于配置JSP页面，导入资源文件。

格式：<%@ 指令名称 属性名1=属性值1 属性名2=属性值2 ... %>

分类

1. page：配置JSP页面的
   - contentType：等同于response.setContentType()
     1. 设置响应体的mime类型以及字符集
     2. 设置当前jsp页面的编码（只能是高级的IDE才能生效，如果使用低级工具，则需要设置pageEncoding属性设置当前页面的字符集）
   - import：导包
   - errorPage：当前页面发生异常后，会自动跳转到指定的错误页面
   - isErrorPage：标识当前页面是否是错误页面
     - true：是，可以使用内置对象exception
     - false：否。默认值。不可以使用内置对象exception
2. include：页面包含的。导入页面的资源文件
   - <%@include file="top.jsp"%>
3. taglib：导入资源
   - <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
     - prefix：前缀，自定义的

**注释**

html注释

- \<!-- -->：只能注释html代码片段

jsp注释：推荐使用

- <%-- --%>：可以注释所有

**内置对象**

- 在jsp页面中不需要创建，直接使用的对象
- 一共有9个

|   变量名    |      真实类型       |                     作用                     |
| :---------: | :-----------------: | :------------------------------------------: |
| pageContext |     PageContext     | 当前页面共享数据，还可以获取其他八个内置对象 |
|   request   | HttpServletRequest  |         一次请求访问的多个资源(转发)         |
|   session   |     HttpSession     |             一次会话的多个请求间             |
| application |   ServletContext    |              所有用户间共享数据              |
|  response   | HttpServletResponse |                   响应对象                   |
|    page     |       Object        |        当前页面(Servlet)的对象  this         |
|     out     |      JspWriter      |          输出对象，数据输出到页面上          |
|   config    |    ServletConfig    |              Servlet的配置对象               |
|  exception  |      Throwable      |                   异常对象                   |

### 13.2 MVC：开发模式

**JSP演变历史**

1.早期只有servlet，只能使用response输出标签数据，非常麻烦

2.后来有Jsp，简化了Servlet的开发，如果过度使用jsp，在jsp中既写大量的java代码，又写html标签，造成难于维护，难于分工协作

3.再后来，java的web开发，借鉴mvc开发模式，使得程序的设计更加合理性

**MVC**

1.M：Model，模型。JavaBean

- 完成具体的业务操作，如：查询数据库，封装对象

2.V：View，视图。JSP

- 展示数据

3.C：Controller，控制器。Servlet

- 获取用户的输入
- 调用模型
- 将数据交给视图进行展示

**优缺点**

优点

1. 耦合性低，方便维护，可以利于分工协作
2. 重用性高

缺点

1. 使得项目架构变得复杂，对开发人员要求高

### 13.3 EL表达式

**概念：**Expression Language，表达式语言。

**作用：**替换和简化jsp页面中java代码的编写。

**语法：**${表达式}

**注意**

Jsp默认支持el表达式的。如果要忽略el表达式

- 设置jsp中page指令中：isELIgnored="true"，忽略当前jsp页面中所有的el表达式
- \${表达式}：忽略当前这个el表达式

**使用**

1.运算

- 运算符
  - 算术运算符：+ - * /(div) %(mod)
  - 比较运算符：> < >= <= == !=
  - 逻辑运算符：&&(and) ||(or) !(not)
  - 空运算符：empty
    - 功能：用于判断字符串、集合、数组对象是否为null或者长度是否为0
    - ${empty list}：判断字符串、集合、数组对象是否为null或者长度为0
    - ${not empty str}：表示判断字符串、集合、数组对象是否不为null并且长度>0

2.获取值

- el表达式只能从域对象中获取值
- 语法
  - ${域名称.键名}：从指定域中获取指定键的值
    - 域名称
      1. pageScope		    -->      pageContext
      2. requestScope 	  -->      request
      3. sessionScope        -->     session
      4. applicationScope -->      application（ServletContext）
    - 举例：在request域中存储了name=张三
    - 获取：${requestScope.name}
  - ${键名}：表示依次从最小的域中查找是否有该键对应的值，直到找到为止
  - 获取对象、List集合、Map集合的值
    1. 对象：${域名称.键名.属性名}
       - 本质上会去调用对象的getter方法
    2. List集合：${域名称.键名[索引]}
    3. Map集合
       - ${域名称.键名.key名称}
       - ${域名称.键名["key名称"]}

3.隐式对象

- el表达式中有11个隐式对象
- pageContext
  - 获取jsp其他八个内置对象
  - ${pageContext.request.contextPath}：动态获取虚拟目录

### 13.4 JSTL

**概念：**JavaServer Pages Tag Library，JSP标准标签库。

- 是由Apache组织提供的开源的免费的jsp标签		<标签>

**作用：**用于简化和替换jsp页面上的java代码。

**使用步骤**

1. 导入jstl相关jar包
2. 引入标签库。taglib指令：<%@ taglib %>
3. 使用标签

**常用的JSTL标签**

1.if：相当于java代码的if语句

- 属性
  - test 必须属性，接受boolean表达式
    - 如果表达式为true，则显示if标签体内容，如果为false，则不显示标签体内容
    - 一般情况下，test属性值会结合el表达式一起使用
- 注意
  - c:if标签没有else情况，想要else情况，则可以在定义一个c:if标签

2.choose：相当于java代码的switch语句

- 使用choose标签声明，相当于switch声明
- 使用when标签做判断，相当于case
- 使用otherwise标签做其他情况的声明，相当于default

3.foreach：相当于java代码的for语句

**练习：**在request域中有一个存有User对象的List集合。需要使用jstl+el将list集合数据展示到jsp页面的表格table中。

```JSP
<%@ page import="java.util.List" %>
<%@ page import="java.util.ArrayList" %>
<%@ page import="com.itahu.domain.User" %>
<%@ page import="java.util.Date" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>test</title>
</head>
<body>
<%
    List list = new ArrayList();
    list.add(new User("张三",23,new Date()));
    list.add(new User("李四",24,new Date()));
    list.add(new User("王五",25,new Date()));
    request.setAttribute("list",list);
%>
<table border="1" width="500" align="center">
    <tr>
        <th>编号</th>
        <th>姓名</th>
        <th>年龄</th>
        <th>生日</th>
    </tr>
    <c:forEach items="${list}" var="user" varStatus="s">
        <c:if test="${s.count % 2 != 0}">
            <tr bgcolor="red">
                <td>${s.count}</td>
                <td>${user.name}</td>
                <td>${user.age}</td>
                <td>${user.bitStr}</td>
            </tr>
        </c:if>
        <c:if test="${s.count % 2 == 0}">
            <tr bgcolor="green">
                <td>${s.count}</td>
                <td>${user.name}</td>
                <td>${user.age}</td>
                <td>${user.bitStr}</td>
            </tr>
        </c:if>
    </c:forEach>
</table>
</body>
</html>
```

**三层架构：软件设计架构**

1. 界面层(表示层)：用户看的得界面。用户可以通过界面上的组件和服务器进行交互。
2. 业务逻辑层：处理业务逻辑的。
3. 数据访问层：操作数据存储文件。

**案例：用户信息列表展示**

1.需求：用户信息的增删改查操作

2.设计

- 技术选型：Servlet+JSP+MySQL+JDBCTempleat+Druid+BeanUtilS+tomcat

- 数据库设计

- ```SQL
  create database day16; -- 创建数据库
  use day16; 			   -- 使用数据库
  create table user(     -- 创建表
      id int primary key auto_increment,
      name varchar(20) not null,
      gender varchar(5),
      age int,
      address varchar(32),
      qq	varchar(20),
      email varchar(50)
  );
  ```

3.开发

1. 环境搭建
   - 创建数据库环境
   - 创建项目，导入需要的jar包
2. 编码

4.测试

5.部署运维
