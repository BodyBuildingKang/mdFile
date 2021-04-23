#  数据库的基本操作（数据库；db  表 tb）

1. create database db;
2. alter database db default character set utf8 collate utf8_general_ci;  ## 设置编码格式
3. show databases;
4. show create database db;
5. use db;
6. create table tb;
7. drop database if exists db;
8. drop table if exists tb;

# 约束

1. not null
2. unsigned                     ##  插入数字不能赋值
3. primary key                ## 值唯一
4. auto increment          ## 只能用于整型的主键列
5. default
6. comment                     ## 注释 

```sql
create table tb(
    tb_id integer(10) auto_increment primary key comment '测试描述' ,
    tb_name varchar(30) not null,
    tb_pwd varchar(20) not null default '123'
);
```

#  常用类型

1. 极小整型 tinyint 
   1. 非负最大值255
   2. 1个字节
2. 小整型samllint
   1. 非负最大值6535
   2. 2个字节
3. 整型int
   1. 非负最大值4294967295
   2. 4个字节
4. 长整型long
5. 单精度
   1. float  -------- 4 个字节
   2. deciaml(6,3)
6. 定长字符串char
   1. 最大保存255个字符
   2. 如果值没有给定长度用空格补充
7. 变长字符串varchar
   1. 最大保存255
   2. 用多大占多大
8. 文本text --------最大保存65535个字节
9. 日期
   1. Date
   2. DateTime
   3. TimeStamp







