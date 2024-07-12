# mysql

## 创建表

```mysql
create table if not exists student(
id int auto_increment primary key comment '主键id',
name varchar(30) not null comment '学生姓名',
phone varchar(20) comment '电话号码',
address varchar(100) default '暂时未知' comment '住址' 
)engine=innodb;
```



##  查看表的结构

````mysql
desc 表名
````



## 删除表

````mysql
drop table if exists 表名1，表名2;
````



# 修改表

## 添加字段：

````mysql
alter table 表名 add 字段名 type(num);
````

### `指定位置：`

````mysql
alter table 表名 add 字段名1 type(num) after 字段名2;
alter table 表名 add 字段名1 type(num) first;
````



## 删除字段：

````mysql
alter table 表名 drop 字段名;
````



## 修改字段名称，类型：

````mysql
alter table 表名 change 字段名1  字段名3 type(num);
alter table 表名 modify 字段名1   type(num);
````



## 修改表名：

```mysql
alter table 表名1 rename to 表名2;
```







## 插入数据

````mysql
insert into 表名 (字段1,字段2,字段3,........字段n) values(值1,值2,值3,......,值n);
//注意字段与值一一对应
insert into 表名(按照表的字段默认顺序时可省略) values (值1,值2,值3,......,值n);
insert into 表名 values (NULL,值2,default,......,值n);
主键是自增的，写NULL默认往下排
如果字段有默认值，写dafault 会显示默认值
````



## 查看数据

`````mysql
select * from 表名;
`````



## 一次插入多条数据

````mysql
insert into 表名(按照表的字段默认顺序时可省略) values (值1,值2,值3,......,值n),(值1,值2,值3,......,值n)
````









# 查询表（基本）

````mysql
select * from 表名;
select 字段1,字段2,... from 表名;
````





# 更新数据



````mysql
update 表名 set 要修改的字段=.... where  限制条件
update teacher set name='frank' where id=1;
update teacher set name='tom' ,address='shanghai'where phone='22222' or phone='1111';
````



##  删除数据



````mysql
delete from 表名 where 条件;
delete from  teacher where id=2;
delete from  teacher where age>30;

delete from teacher;全部删除（遍历，性能慢）下次插入数据时，自增主键id会继续往下排，不会从1开始
清空表
truncate table 表名;
旧表直接报废，如上id从1开始
````

# 字符集编码问题

```mysql
显示字符编码

show variables like 'character_set_%';

修改字符编码
set character_set_client=gbk;
（其他类似，根据variable_name 写即可）
```





# 数据库数据类型

## int类型

## float类型：

会出现精度丢失

## decimal类型（定点数）：

不会精度丢失

````mysql
create table bank(
money decimal(20,19)
);
````



字符串类型与文本类型

## char 定长字符串

## varchar 变长字符串

## 布尔类型

boolean



枚举类型：

## enum

````mysql
create table sex(
gender enum('man','woman','?','it','nothing')
);
````

man-->1

woman-->2

....(插入数据时也可以直接插入1，2，3，4，5)



## set类型

````mysql
create table t_1(
hobby set('哲学','经济','文学','IT','数学')
);

插入
insert into t_1 values('IT,数学');
````



## 时间和日期类型

datetime 





# Primary key 含义以及企业用途

## 主键

唯一型且能确定数据的存在，必须含有主键

不能重复，不能为空

可能会被其他表引用

````mysql
alter table 表名 add primary key (字段);
alter table 表名 drop primary key (字段);
````



## 唯一键

保证数据没重复,可以为空

只在当前表作用

````mysql
alter table 表名 add unique(字段);
alter table 表名 drop unique index 字段;
````





## 外键

学生表(主表)

| stuId | 姓名 |
| ----- | ---- |
| 1     | 张三 |
| 2     | 李四 |
| 3     | 王五 |

食堂订单表（从表）

| id   | stuId | money |
| ---- | ----- | ----- |
| 111  | 2     | 13.5  |
| 112  | 3     | 17    |
| 113  | 1     | 14    |

````mysql
create table stu(
stuId int(4) primary key,
name varchar(20)
);
````

````mysql
create table eatery(
id int(4) primary key,
money decimal(10,4),
stuId int(4),
foreign key (stuId) references stu(stuId)
);
````



###  创建表时创建外键

````mysql
 foreign key (字段) references 主表名(字段)
````

### 更新外键

````mysql
alter table 表名 add  foreign key (字段) references 主表名(字段);
````

### 删除外键

````mysql
show create table 表名;
#找到外键名称
alter table 表名 drop foreign key 外键名;
````





## 外键的操作

### 置空，级联

删除时一般置空，更新时一般级联

````mysql
create table eatery(
id int(4) primary key,
money decimal(10,4),
stuId int(4),
foreign key (stuId) references stu(stuId) on delete set null on update  cascade
);
````



# 查询语句

## 单表查询

select,from,dual,where, in,between...and,is null

```mysql
select 2*7 from dual ;
```

dual 虚拟的表， 伪表

![](F:\Photos\snipaste\mysql\Snipaste_2024-03-16_14-02-03.png)

```mysql
select * from t3 where address='beijing' or address='shanghai'; 
```

![](F:\Photos\snipaste\mysql\Snipaste_2024-03-16_14-10-06.png)

```mysql
select * from t3 where address in ('beijing','shenzhen'); 
```

![](F:\Photos\snipaste\mysql\Snipaste_2024-03-16_14-10-40.png)

### 聚合函数

sum,avg,max,min,count





### like模糊查询

````mysql
select * from 表名 where 字段 like '%'
select * from student where name like '张%'
select * from student where name like '张_'
````

