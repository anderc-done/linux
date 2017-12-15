# Centos7安装mysql-5.7 + JAVA1.8+ tomcat8
## 安装mysql-5.7
* 下载mysql-5.7

[mysql-5.7下载地址](https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.20-1.el7.x86_64.rpm-bundle.tar)
下载 mysql-5.7.20-1.el7.x86_64.rpm-bundle.tar

下载后上传到服务器

或者在终端输入

```shell
wget https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.20-1.el7.x86_64.rpm-bundle.tar
```
* 解压rpm包

```shell
tar xf mysql-5.7.20-1.el7.x86_64.rpm-bundle.tar 
```
* 清除原有的安装包和yum源

```shell
rpm -qa |grep mariadb
```
> mariadb-libs-5.5.50-1.el7_2.x86_64

```shell
rpm -e --nodeps mariadb-libs-5.5.50-1.el7_2.x86_64
```
* 添加用户

```shell
useradd -s /sbin/nologin mysql
```
* 安装mysql

```shell
rpm -ivh mysql-community-common-5.7.20-1.el7.x86_64.rpm 
rpm -ivh mysql-community-libs-5.7.20-1.el7.x86_64.rpm
rpm -ivh mysql-community-devel-5.7.20-1.el7.x86_64.rpm
rpm -ivh mysql-community-client-5.7.20-1.el7.x86_64.rpm
rpm -ivh mysql-community-libs-compat-5.7.20-1.el7.x86_64.rpm
# 解决mysql-server依赖关系
yum -y install numactl-libs
rpm -ivh mysql-community-server-5.7.20-1.el7.x86_64.rpm
```
5.7中已经自动生成了/etc/my.cnf文件

* 初始化mysql

```shell
cd /usr/bin/
mysqld --initialize --user=mysql
systemctl start mysqld
```

* 查看mysql的root密码

```shell
cat /var/log/mysqld.log |grep pass
```

* 安全初始化

```shell
mysql_secure_installation
```
输入root密码后输入新密码，新密码要求长度应该大于8位，然后全部输入‘y’

* 登录mysql数据库

```shell
mysql -uroot -p
```
> mysql> select version();
> 
> +-----------+
> 
> | version() |
> 
> +-----------+
> 
> | 5.7.20    |
> 
> +-----------+
> 
> 1 row in set (0.00 sec)

## yum安装jdk

* 更新系统

```shell
yum -y update
```
* 查找可用的jdk

```shell
yum list java*
```

* 安装java1.8

```shell
yum -y install java-1.8.0-openjdk*
```
此时JAVA_HOME的环境变量值是：

JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.151-1.b12.el7_4.x86_64

此变量值后面要用到
## 安装apache-tomcat
* 创建用户组和用户

```shell
groupadd tomcat
useradd -s /bin/bash -g tomcat tomcat
```
* 下载apache-tomcat

[apache-tomcat下载](http://mirror.bit.edu.cn/apache/tomcat/tomcat-8/v8.5.24/bin/apache-tomcat-8.5.24.tar.gz)

下载后上传到服务器

或者在终端输入

```shell
wget http://mirror.bit.edu.cn/apache/tomcat/tomcat-8/v8.5.24/bin/apache-tomcat-8.5.24.tar.gz
```
* 解压apache-tomcat

```shell
tar xf apache-tomcat-8.5.24.tar.gz -C /usr/local/
```
* 修改apache-tomcat文件夹权限

```shell
cd /usr/local/
chown -R tomcat:tomcat apache-tomcat-8.5.24/
```
* 启动apache-tomcat

```shell
/usr/local/apache-tomcat-8.5.24/bin/startup.sh
```
> 输出

```shell
Using CATALINA_BASE:   /usr/local/apache-tomcat-8.5.24
Using CATALINA_HOME:   /usr/local/apache-tomcat-8.5.24
Using CATALINA_TMPDIR: /usr/local/apache-tomcat-8.5.24/temp
Using JRE_HOME:        /usr
Using CLASSPATH:       /usr/local/apache-tomcat-8.5.24/bin/bootstrap.jar:/usr/local/apache-tomcat-8.5.24/bin/tomcat-juli.jar
Tomcat started.
```
* 将tomcat配置为系统服务

```shell
cp /usr/local/apache-tomcat-8.5.24/bin/catalina.sh /etc/init.d/
mv /etc/init.d/catalina.sh /etc/init.d/tomcat
```
* 修改tomcat文件

第二行插入如下内容

```shell
#chkconfig:2345 10 90
#description:Tomcat service
```
在下面内容上面插入

> 112 # OS specific support.  $var _must_ be set to either true or false.

```shell
CATALINA_HOME=/usr/local/apache-tomcat-8.5.24
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.151-1.b12.el7_4.x86_64
```
* 修改tomcat文件权限

```shell
cd /etc/init.d/
chmod +x tomcat
```
* 加入服务列表

```shell
chkconfig --add tomcat
```
* 检查是否加入列表

```shell
chkconfig --list tomcat
```
> 输出如下
>>
```shell
tomcat         	0:关	1:关	2:开	3:开	4:开	5:开	6:关
```

可以在终端输入`service tomcat`查看tomcat的命令

* 启动tomcat服务

```shell
service tomcat start
```
* 修改防火墙

```shell
firewall-cmd --zone=public --add-port=8080/tcp --permanent
firewall-cmd --reload
```
* 浏览器访问IP地址，可以看到tomcat主页

![Centos7安装mysql-5.7 + JAVA1.8+ tomcat8浏览器访问](https://github.com/anderc-done/linux/blob/master/image/Centos7%E5%AE%89%E8%A3%85mysql-5.7%20+%20JAVA1.8+%20tomcat8%E6%B5%8F%E8%A7%88%E5%99%A8%E8%AE%BF%E9%97%AE.jpg?raw=true)

```SHELL
-----------------------The END-----------------------
```


