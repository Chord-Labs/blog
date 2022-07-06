Centos 安装Mysql 8.0 详细教程

### 1.下载正确的tar包
主页：https://www.oracle.com/mysql/index.html  
下载主页面：https://www.mysql.com/downloads/  
社区资源下载页面：https://dev.mysql.com/downloads/  
MySQL社区版下载页面：https://dev.mysql.com/downloads/mysql/  


### 2.MySQL社区相关产品介绍  
MySQL Community Server  
  最流行的开源数据库管理软件，当前最新版本是8  
MySQL Cluster  
  基于MySQL数据库而实现的集群服务，自身能提供高并发高负载等特性  
MySQL Fabric  
  MySQL官方提供的关于MySQL数据库高可用和数据分片的解决方案  
MySQL Connectors  
  为应用程序提供JDBC/ODBC等访问MySQL数据库的接口服务  
  
### 3.上传tar包到服务器并解压

```Bash
wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.29-linux-glibc2.12-x86_64.tar.xz
cp mysql-8.0.20-linux-glibc2.12-x86_64.tar.xz /usr/local
cd /usr/local/
tar -xvf mysql-8.0.20-linux-glibc2.12-x86_64.tar.xz
tar -zxvf mysql-8.0.20-linux-glibc2.12-x86_64.tar.gz
mv mysql-8.0.20-linux-glibc2.12-x86_64 mysql
```
查看空间占用
```
du -h --max-depth=1
```
### 4.创建运行MySQL的用户和组

```
groupadd mysql
useradd mysql -g mysql
```

### 5.创建MySQL数据目录
```
mkdir data
chown mysql:mysql data
```

### 6.初始化MySQL
在myslq目录下执行如下命令
```
##初始化数据目录
[root@ mysql]# bin/mysqld --initialize --user=mysql --datadir /usr/local/mysql/data

#bin/mysqld_safe --datadir=/usr/local/mysql/data --user=mysql & 		##启动MySQL服务
#cp support-files/mysql.server /etc/init.d/mysql.server 		##将MySQL加入到服务自启动
```

### 7.启动MySQL
```
##将默认启动文件复制到指定目录
[root@old support-files]# cp mysql.server /etc/init.d/
#需要判断当前镜像是否安装的有mariadb执行卸载
rpm -e --nodeps  mariadb-libs
rm -rf /etc/my.cnf
##通过服务启动MySQL
/etc/init.d/mysql.server start
/etc/init.d/mysql.server stop
```
查看启动进程：
```
ps -ef|grep mysql
```
查看监听端口
```
netstat -an|grep LISTEN
```
将mysql命令添加到系统环境变量
```
vim .bash_profile
PATH=$PATH:$HOME/bin:/usr/local/mysql/bin
source .bash_profile
```

### 8.连接MySQL

```
mysql -u root -p
```
修改超级管理用户密码
```
5.7
set password=password('mysql');
8.0版本需要这种方式更新用户密码
alter user user() identified by 'mysql';
```
创建新用户并授权

```
create user 'XXX'@'%' identified by 'XXX';

all privileges 全部权限
select 查询权限
select,insert,update,delete 增删改查权限
select,[…]增…等权限

grant all privileges on *.* to 'XXX'@'%' with grant option;
```
### 9.MySQL错误解决

```
启动过程中如果碰到如下错误
[root@localhost mysql]# bin/mysqld --initialize --user=mysql --datadir /usr/local/mysql/data
bin/mysqld: error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory
则需要安装包
yum install -y libaio
```
