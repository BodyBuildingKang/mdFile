# 安装

##  [下载MySQL](https://downloads.mysql.com/archives/community/)

1. 注意 下载编译好的包(ps 下载源码需要编译)

##  把下载的MySQL传到inux服务器上面

##  解压上传的tar.gz

1. tar -zxvf 【下载的包名】

## 把解压的文件移动到/usr/local目录下面

1. mv 【解压的包名】 /usr/local/mysql

## 添加MySQL组和用户(默认会添加，没有添加就自己添加)

cd /usr/local/mysql
chown -R mysql:mysql ./

## mysql初始化操作,记录下临时密码,之后第一次登录的时候会用
到。

./mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data

密码 fVdpg:bM9pAk

## 创建MySQL配置文件/etc/my.cnf



[mysqld]
port=3306
basedir=/usr/local/mysql
datadir=/usr/local/mysql/data
max_connections=200
max_connect_errors=10
character-set-server = UTF8MB4
default-storage-engine=INNODB
default_authentication_plugin=mysql_native_password
[mysql]
default-character-set=utf8mb4
[client]
port=3306
default-character-set=utf8mb4

## 启动MySQL服务

cd /usr/local/mysql/support-files

./mysql.server start

## 通过临时密码登录MYSQL并修改密码

./mysql -u root -p密码
alter user 'root'@'localhost' identified by '123';

## 开启远程访问

CREATE USER 'root'@'%' IDENTIFIED BY '123'; -- 这一步执行失败没关系
GRANT ALL ON *.* TO 'root'@'%';
flush privileges;

# 问题

## 1. 通过ip连接不上的问题 1066

1. 重启了虚拟机需要重新启动mysql服务
2. 需要开启远程访问
3. [需要关闭防火墙](https://zifeng.blog.csdn.net/article/details/108041744?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-3.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-3.control)
4.  。。todo