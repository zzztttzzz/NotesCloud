# MySQL Learn

## What is MySQL

* 关系型数据库，relational database。例如，某个产品是依赖于产品列表，并且有多个标签，所以称之为关系型。
* SQL(Structured Query Language)



## 安装配置

* 官网下载.msi文件安装

* 最后配置一个环境变量即可

* 终端输入: 

  ```dos
  mysql -u root -p 
  ```

  实现登录

* `show databases`展示所有databases

##  基本命令

* 创建数据库：

  ```sql
  create database test;
  ```

  使用数据库：

  ```sql
  use test;
  ```

  创建数据表：

  ```sql
  CREATE TABLE pet(
  name VARCHAR(20),
  owner VARCHAR(20),
  species VARCHAR(20),
  sex CHAR(1),
  birth DATE,
  death DATE);
  )
  ```

  查看数据表的信息：

  ```sql
  describe pet;
  ```

  插入：

  ```
  INSERT INTO......
  ```

* create的时候相当于是创建了数据表中的列名称，含有各种属性，每insert一条，相当于每一行是一个数据样本，列数表示该样本的属性特征，列数要和先前create的变量维度要统一。

## 常用数据类型

* 数值
* 日期时间
* 字符串

* 使用的时候再选择合适的数据格式



## 删除修改数据

* 从数据表中删除一行数据：

  ```sql
  DELETE FROM pet WHERE name='VarName';
  ```

* 修改：

  ```sql
  UPDATE pet SET name='VarName1' WHERE owner='owenerVarname1'
  ```



## mySQL建表约束

* **主键**(primary key)约束：唯一性，**不重复且不为空**。创建数据表的时候，在变量名后面添加`primary key`即可，例如：

  ```sql
  create table test_primary(
  -> id int primary key, name varchar(20), birthday date);
  ```

  这样对于变量id只能插入唯一一个元素，并且不能为空。

* 联合主键，如果有多个主键，则两个主键不完全相同就可以。

* **自增约束**：auto_increment。插入的时候，指定插入的数据维数即可。

  ```sql
  insert into test4(name, password) values('name1', 'password1');
  ```

* 如果创建表的时候忘记添加主键约束，可以增加主键约束，通过代码：

  ```sql
  alter table user4 add primary key(id);
  ```

  还可以删除主键约束， 代码：

  ```sql
  alter table user4 drop primary key;  -- 此处必须全部drop
  ```

  可以使用`modify`字段修改主键的属性：

  ```sql
  alter table user4 modify id int primary key;
  ```

* **唯一约束**，如果在表中已经有了一个该属性的值，则无法insert。区别于主键的区别在于，唯一可以为空，并且NULL可以重复。

  ```
  alter table user4 add unique(name);
  ```

* 使用`alter table`命令，后面的`add`, `modify`, `drop`使用的格式不同。`add`后跟键属性，`drop`后同样跟键属性，加了`drop index`后，可以加变量，例如`drop index name`，可以将`name`的属性删除。而`modify`类似于`create table`时的操作，后跟变量名，数据类型名以及键属性。

* **非空约束**：顾名思义，变量的值不能为空。

  ```sql
  alter table user4 modify password varchar(20) not null;
  ```

  如果不添加后面的默认约束，则无法执行以下语句：

  ```sql
  insert into user4(id) values(29);
  ```

  因为默认的值都是NULL，与非空约束冲突。

* **默认约束**：添加默认值，插入的时候没有指定会插入默认值，不指定则都为NULL。

  ```sql
  create table user5(id int primary key, name varchar(20), age int default 100);
  ```

* **外键约束**：
  涉及两个表，父表和子表。语法：

  ```sql
  create table classes(id int primary key, classname varchar(20) unique);
  create table students(id int primary key, name varchar(20), class varchar(20), foreign key(class) references classes(className);
  ```

  子表的外键约束至少是个unique，而且数据类型需要一致，都为字符串数值或者时间。

  外键约束的作用有两个，主表中没有的副表不能插入，而且主表中被引用的数据无法被删除。



