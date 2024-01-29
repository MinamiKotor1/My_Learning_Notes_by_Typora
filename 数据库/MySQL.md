### 4.2 mysql基础指令

```sql
# mysql外
mysql -u root -p # 登录

# mysql内
set password = password('123456'); # 更改密码
```

### 6.1 数据库管理

```sql
show databases; # 显示当前所有数据库
create database demo1; # 创建数据库（文件夹）
create database demo1 DEFAULT CHARSET utf8 COLLATE utf8_general_ci; # 指定utf-8
drop database demo1; # 删除数据库
use demo1; # 进入数据库
show tables; # 查看所有表
create table table_1 (
    id int auto_increment primary key, # 主键（不为空且唯一值）
    # auto_increment 自增
    name varchar(16) not null, # 不允许为空
    age int default 3 # 默认3
) default charset=utf8; # 创建表
desc table_1; # 显示表设置信息
drop table_1; # 删除表
```

### 6.2 常用数据类型

+ tinyint
  
  有符号 -128~127
  
  无符号 0~255

+ int

+ bigint

+ decimal(d,m) 
  
  d表示总位数，最大值65；m表示小数点后位数，最大值30

+ char(n)
  
  定长字符串，n表示字符个数

+ varchar(n)
  
  变长字符串

+ text
  
  变长大字符串，最多65535个

+ mediumtext
  
  2^24

+ longtext
  
  2^32

+ datetime
  
  年月日时分秒

+ date
  
  年月日

### 6.3 数据行管理

```sql
# 插入数据
insert into table_1(id,name,age) values (1,"zhangsan",23),(2,"lisi",88);
# 删除数据
delete from table_1;
delete from table_1 where id=4;
```
