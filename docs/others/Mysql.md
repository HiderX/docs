# Mysql

SQL：Structured Query Language，操作关系型数据库的编程语言，是一套标准

sql是关系型数据库（RDBMS），建立在关系模型基础上，由多张相互连接的二维表组成的数据库。

## SQL

### 通用语法

1. 可以单行或多行书写，以分号结尾
2. 不区分大小写，关键字建议大写
3. 注释：
   - 单行：-- 注释内容 or # 注释内容
   - 多行：/*注释内容\*/

### SQL分类

| 分 类 | 全称                       | 说明                                                    |
| ----- | -------------------------- | ------------------------------------------------------- |
| DDL   | Data Definition Language   | 数据定义语言，用来定义数据库对象(数据库，表， 字段)     |
| DML   | Data Manipulation Language | 数据操作语言，用来对数据库表中的数据进行增删改          |
| DQL   | Data Query Language        | 数据查询语言，用来查询数据库中表的记录                  |
| DCL   | Data Control Language      | 数据控制语言，用来创建数据库用户、控制数据库的 访问权限 |

### DDL

#### 数据库操作

##### 查询

查询所有数据库

```sql
SHOW DATABASES;
```

查询当前数据库

```sql
SHOW DATABASE();
```

##### 创建

```sql
CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
```

##### 删除

```sql
DROP DATABASE [IF EXISTS] 数据库名;
```

##### 使用

```sql
USE 数据库名;
```

#### 表操作

##### 查询

查询当前数据库所有表

```sql
SHOW TABLES;
```

查询表结构

```sql
DESC 表名;
```

查询制定表的建表语句

```sql
SHOW CREATE TABLE 表名;
```

##### 创建

```sql
CREATE TABLE 表名(
    字段1 字段1类型[COMMENT 字段1注释],
    字段2 字段2类型[COMMENT 字段2注释],
    字段3 字段3类型[COMMENT 字段3注释],
    ......
    字段n 字段n类型[COMMENT 字段n注释]
)[COMMENT 表注释];
```

例子：

```sql
create table tb_user(
  	id int comment '编号',
  	name varchar(50) comment '姓名', 
  	age int comment '年龄', 
  	gender varchar(1) comment '性别'
) comment '用户表';
```

##### 修改

添加字段

```sql
ALTER TABLE 表名 ADD 字段名 类型 (长度) [ COMMENT 注释 ] [ 约束 ];
```

修改数据类型

```sql
ALTER TABLE 表名 MODIFY 字段名 新数据类型 (长度);
```

修改字段名和字段类型

```sql
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型 (长度) [ COMMENT 注释 ] [ 约束 ];
```

例如将emp表的nickname字段修改为username，类型为varchar(30)

```sql
ALTER TABLE emp CHANGE nickname username varchar(30) COMMENT '用户名';
```

删除字段

```sql
ALTER TABLE 表名 DROP 字段名;
```

修改表名

```sql
ALTER TABLE 表名 RENAME TO 新表名;
```

##### 删除

删除表

```sql
DROP TABLE [ IF EXISTS ] 表名;
```

删除制定表，并重新创建该表

```sql
TRUNCATE TABLE 表名;
```

#### 数据类型

##### 数值类型

| 类型        | 大小   | 有符号(SIGNED)范围                                     | 无符号(UNSIGNED)范围                                       | 描述                  |
| ----------- | ------ | ------------------------------------------------------ | ---------------------------------------------------------- | --------------------- |
| TINYINT     | 1byte  | (-128，127)                                            | (0，255)                                                   | 小整 数值             |
| SMALLINT    | 2bytes | (-32768，32767)                                        | (0，65535)                                                 | 大整 数值             |
| MEDIUMINT   | 3bytes | (-8388608，8388607)                                    | (0，16777215)                                              | 大整 数值             |
| INT/INTEGER | 4bytes | (-2147483648， 2147483647)                             | (0，4294967295)                                            | 大整 数值             |
| BIGINT      | 8bytes | (-2^63，2^63-1)                                        | (0，2^64-1)                                                | 极大 整数 值          |
| FLOAT       | 4bytes | (-3.402823466 E+38， 3.402823466351 E+38)              | 0 和 (1.175494351 E- 38，3.402823466 E+38)                 | 单精 度浮 点数 值     |
| DOUBLE      | 8bytes | (-1.7976931348623157 E+308， 1.7976931348623157 E+308) | 0 和 (2.2250738585072014 E-308， 1.7976931348623157 E+308) | 双精 度浮 点数 值     |
| DECIMAL     |        | 依赖于M(精度)和D(标度) 的值                            | 依赖于M(精度)和D(标度)的 值                                | 小数 值(精 确定 点数) |

