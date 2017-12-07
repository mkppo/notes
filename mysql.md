# Centos7下安装mysql5.7

### 下载mysql源

``` bash
[root@localhost ~]# wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
```

### 安装mysql源

``` bash
[root@localhost ~]# yum -y localinstall mysql57-community-release-el7-11.noarch.rpm 
```

### 在线安装mysql

``` bash
[root@localhost ~]# -y install mysql-community-server
```

### 启动mysql服务

``` bash
[root@localhost ~]# systemctl start mysqld
```

### 设置开机启动

``` bash
[root@localhost ~]# systemctl enable mysqld
[root@localhost ~]# systemctl daemon-reload
```

### 修改root本地登录密码

mysql安装完成后，在 /var/log/mysqld.log 文件中会生成一个默认密码
``` bash
[root@localhost ~]# vi /var/log/mysqld.log

A temporary password is generated for root@localhost: t5yZjoGr2E?Q
```

``` bash
[root@localhost ~]# mysql -u root -p 
Enter password t5yZjoGr2E?Q

# 修改密码 必须是大小写字母数字特殊字母的组合，至少8位
ALTER USER 'root'@'localhost' IDENTIFIED BY 'xxx'
```

### 设置允许远程登录

``` bash
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'xxx' WITH GRANT OPTION;
```

### 配置默认编码

修改 /etc/my.cnf 配置文件，在[mysqld]下添加编码配置

``` bash
character_set_server=utf8
init_connect='SET NAMES utf8'
```

重启服务

``` bash
[root@localhost ~]# systemctl restart mysqld
```
