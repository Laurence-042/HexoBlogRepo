---
title: Python-MySQL数据查询
date: 2018-07-31 16:03:33
tags: [Python, 笔记]
---
此处记录了这个鶸的第一个和数据库相关的用于查询远程数据库的python程序
<!--more-->

若只想连接本地的MySQL数据库，直接看最下面的部分就行了，如果要连接远程数据库，你就需要进行一系列不算麻烦但绝对说不上简易的操作了······

前几天经历了一串令人智熄的操作后，总算折腾好了MySQL，然而结果竟然无法连接远程服务器的MySQL······ 

~~这个鶸准备先在本地练下手，什么时候需要连接那个远程服务器之后再去找相应的方法~~

这个鶸发现了连接失败的问题所在：MySQL服务用的3306端口他喵的防被火墙给关了······

好吧，闲话说得够多了，下面进入正题，也就是连接远程数据库并查询其中的数据

---

当然，你要连接一个数据库的话，首先数据库里要有数据才行
首先登陆数据库
```shell
mysql -u root -p
```
> 如果你用的是Windows，即使安装了MySQL并配置好了Path依旧可能会提示`'mysql'不是内部或外部命令，也不是可运行的程序或批处理文件。`此时以管理员权限运行CMD就可以执行`mysql`命令了。

创建数据库(Database)
```shell
CREATE DATABASE 数据库名;
```
本次创建一个名为`test0`的数据库：
```shell
CREATE DATABASE test0;
```

创建数据表(Table)
```shell
CREATE TABLE table_name (column_name column_type);
```
本次创建一个名为`testt`，有分别名为`testC`和`testC_re`的两列数据的数据表
> 注意：应先指定操作的数据库再创建数据表

```shell
mysql> use test0;
Database changed
mysql> CREATE TABLE testt(
   -> testC INT NOT NULL,
   -> testC_re VARCHAR(100) NOT NULL
   -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
出现类似`Query OK, 0 rows affected (0.16 sec)`的输出就说明创建过程成功结束了

> * NOT NULL，在操作数据库时如果输入该字段的数据为NULL ，就会报错。
> * AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。
> * PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。
> * ENGINE 设置存储引擎
> * CHARSET 设置编码。
>
> 更多的关于数据类型和指定属性的教程可以在[来自runoob的数据类型的教程](http://www.runoob.com/mysql/mysql-data-types.html)和[来自runoob的创建数据表的教程](http://www.runoob.com/mysql/mysql-create-tables.html)里面找到，本文仅作为第一次操作的引导写成，不包含任何非必要操作的详细介绍

就这样，我们第一个数据表就建好了

现在往里面插入几条数据以便进行查询测试

```shell
mysql> INSERT INTO testt
    -> (testC, testC_re)
    -> VALUES
    -> (1, "test data");
```
出现类似`Query OK, 1 rows affected, 1 warnings (0.01 sec)`的输出就说明插入成功了

现在你的数据库中带查询数据就准备完成了

---

但是！你还是要等一会才能愉快的敲python，因为你还没有一个有操作权限的用户（root不算，root默认只能从localhost访问，无法远程访问）
```shell
mysql> GRANT USAGE ON *.* TO'laurence042'@'%' IDENTIFIED BY '[您没有查案此数据的权限]' WITH GRANT OPTION;
mysql> GRANT ALL PRIVILEGES ON *.* TO 'laurence042'@'%' IDENTIFIED BY '[您没有查案此数据的权限]' WITH GRANT OPTION;
```
这段设置里，我的用来进行数据库管理的用户名是`laurence042`，并设置成`可从任意IP访问`。将`'%'`换成类似`'127.0.0.1'`这样的IP就可以限定用户只能从这个IP进行访问。至于`'[您没有查案此数据的权限]'`······这是我的密码诶，怎么可能让你看呢（笑）如果你恰好认识我而且想要的话，可以当面找我要，这样的话我就能当面嘲笑你了（手动滑稽）

为保险起见，防止和这个鶸犯一样的白痴错误，你最好先检查下防火墙那边`3306`端口的状态。

不同操作系统的防火墙相关指令不一样，以这个鶸在用的Centos7为例，CentOS7的默认防火墙为firewall  
首先查看firewall启动情况
```shell
systemctl status firewalld
```
如果没有启动，那最好还是启动一下，毕竟防火墙还是挺重要的······用下面的命令启动防护墙
```shell
systemctl start firewalld
```
查看一下`3306`端口是否已经开启，如果显示`yes`,则表示防火墙已开启该端口（没错，这个鶸的显示的是`no`）
```shell
firewall-cmd --query-port=3306/tcp 
```
如果你和这个鶸一样看到了`no`，那么，开启开启`3306`端口
```
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```
然后重启防火墙使刚刚的打开端口的操作生效
```
firewall-cmd --reload
```

> 当然也可以关闭centos7的默认防火墙
> `systemctl stop firewalld` 
> 和禁用防火墙
> `systemctl mask firewalld`
>然后使用iptables防火墙，centos7默认是没有安装iptables的，使用
> `yum install iptables`
> `yum install iptables-services`
> 两步进行安装即可。
> 可以参考[@anne的夏天](http://www.cnblogs.com/anne32184/)大佬的这篇关于详细iptables安装配置和讲解的教程[CentOS7安装iptables防火墙](https://www.cnblogs.com/anne32184/p/5961806.html)进行安装配置

如果之后还使出了问题······问度娘（baidu）或谷哥（Google）吧，这个鶸也不知道怎么办了······



---

接下来就能用python进行数据库中数据的读操作了，注释很详细，就不赘述了

值得一提的是，代码里连接的是本地服务器（`127.0.0.1`），所以可以安装完MySQL就直接用root连接，如果是远程服务器，用前文的步骤创建一个可以在你的IP地址连接的用户进行连接

```python
import mysql.connector  # 首先导入包，没有的话用pip安装相应的包或用IDE解决

config = {
    'host': '127.0.0.1',  # 服务器地址，本次测试连接的是本地服务器
    'user': 'root',  # 用来访问MySQL数据库的用户名
    'password': '[您没有查案此数据的权限]',  # 用来访问MySQL数据库的用户的密码
    'port': 3306,  # MySQL数据库所用的端口号，默认是3305
    'database': 'test0',  # 数据库名称
    'charset': 'utf8'  # 编码
}
try:
    cnn = mysql.connector.connect(**config)  # 连接数据库
except mysql.connector.Error as e:
    print('connect fails!{}'.format(e))
cursor = cnn.cursor()
try:
    '''
    此段代码用于获取并输出数据
    sql_query为请求数据字符串
    此处的字符串含义为“获取当前数据库中名为“testt”的数据表中名字分别为“testC”和“testC_re”的两列数据
    '''
    sql_query = 'select testC,testC_re from testt ;'
    cursor.execute(sql_query)
    for testC, testC_re in cursor:
        print(testC, testC_re)
except mysql.connector.Error as e:
    print('query error!{}'.format(e))
finally:
    cursor.close()  # 不要忘记关闭连接
    cnn.close()

```

---
<!--more-->