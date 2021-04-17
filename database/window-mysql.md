





1. [下载mysql](https://downloads.mysql.com/archives/community/)
2. 解压并配置MySQL环境变量
3. 在解压根目录创建my.ini配置文件

```
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
basedir=D:\DB\mysql-8.0.22-winx64
# 设置mysql数据库的数据的存放目录
datadir=D:\DB\mysql-8.0.22-winx64/data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server = UTF8MB4
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8mb4
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8mb4
```

4. 安装mysqld

```
mysqld -install
```

5. 启动mysql服务

```
net start mysql
```

6. 初始化mysql

```
mysqld --defaults-file=D:\DB\mysql-8.0.22-winx64\my.ini --initialize –-console
```

注意：  初始化过程时会生成初始密码，要记录下来 密码类似：-T?a0&,_yIi1

7. 登陆mysql以及更改初始密码

```
mysql -u root -p
Ener password:-T?a0&,_yIi1
alter user root@localhost identified by '199515';  // 修改初始密码
```

8. 开启远程访问

```
CREATE USER 'root'@'%' IDENTIFIED BY '199515'; --这一步执行失败没关系
GRANT ALL ON *.* TO 'root'@'%';
flush privileges;
```

9. 打开数据库进行连接



ps :

使用上面方式无法登陆的解决方案

1、停止mysql8 net stop mysql

2、无密码启动mysqld --console --skip-grant-tables --shared-memory

3、前面窗口不能关闭，在开启列外一个新窗口进行无密码登陆mysql -u root -p

4、清空密码update mysql.user set authentication_string='' where user='root' and host='localhost'