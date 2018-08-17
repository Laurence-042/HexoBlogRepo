---
title: 关于在Vultr上折腾MySQL的那些事
date: 2018-07-19 22:47:46
tags: [MySQL,服务器,报错解决方案]
preview:
---
我租的是Vultr的Centos7服务器，按操作流程来安装一般不会有什么大问题······嗯，一般······
<!--more-->
---

## 第一步当然是安装MySQL
下载源安装包
```shell
wget http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
```
安装 Mysql 源
```shell
yum localinstall mysql57-community-release-el7-8.noarch.rpm
```
检测是否安装成功
```shell
yum repolist enabled | grep "mysql.*-community.*"
```
> 可能需要修改 默认安装的 Mysql 版本，不需要的话可跳过:
> ```shell
> vim /etc/yum.repos.d/mysql-community.repo
> ```
> 将5.7源的`enabled=0`改为`endaled=1`

安装 Mysql
```shell
yum install mysql-community-server
```
启动 Mysql 服务
```shell
systemctl start mysqld
```
查看启动是否成功
```shell
ps -ef | grep mysqld | grep -v grep
```
查看状态
```shell
systemctl status mysql
```
显示那一大串里有`Active:active(running)`就没问题了

设置开机启动
```shell
systemctl enable mysqld
systemctl daemon-reload
```

mysql 安装完成后，在`/var/log/mysql.log`文件中给 root 生成了一个默认密码  
```shell
grep 'temporary password' /var/log/mysqld.log
```
`root@localhost:`后面就是默认初始密码
*当然你也可以直接`cat /var/log/mysql.log`然后从输出的全部文件内容里面找*

然后用密码登陆MySQL
```shell
mysql -u root -p
```
理论上会显示`password:`之类的，这时候输入初始默认密码即可登陆
*Linux输密码时是没有`*`之类的回显的，虽然大部分用过Linux的都知道这个事，不知道的还是先习惯下Linux操作再在Linux上折腾MySQL吧······*

登陆成功后左边的`[root@vultr ~]# `之类的就会变成`mysql> `了

然后修改root的密码（毕竟默认密码不好记，如果你能记得住这步当然用不着了）
设置密码的格式是
```shell
set password for 用户名@localhost = password('新密码');
```
*别忘了最后的`;`*

> 举个例子，假如现在你想把root的密码改成1024，就输入下面的指令（但实际上现在是无法把1024设为密码的，因为密码强度太低）
> ```
> set password for root@localhost = password('1024');
> ```

不推荐设置为简单密码甚至无密码，故不在此介绍方法，一定要的话自己问Baidu或Google要相应教程

顺便说一下，日志是`/var/log/mysqld.log`  
出了问题先看日志，能解决最好，解决不了去StackOverflow问的时候记得附上相应的日志

---

## 以下为题外话
> 题外话的内容为这个鶸安装时出的问题，一般问题可通过Google解决，解决不了的话······就只能和这个鶸一样卸载重装了······
#### 当日（23：00）：
说实话，一开始吧，我学计算机专业是抱着“一年能做应用程序，两年能搞个服务器，三年能黑个服务器”的期待进的校门，然而现实给了我重重一击————这头一年全在学基础数学物理，专业课只有一个C语言，直到半个月前才得以上第一门限选课程“Java程序设计”并在各种纠结中用Swing弄了个学生成绩管理系统······  
但我还是想弄下服务器，于是在一个晚上的折腾下（或者说是被折腾下），遇见了一堆问题，于是决定把这些写下来以造福和我一样苦逼的新人（手动滑稽）  

#### 第二天（00：00）：
虽说如此······ 我还没能成功启动着玩意  
给的错误信息是
```
mysqld: Error on realpath() on '/var/lib/mysql-files' (Error 13 - Permission denied)
```
然而······  
```
drwxrwxrwx 2 mysql mysql 4096 Apr  8 07:23 /var/lib/mysql-files  
```
完全不知道问题出在哪里，错误日志还不知为何半小时前就罢工了······   

#### 临睡前（02：00）
三小时前出的问题，照着网上教程折腾一小时无果，果断直接照着官网全英文的安装指导来安装，结果······依旧出错，一直折腾到现在，搞得我现在闭着眼睛都能重设文件权限和所有者了（望天）

·································过了很久很久·································

#### 新进展（这个鶸放假回家前终于想起来这件事了）
他想起来当时第一次安装完之后发现安装错了版本，所以曾经卸载过一次MySQL，有可能是当时没卸载干净引发的错误
**卸载重装大法好！！！**
没错，这个鶸终于再次使用这一招了，于是他开始仔细卸载MySQL  

先卸载掉MySQL的组件
```
rpm -qa | grep -i mysql
```
这样就能获取到已安装的组件了，然后就是卸载的时间了！  
*注意：一般卸载前需要先关闭相应程序，但我的MySQL根本没有成功启动过，所以才直接卸载*

示例：
```shell
rpm -ev MySQL-devel-5.6.23-1.linux_glibc2.5
rpm -ev MySQL-server-5.6.23-1.linux_glibc2.5
rpm -ev MySQL-client-5.6.23-1.linux_glibc2.5
```
> 这一步可能出现“这个组件是[某个组件]的依赖”之类的报错，这时候先卸载那个[某个组件]再来删现在要卸载的组件

但不要以为现在就万事大吉了！**还有残留文件！**  

*当时这个鶸第一次从装时貌似就是因为没删干净残留文件，再次出错了*  
```shell
find / -name mysql
```
找到残留的文件夹后，全部`rm -rf`！
*注意不要`rm -rf \ `（笑）*

示例：
```shell
rm -rf /var/lib/mysql
rm -rf /var/lib/mysql/mysql
rm -rf /usr/lib64/mysql
```
注意：卸载后`/etc/my.cnf`不会删除，需要进行手工删除
```shell
rm -rf /etc/my.cnf
```

最后检查下确认卸载干净后再次进行安装，问题得以解决

---

<!--more-->