```sql
/*如:
1). 年龄字段 -- 不会出现负数, 而且人的年龄不会太大 */
age tinyint unsigned

/*2). 分数 -- 总分100分, 最多出现一位小数*/
score double(4,1)
```

##### 字符串类型

| 类型       | 大小                  | 描述                         |
| ---------- | --------------------- | ---------------------------- |
| CHAR       | 0-255 bytes           | 定长字符串(需要指定长度)     |
| VARCHAR    | 0-65535 bytes         | 变长字符串(需要指定长度)     |
| TINYBLOB   | 0-255 bytes           | 不超过255个字符的二进制数据  |
| TINYTEXT   | 0-255 bytes           | 短文本字符串                 |
| BLOB       | 0-65 535 bytes        | 二进制形式的长文本数据       |
| TEXT       | 0-65 535 bytes        | 长文本数据                   |
| MEDIUMBLOB | 0-16 777 215 bytes    | 二进制形式的中等长度文本数据 |
| MEDIUMTEXT | 0-16 777 215 bytes    | 中等长度文本数据             |
| LONGBLOB   | 0-4 294 967 295 bytes | 二进制形式的极大文本数据     |
| LONGTEXT   | 0-4 294 967 295 bytes | 极大文本数据                 |

char 与 varchar 都可以描述字符串，char是定长字符串，指定长度多长，就占用多少个字符，和字段值的长度无关，剩下的用空格补位 。而varchar是变长字符串，指定的长度为最大占用长度 。相对来说，char的性能会更高些。

```sql
/*如：
1). 用户名 username ------> 长度不定, 最长不会超过50*/
username varchar(50)

/*2). 性别 gender ---------> 存储值, 不是男,就是女*/
gender char(1)

/*3). 手机号 phone --------> 固定长度为11*/
phone char(11)
```

##### 日期时间类型

| 类型      | 大小 | 范围                                       | 格式                | 描述                     |
| --------- | ---- | ------------------------------------------ | ------------------- | ------------------------ |
| DATE      | 3    | 1000-01-01 至  9999-12-31                  | YYYY-MM-DD          | 日期值                   |
| TIME      | 3    | -838:59:59 至  838:59:59                   | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1    | 1901 至 2155                               | YYYY                | 年份值                   |
| DATETIME  | 8    | 1000-01-01 00:00:00 至 9999-12-31 23:59:59 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 4    | 1970-01-01 00:00:01 至 2038-01-19 03:14:07 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值，时间戳 |

```sql
/*如:
1). 生日字段 birthday*/
birthday date

/*2). 创建时间 createtime*/
createtime datetime
```

### DML

DML英文全称是Data Manipulation Language(数据操作语言)，用来对数据库中表的数据记录进行增、删、改操作。

- 添加数据（INSERT）
- 修改数据（UPDATE）
- 删除数据（DELETE）

#### 添加数据

- 字符串和日期型数据应该包含在引号中
- 不能爆数据类型

给指定字段添加数据

```sql
INSERT INTO 表名 (字段名1, 字段名2, ...) VALUES (值1, 值2, ...);
```

例子

```sql
insert into user(id,name,age) values(1,'Kamisato Ayaka',18)
```

给全部字段添加数据

```sql
INSERT INTO 表名 VALUES (值1, 值2, ...);
```

例子

```sql
insert into user values(2,'Ganyu',17);
```

批量添加数据

```sql
INSERT INTO 表名 (字段名1, 字段名2, ...) VALUES (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...) ;
```

```sql
INSERT INTO 表名 VALUES (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...) ;
```

例子

```sql
insert into user values(3,'Yae Miko',500),(4,'Raiden Shogun',300);
```

#### 修改数据

