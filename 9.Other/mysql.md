



## mysql安装

1. 官网下载MSI安装包（32位和64位是同一个，选400多M的别选web-community ）
2. 自定义安装路径和data路径
3. 安装完后，右键点击“我的电脑”－“属性”－“高级”－“环境变量”－“系统变量”－双击“Path”－将mysql的路径“D:\Program Files\MySQL\MySQL Server 8.0\bin”添加进去 
4. 在命令窗口 输入mysql -u root -p 验证



## 终端操作

- 登录：mysql -u root -p

- 查询所有数据库：show databases;
- 选中某个数据库：use 数据库名;
- 退出数据库：exit;
- 创建数据库：create database test;
- 查看数据库里的数据表：show tables;
- 创建数据表：create table pet(name VARCHAR(20), ...)
- 查看数据表结构：describe pet;
- 查看表中的记录：select * from pet;
- 往数据表中添加记录：insert into pet  ->VALUES ('xx','xxx'...)
- 删除数据：delete from pet where name='xxx';
- 修改数据：update pet set name='新xxx' where owner='xxx';

## 常用数据类型

#### 数值

| 类型         | 大小                                     | 范围（有符号）                                               | 范围（无符号）                                               | 用途            |
| :----------- | :--------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------- |
| TINYINT      | 1 字节                                   | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
| SMALLINT     | 2 字节                                   | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
| MEDIUMINT    | 3 字节                                   | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
| INT或INTEGER | 4 字节                                   | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
| BIGINT       | 8 字节                                   | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
| FLOAT        | 4 字节                                   | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
| DOUBLE       | 8 字节                                   | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |

#### 日期/时间

| 类型      | 大小 (字节) | 范围                                                         | 格式                | 用途                     |
| :-------- | :---------- | :----------------------------------------------------------- | :------------------ | :----------------------- |
| DATE      | 3           | 1000-01-01/9999-12-31                                        | YYYY-MM-DD          | 日期值                   |
| TIME      | 3           | '-838:59:59'/'838:59:59'                                     | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1           | 1901/2155                                                    | YYYY                | 年份值                   |
| DATETIME  | 8           | 1000-01-01 00:00:00/9999-12-31 23:59:59                      | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 4           | 1970-01-01 00:00:00/2038结束时间是第 **2147483647** 秒，北京时间 **2038-1-19 11:14:07**，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYYMMDD HHMMSS     | 混合日期和时间值，时间戳 |

#### 字符串

| 类型       | 大小                | 用途                            |
| :--------- | :------------------ | :------------------------------ |
| CHAR       | 0-255字节           | 定长字符串                      |
| VARCHAR    | 0-65535 字节        | 变长字符串                      |
| TINYBLOB   | 0-255字节           | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255字节           | 短文本字符串                    |
| BLOB       | 0-65 535字节        | 二进制形式的长文本数据          |
| TEXT       | 0-65 535字节        | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215字节    | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215字节    | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967 295字节 | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967 295字节 | 极大文本数据                    |

## 建表约束

- 主键约束：通过给某个字段添加约束使得该字段不重复且不为空

  ```
  create table user(
  	id int primary key,		//id重复或为空会报错
  	name varchar(20)
  );
  ```

  ```
  create table user(
  	id int,
  	name varchar(20),
  	primary key(id,name)	//为id和name都添加约束，***联合主键值加起来不重复就可以***
  );
  ```

- 自增约束：让某个字段自增长，可不用传值

  ```
  create table user(
  	id int primary key auto_increment,		//id可不传且会自增长
  	name varchar(20)
  );
  ```

  建表后添加约束：

  ```
  alter table user add primary key(id);
  ```

  删除约束：

  ```
  alter table user drop primary key;
  ```

  修改字段来添加约束：

  ```
  alter table user modify id int primary key;
  ```

- 唯一约束：约束修饰的字段的值不可以重复

  ```
  create table user(
  	id int,
  	name varchar(20),
  	unique(name)
  );
  ```

  建表后添加约束：

  ```
  alter table user add unique(name);
  ```

  删除约束：

  ```
  alter table user drop index name;
  ```

  修改字段来添加约束：

  ```
  alter table user modify name varchar(20) unique;
  ```

- 非空约束：修饰的字段不能为空

  ```
  create table user(
  	id int,
  	name varchar(20) not null
  );
  ```

- 默认约束：当没有传值时使用默认值

  ```
  create table user(
  	id int,
  	name varchar(20),
  	age int default 10
  );
  ```

- 外键约束：一个表中的字段被另一个表引用

## 设计范式

