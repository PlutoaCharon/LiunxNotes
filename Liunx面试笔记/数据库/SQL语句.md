## SQL语句

### 增

#### 增创建用户：

```mysql
mysql>create user test@‘%’ identified by ‘123456’;
```

#### 创建数据库：

```mysql
mysql>create database web;
```

#### 创建数据表：

```mysql
mysql>create table a1 (id int ,name char(30));
```

#### 插入数据：

```mysql
mysql>insert into a2 (id,name,age) values (1,‘zhangsan’,21)；
```

### 删

#### 删除用户：

```mysql
mysql>drop user test@’%’;
```

#### 删除数据库：

```mysql
mysql>drop database web;
```

#### 删除数据表：

```mysql
mysql>drop table a1;
```

#### 删除数据：

```mysql
mysql>delete from a2 where id=5;

mysql>delete from a2 where age between 23 and 25;
```

### 改

#### 修改表中的数据：

```mysql
mysql>update a2 set age=21 where id=3;
```

#### 修改数据表的名称：

```mysql
mysql>alter table a2 rename a1;
```



#### 修改数据表的字段类型：

```mysql
mysql>describe a1;

mysql>alter table a1 modify name char(50);

mysql>describe a1;
```

#### 修改数据表的字段类型：

```mysql
mysql>alter table a1 change name username char(50) not null default ‘’;

mysql>describe a1;
```

#### 添加删除字段

```mysql
mysql>alter table a1 add time datetime;

mysql>alter table a1 drop time;
```

### 查

#### 查看所有数据库：

```mysql
mysql>show databases;
```

#### 查看指定库内所有数据表：

```mysql
mysql>show tables;
```

#### 查看指定数据表的字段结构：

```mysql
mysql>describe a1;
```

#### 查看所有MySQL用户密码及登录方式：

```mysql
mysql>select User,Password,Host from mysql.user;
```

### 授权

#### 授予用户全部权限：

```mysql
mysql>grant all on aa.a1 to test@‘%’；#给已存在用户授权

mysql>grant all on aa.a1 to abc@‘%’ identified by ‘123456’；#创建用户并授权
```

#### 取消abc用户的删除库、表、表中数据的权限：

```mysql
mysql>revoke drop,delete on aa.a1 from abc@‘%’；#取消删除权限（登录abc测试）

mysql>show grants for abc@‘%’；#查看指定用户的授权

mysql>show grants for test@‘%’；
```

### 启动关闭

#### 启动：

```mysql
service mysqld start

/etc/init.d/mysqld start

mysqld_safe &
```



#### 关闭：

```mysql
service mysqld stop

/etc/init.d/mysqld stop

mysqladmin -uroot -p123456 shutdown
```