- 不加where对整张表修改

```sql
UPDATE 表名 SET 字段名1 = 值1 , 字段名2 = 值2 , .... [ WHERE 条件 ] ;
```

#### 删除数据

- 不加where删除整张表的数据

- 不能删除某一个字段的值（用update）

```sql
DELETE FROM 表名 [ WHERE 条件 ] ;
```

例子

```sql
delete from user where id is null;
```

### DQL

Data Query Language，数据库查询语言

关键字SELECT

#### 基本语法

按编写顺序：

```sql
SELECT 字段列表
FROM 表名列表
WHERE 条件列表
GROUP BY 分组字段列表
HAVING 分组后条件列表
ORDER BY 排序字段列表
LIMIT 分页参数
```

#### 基础查询

查询多个字段

```sql
SELECT 字段1, 字段2, 字段3 ... FROM 表名;
SELECT * FROM 表名;
```

设置别名

```sql
SELECT 字段1 [AS 别名1], 字段2 [AS 别名2] ... FROM 表名
# AS 可省略
```

去除重复记录

```sql
SELECT DISTINCT 字段列表 FROM 表名;
```

#### 条件查询

语法

```sql
SELECT 字段列表 FROM 表名 WHERE 条件列表;
```

条件

| 比较运算符          | 功能                                     |
| ------------------- | ---------------------------------------- |
| >                   | 大于                                     |
| >=                  | 大于等于                                 |
| <                   | 小于                                     |
| <=                  | 小于等于                                 |
| =                   | 等于                                     |
| <> 或 !=            | 不等于                                   |
| BETWEEN ... AND ... | 在某个范围之内(含最小、最大值)           |
| IN(...)             | 在in之后的列表中的值，多选一             |
| LIKE 占位符         | 模糊匹配(_匹配单个字符, %匹配任意个字符) |
| IS NULL             | 是NULL                                   |

| 逻辑运算符 | 功能                        |
| ---------- | --------------------------- |
| AND 或 &&  | 并且 (多个条件同时成立)     |
| OR 或 \|\| | 或者 (多个条件任意一个成立) |
| NOT 或 !   | 非 , 不是                   |

例子

```sql
select * from emp where name like '__';
# 查询名字是两个字的员工信息，每个_代表一个字符
select * from emp where idcard like '%X';
# 查询身份证结尾是X的员工信息
```

#### 聚合函数

将某一列数据作为整体进行纵向计算

null不参与计算

常见聚合函数

| 函数  | 功能     |
| ----- | -------- |
| count | 统计数量 |
| max   | 最大值   |
| min   | 最小值   |
| avg   | 平均值   |
| sum   | 求和     |

```sql
SELECT 聚合函数(字段列表) FROM 表名;
```

例子

```sql
select sum(age) as 'xxx' from emp where workaddress='西安';
```

#### 分组查询

```sql
SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件]
```

where与having区别：

执行时机不同：where是分组之前进行过滤，不满足where条件，不参与分组；而having是分组 之后对结果进行过滤。 

判断条件不同：where不能对聚合函数进行判断，而having可以。

例子

```sql
select workaddress from emp where age<45 group by workaddress having count(*)>=3;
```

#### 排序查询

ASC : 升序(默认值) 

DESC: 降序

如果是升序, 可以不指定排序方式ASC 

如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序 

```sql
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1 , 字段2 排序方式2 ;
```

例子

```sql
select * from emp order by emp.age ,entrydate desc
```

#### 分页查询

• 起始索引从0开始，起始索引 = （查询页码 - 1）* 每页显示记录数

• 分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT

• 如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10

```sql
SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询记录数;
```

例子：

```sql
select * from emp limit 10,10
```

### DCL

Data Control Language，管理数据库用户、控制数据库的访问权限

#### 用户管理

在MySQL中需要通过用户名@主机名的方式，来唯一标识一个用户。

主机名可以使用 % 通配。

这类SQL开发人员操作的比较少，主要是DBA（ Database Administrator 数据库管理员）使用。

查询用户

```sql
USE mysql;
SELECT * FROM user;
```

创建用户

```sql
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
CREATE USER '用户名'@'%' IDENTIFIED BY '密码';
#% 表示任意主机都可以访问
```

