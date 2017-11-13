# SSHD服务防止暴力破解

* **软件**

fail2ban-0.8.14

* **系统环境**

CentOS 6.8

### 步骤

* **下载fail2ban**

[fail2ban下载链接](http://www.fail2ban.org/wiki/index.php/Downloads)

* **上传服务器并解压**

```shell
# tar zxf fail2ban-0.8.14.tar.gz
```
* **安装**

需要python版本大于2.4，默认系统已安装python2.6.6

进入fail2ban目录并安装

```shell
# python setup.py install
```
* **生成服务启动脚本**

```shell
# cp files/redhat-initd /etc/init.d/fail2ban
```

* **设置开机自动启动**

```shell
# chkconfig --add fail2ban
```
* **设置防暴力破解规则**

```shell
# vim /etc/fail2ban/jail.conf
```
>96行enabled改为true

>100行logpath改为/var/log/secure		#系统登陆日志文件

>102行增加	bantime = 86400		#输入错误禁止登陆时间  86400=24小时

>103行增加	findtime = 300			#5分钟内出现规定次数密码错误就禁止登陆

>maxretry = 5						#设置允许输入错误次数

保存退出
* **启动服务**

```shell
# service fail2ban start
```
* **测试**

连接服务器，输入错误密码5次

* **自己输入错误，解除禁止**

清空登陆日志
```shell
# > /var/log/secure
```
重启fail2ban服务
```shell
# service fail2ban restart
```
* **查看禁止列表**

```shell
# fail2ban-client status
# fail2ban-client status ssh-iptables
```