%代表一个或多个字符

_代表一个字符





### group by 分组查询

````mysql
select avg(age) as age,address as address from info group by address;
````

![](F:\Photos\snipaste\mysql\group by.png)

### group_concat查询

````mysql
select group_concat(id),address from info group by address;
````

![](F:\Photos\snipaste\mysql\group_concat.png)



### having

````mysql
select 字段 as 别名,字段 as 别名 from 表名 group by 字段 having 条件;
select avg(age) as age,address as address from info group by address having age>20;
````

![](F:\Photos\snipaste\mysql\having.png)

### limit 

````mysql
select *from 表名 limit x,y;
从x开始查询往后y个长度的数据
select *from 表名 limit y;
省去第一个数字，默认从开头查询
````

### distinct ,all

````mysql
select distinct 字段 from 表名;
select all 字段 from 表名;
````

![image-20230527110725567](C:\Users\magicman\AppData\Roaming\Typora\typora-user-images\image-20230527110725567.png)

![image-20230527110742482](C:\Users\magicman\AppData\Roaming\Typora\typora-user-images\image-20230527110742482.png)

distinct 去重 可搭配 聚合函数count 使用

all不写出来时作用一样 ==select 字段 from 表名;





## 多表查询

### union联合查询

````mysql
select  字段1,字段2 from 表名1 union select 字段1,字段2 from 表名2
select  字段1,字段2 from 表名1 union distinct select 字段1,字段2 from 表名2//去重
````





### inner join

````mysql
select 字段1,字段2 from 表名1 inner join  表名2  on 表名1.公共字段1=表名2.公共字段1
````

//内连接 需要有一个公共字段

![](F:\Photos\snipaste\mysql\inner join.png)

### left join 

````mysql
select 字段1,字段2 from 表名1 left join  表名2 on 表名1.公共字段1=表名2.公共字段1
````

//以左表为基准（即表1）

### right join 

### cross join 

````mysql
select *from 表名1 cross join 表名3// 返回一个笛卡儿积
````

### natural join



 多表查询一般写全，用inner join 查询

全外连接

mysql 没有全外连接的关键词，但是可以使用 union 联合左外连接和右外连接 实现





## 子查询

````mysql
select *from 表名1 where 字段in(select 字段 from 表名2 where 条件)
select *from student where id in (select stuid from score where score >85)
````

in ,not in 

exists ,not exists

# 高级部分

## 视图

隐藏敏感信息,限定查看数据

![](F:\Photos\snipaste\mysql\view 创建.png)

视图算法

temptable   merge

![](F:\Photos\snipaste\mysql\视图算法.png)

## 事务

![](F:\Photos\snipaste\mysql\事务.png)

rollback 回滚

savepoint

![](F:\Photos\snipaste\mysql\回滚点.png)

![](F:\Photos\snipaste\mysql\savepoint.png)

事物的特点

ACID

atomicity 原子性

consistency 一致性

isolation 隔离性

durability 持久性



## 索引

index

方便查询 

```mysql
create index balance_index on wallet(balance);

create unique index balance_index on t2(score1); 
```

![](F:\Photos\snipaste\mysql\索引.png)



# 规范

## 常用

1表示判断的字段名  前缀is_ 开头 类型 unsigned tinyint 长度 1

2字段名不能出现大写

3表名不能出现mysql 的关键字 select ,table

4索引命名规范 

主键索引 pk_

唯一键索引uk_

非唯一键索引idx_

5小数用decimal 禁止使用float double

6字符串字符很少，使用char  字符超过5000 用 text

7表中必须存在三个字段id, create_time, update_time

id 类型 无符号bigint  若为单表时， 设为自动递增  

create_time, update_time 类型为datetime 

## 索引规范

8具有唯一特性的字段需要有唯一索引

9多表查询时 只可2个表join 不可以3，4  而且join的字段类型必须一致 关联字段需要有索引

10在varchar 建立索引，需要指定索引长度，不必全文段索引

## SQL规范

11count(*)无可替代，会统计 NULL 的字段

12如果某一列值全为NULL 需要注意count

13 is null 判断为空  ISNULL() 判断表达式为空

14不要使用外键和级联 (尤其在高并发)

15开发过程 不允许使用存储过程

16删除 更新时，先select 查出数据 再修改

17子查询in 尽量避免

18 utf-8 作为编码



# 思考

## flush与commit的区别

在 MySQL 中，事务的实现确实包括将命令的结果写入到内存中的缓冲区（buffer）中，然后通过 FLUSH 或者 COMMIT 将缓冲区中的数据写入到硬盘中。因此，从这个角度来说，FLUSH 和 COMMIT 在某种程度上确实有一定的相似之处，都涉及到将数据持久化到磁盘中。

然而，它们的作用和使用场景仍然有一些不同：

    FLUSH：
        FLUSH 主要用于刷新服务器的状态和资源，例如刷新表、权限等信息，以保持数据库的一致性和稳定性。
        在事务中使用 FLUSH 并不会提交事务，它只是刷新了服务器的状态，而不会将事务中的操作持久化到磁盘中。
    
    COMMIT：
        COMMIT 用于提交当前事务中的所有操作，将事务中的修改永久性地保存到数据库中。
        在事务中使用 COMMIT 是将事务中的操作真正地写入到数据库的磁盘文件中，以确保数据的一致性和持久性。

因此，尽管两者都涉及到将数据写入到硬盘中，但它们的作用和使用场景仍然有所区别。FLUSH 更多地用于管理服务器的状态和资源，而 COMMIT 则用于事务的提交，将数据持久化到数据库中。