修改用户密码

```sql
ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
```

删除用户

```sql
DROP USER '用户名'@'主机名';
```

#### 权限控制

常用：

| 权限                | 说明               |
| ------------------- | ------------------ |
| ALL, ALL PRIVILEGES | 所有权限           |
| SELECT              | 查询数据           |
| INSERT              | 插入数据           |
| UPDATE              | 修改数据           |
| DELETE              | 删除数据           |
| ALTER               | 修改表             |
| DROP                | 删除数据库/表/视图 |
| CREATE              | 创建数据库/表      |

查询权限

```sql
SHOW GRANTS FOR '用户名'@'主机名';
```

授予权限

```sql
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```

撤销权限

```sql
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```

多个权限直接用逗号分隔，数据库名和表名可以用*通配

## 函数

一段可以直接被另一程序调用的程序或代码

### 字符串函数

常用的内置字符串函数

| 函数                     | 功能                                                       |
| ------------------------ | ---------------------------------------------------------- |
| CONCAT(S1,S2,...Sn)      | 字符串拼接，将S1，S2，... Sn拼接成一个字符串               |
| LOWER(str)               | 将字符串str全部转为小写                                    |
| UPPER(str)               | 将字符串str全部转为大写                                    |
| LPAD(str,n,pad)          | 左填充，用字符串pad对str的左边进行填充，达到n个字符 串长度 |
| RPAD(str,n,pad)          | 右填充，用字符串pad对str的右边进行填充，达到n个字符 串长度 |
| TRIM(str)                | 去掉字符串头部和尾部的空格                                 |
| SUBSTRING(str,start,len) | 返回从字符串str从start位置起的len个长度的字符串            |

例子

```sql
UPDATE emp SET workno=lpad(workno,5,'0')
```

### 数值函数

| 函数       | 功能                               |
| ---------- | ---------------------------------- |
| CEIL(x)    | 向上取整                           |
| FLOOR(x)   | 向下取整                           |
| MOD(x,y)   | 返回x/y的模                        |
| RAND()     | 返回0~1内的随机数                  |
| ROUND(x,y) | 求参数x的四舍五入的值，保留y位小数 |

例子

```sql
select lpad(floor(1000000*rand()),6,'0')
```

### 日期函数

| 函数                               | 功能                                              |
| ---------------------------------- | ------------------------------------------------- |
| CURDATE()                          | 返回当前日期                                      |
| CURTIME()                          | 返回当前时间                                      |
| NOW()                              | 返回当前日期和时间                                |
| YEAR(date)                         | 获取指定date的年份                                |
| MONTH(date)                        | 获取指定date的月份                                |
| DAY(date)                          | 获取指定date的日期                                |
| DATE_ADD(date, INTERVAL expr type) | 返回一个日期/时间值加上一个时间间隔expr后的时间值 |
| DATEDIFF(date1,date2)              | 返回起始时间date2 和 结束时间date1之间的天数      |

例子

```sql
select name,DATEDIFF(CURDATE(),entrydate) days from emp order by days desc
```

### 流程函数

| 函数                                                         | 功能                                                       |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| IF(value , t , f)                                            | 如果value为true，则返回t，否则返回 f                       |
| IFNULL(value1 , value2)                                      | 如果value1不为空，返回value1，否则返回value2               |
| CASE WHEN [ val1 ] THEN [res1] ... ELSE [ default ] END      | 如果val1为true，返回res1，... 否则返回default默认值        |
| CASE [ expr ] WHEN [ val1 ] THEN [res1] ... ELSE [ default ] END | 如果expr的值等于val1，返回 res1，... 否则返回default默认值 |

例子

```sql
select name,case workaddress when '北京' then '一线城市' when '上海' then '一线城市' else '二线城市' end from emp
```

## 约束

概念：约束是作用于表中字段上的规则，用于限制存储在表中的数据。 

目的：保证数据库中数据的正确、有效性和完整性。

| 约束                      | 描述                                                     | 关键字      |
| ------------------------- | -------------------------------------------------------- | ----------- |
| 非空约束                  | 限制该字段的数据不能为null                               | NOT NULL    |
| 唯一约束                  | 保证该字段的所有数据都是唯一、不重复的                   | UNIQUE      |
| 主键约束                  | 主键是一行数据的唯一标识，要求非空且唯一                 | PRIMARY KEY |
| 默认约束                  | 保存数据时，如果未指定该字段的值，则采用默认值           | DEFAULT     |
| 检查约束(8.0.16版本 之后) | 保证字段值满足某一个条件                                 | CHECK       |
| 外键约束                  | 用来让两张表的数据之间建立连接，保证数据的一致性和完整性 | FOREIGN KEY |

例子

```sql
CREATE Table test(
    id int PRIMARY KEY AUTO_INCREMENT comment 'ID唯一标识',
    name varchar(10) Not Null Unique  comment '姓名',
    age int check ( age>0&&age<=120 )  comment '年龄',
    status char(1) DEFAULT '1' comment '状态',
    gender char(1) comment '性别'
)comment '用户表';
```

### 外键约束

添加外键

```sql
CREATE TABLE 表名(
		字段名 数据类型,
		...
		[CONSTRAINT] [外键名称] FOREIGN KEY (外键字段名) REFERENCES 主表 (主表列名)
);
```

```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名) REFERENCS 主表(主表列名);
```

例子

```sql
alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references dept(id);
```

删除外键

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

删除/更新行为

| 行为        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| NO ACTION   | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不 允许删除/更新。 (与 RESTRICT 一致) 默认行为 |
| RESTRICT    | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不 允许删除/更新。 (与 NO ACTION 一致) 默认行为 |
| CASCADE     | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则 也删除/更新外键在子表中的记录。 |
| SET NULL    | 当在父表中删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表 中该外键值为null（这就要求该外键允许取null）。 |
| SET DEFAULT | 父表有变更时，子表将外键列设置成一个默认的值 (Innodb不支持)  |

```sql
ALTER TABLE 表名 主表名 (主表字段名) ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段) REFERENCES ON UPDATE 行为 ON DELETE 行为;
```

## 多表查询

### 多表关系

三种基本关系：

- 一对多
  在多的一方建立外键，指向一的一方的主键

- 多对多
  建立第三张中间表，中间表至少包含两个外键，分别关联两方主键

- 一对一
  多用于单表拆分，将一张表的基础字段放在一张表中，把详情字段放在另一张表中

  在任意一方加入外键，关联另一方主键

### 多表查询

- 连接查询
  - 内连接：相当于查询A、B交集部分数据
  - 外连接： 
    - 左外连接：查询左表所有数据，以及两张表交集部分数据
    - 右外连接：查询右表所有数据，以及两张表交集部分数据
    - 自连接：当前表与自身的连接查询，自连接必须使用表别名
- 子查询

#### 内连接

查询交集

隐式内连接

```sql
SELECT 字段列表 FROM 表1 , 表2 WHERE 条件 ...;
```

显式内连接

```sql
SELECT 字段列表 FROM 表1 [ INNER ] JOIN 表2 ON 连接条件 ...;
```

#### 外连接

左外连接

查询左表（表1）和交集

outer可以省略

```sql
SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件 ...;
```

右外连接

查询右表（表2）和交集

```sql
SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件 ...;
```

#### 自连接

```sql
SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 连接条件 ...;
```

在自连接查询中，必须要为表起别名，要不然我们不清楚所指定的条件、返回的字段，到底是哪一张表的字段。

可以内连接，也可以外链接

例子

查询员工 及其 所属领导的名字

```sql
select a.name , b.name from emp a , emp b where a.managerid = b.id;
```

#### 联合查询

对于union查询，就是把多次查询的结果合并起来，形成一个新的查询结果集。

```sql
SELECT 字段列表 FROM 表A ...
UNION [ ALL ]
SELECT 字段列表 FROM 表B ...;
```

对于联合查询的多张表的列数必须保持一致，字段类型也需要保持一致。

 union **all** 会将全部的数据直接合并在一起，union 会对合并之后的数据去重。

#### 子查询

SQL语句中嵌套SELECT语句，称为嵌套查询，又称子查询。

```sql
SELECT * FROM t1 WHERE column1= (SELECT column1 FROM t2);
```

子查询外部的语句可以是INSERT / UPDATE / DELETE / SELECT 的任何一个。

根据子查询结果不同，分为：

A. 标量子查询（子查询结果为单个值）

B. 列子查询(子查询结果为一列)

C. 行子查询(子查询结果为一行)

D. 表子查询(子查询结果为多行多列)

##### 标量子查询

子查询返回的结果是单个值（数字、字符串、日期等），最简单的形式，这种子查询称为标量子查询。

例子

```sql
select * from emp where dept_id = (select id from dept where name = '销售部');
```

```sql
select * from emp where entrydate > (select entrydate from emp where name = '方东白');
```

##### 列子查询

子查询返回的结果是一列（可以是多行），这种子查询称为列子查询。

| 操作符 | 描述                                   |
| ------ | -------------------------------------- |
| IN     | 在指定的集合范围之内，多选一           |
| NOT IN | 不在指定的集合范围之内                 |
| ANY    | 子查询返回列表中，有任意一个满足即可   |
| SOME   | 与ANY等同，使用SOME的地方都可以使用ANY |
| ALL    | 子查询返回列表的所有值都必须满足       |

例子：

查询比研发部其中任意一人工资高的员工信息

```sql
select * from emp where salary > any ( select salary from emp where dept_id = (select id from dept where name = '研发部') );
```

##### 行子查询

子查询返回的结果是一行（可以是多列），这种子查询称为行子查询。

例子

查询与 "张无忌" 的薪资及直属领导相同的员工信息 

```sql
select * from emp where (salary,managerid) = (select salary, managerid from emp where name = '张无忌');
```

##### 表子查询

子查询返回的结果是多行多列，这种子查询称为表子查询。

例子

查询入职日期是 "2006-01-01" 之后的员工信息 , 及其部门信息

```sql
select e.*, d.* from (select * from emp where entrydate > '2006-01-01') e left join dept d on e.dept_id = d.id;
```

## 事务

事务是一组操作的集合，它是一个不可分割的工作单位，事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求，即这些操作要么同时成功，要么同时失败。

### 控制事务

查看/设置事务提交方式

```sql
SELECT @@autocommit;
SET @@autocommit = 0;
```

提交事务

```sql
COMMIT;
```

回滚事务

```sql
ROLLBACK;
```

开启事务

```sql
START TRANSACTION 或 BEGIN;
```

 ### 四大特性ACID

原子性（**A**tomicity）：事务是不可分割的最小操作单元，要么全部成功，要么全部失败。

一致性（**C**onsistency）：事务完成时，必须使所有的数据都保持一致状态。

隔离性（**I**solation）：数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立 环境下运行。

持久性（**D**urability）：事务一旦提交或回滚，它对数据库中的数据的改变就是永久的。

### 并发事务问题

赃读：一个事务读到另外一个事务还没有提交的数据。

![赃读](https://s2.loli.net/2024/02/07/tN7YfEdxRmUlTVX.png)

不可重复读：一个事务先后读取同一条记录，但两次读取的数据不同，称之为不可重复读。

![不可重复读](https://s2.loli.net/2024/02/07/mE2oMhxckNPRbdp.png)

幻读：一个事务按照条件查询数据时，没有对应的数据行，但是在插入数据时，又发现这行数据已经存在，好像出现了 "幻影"。

![幻读](https://s2.loli.net/2024/02/07/wclKrdmQ4Fu5Jnh.png)

### 事务隔离级别

为了解决并发事务所引发的问题，在数据库中引入了事务隔离级别。主要有以下几种：

| 隔离级别              | 脏读 | 不可重复读 | 幻读 |
| --------------------- | ---- | ---------- | ---- |
| Read uncommitted      | √    | √          | √    |
| Read committed        | ×    | √          | √    |
| Repeatable Read(默认) | ×    | ×          | √    |
| Serializable          | ×    | ×          | ×    |

查看事务隔离级别

```sql
SELECT @@TRANSACTION_ISOLATION;
```

设置事务隔离级别

```sql
SET [ SESSION | GLOBAL ] TRANSACTION ISOLATION LEVEL { READ UNCOMMITTED |READ COMMITTED | REPEATABLE READ | SERIALIZABLE } 
```



<center>基础篇完结撒花！！！</center>
