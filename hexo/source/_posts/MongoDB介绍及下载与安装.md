---
title: MongoDB介绍及下载与安装
---

# MongoDB介绍及下载与安装
MongoDB是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。他支持的数据结构非常松散，是类似json的bjson格式，因此可以存储比较复杂的数据类型。Mongo最大的特点是他支持的查询语言非常强大，其语法有点类似于面向对象的查询语言，几乎可以实现类似关系数据库单表查询的绝大部分功能，而且还支持对数据建立索引。

它的特点是高性能、易部署、易使用，存储数据非常方便。主要功能特性有：

*  集合存储，易存储对象类型的数据。
*  模式自由。
*  支持动态查询。
*  支持完全索引，包含内部对象。
*  支持查询。
*  支持复制和故障恢复。
*  使用高效的二进制数据存储，包括大型对象（如视频等）。
*  自动处理碎片，以支持云计算层次的扩展性
*  支持RUBY，PYTHON，JAVA，C++，PHP,Javascript等多种语言。
*  文件存储格式为BSON（一种JSON的扩展）
*  可通过网络访问

所谓“面向集合”（Collenction-Orented），意思是数据被分组存储在数据集中，被称为一个集合（Collenction)。每个 集合在数据库中都有一个唯一的标识名，并且可以包含无限数目的文档。集合的概念类似关系型数据库（RDBMS）里的表（table），不同的是它不需要定 义任何模式（schema)。
模式自由（schema-free)，意味着对于存储在mongodb数据库中的文件，我们不需要知道它的任何结构定义。如果需要的话，你完全可以把不同结构的文件存储在同一个数据库里。
存储在集合中的文档，被存储为键-值对的形式。键用于唯一标识一个文档，为字符串类型，而值则可以是各中复杂的文件类型。我们称这种存储形式为BSON（Binary Serialized dOcument Format）。

MongoDB服务端可运行在Linux、Windows或OS X平台，支持32位和64位应用，默认端口为27017。推荐运行在64位平台，因为MongoDB在32位模式运行时支持的最大文件尺寸为2GB。

#一、下载
MongoDB的官网是：[http://www.mongodb.org/](http://www.mongodb.org/)

MongoDB最新版本下载在官网的DownLoad菜单下：[http://www.mongodb.org/downloads](http://www.mongodb.org/downloads)

#二、安装

将下载好的安装包文件解压放到盘符的根目录（如C：或D：），为了方便建议文件夹命名尽量简短如（d:\mongodb）

解压后的文件
![Alt 安装后的文件](az.png)

#三、启动数据库

1.创建数据库目录（用来存放数据的目录）
![Alt ](cj.png)

2.打开终端
![Alt ](zd.png)

3.进入mongodb/bin目录

我的mongdb文件是放到桌面的

```basic	
	$ cd desktop/mongdb/bin
```

4.启动数据库

执行bin目录里面的`mongod`命令创建数据库

`--dbpath`：指定创建数据库的目录

```basic	
	$ sudo ./mongod --dbpath ../data
```
启动成功
![Alt ](qd.png)

mongodb默认连接端口27017，如果出现如图的情况，可以打开http://localhost:27017查看，发现以下文字连接成功，如果不成功，可以查看端口是否被占用。

It looks like you are trying to access MongoDB over HTTP on the native driver port.

启动成功后窗口不能关闭(**关闭就不能连接数据库了**)

#四、操作数据库

成功启动MongoDB后，再打开一个命令行窗口进入mongodb/bin目录输入mongo，就可以进行数据库的一些操作。

mac系统需要加上`./` window系统不需要

```basic
	$ ./mongo
```

mongodb基本命令

* show dbs:显示数据库列表 
* show collections：显示当前数据库中的集合
* db.getName();查看当前使用的数据库
* db.stats();显示当前db状态
* db.version();当前db版本
* use myDB:切换/创建数据库
* db.createCollection('test'):创建一个聚集集合（table）

#增删改查

###增加

```sql
//mongodb语句
db.test.insert({"name":"abc","age":18})
//相当于sql语句
INSERT INTO test (name,age) VALUES("abc","18")
```

###删除
```sql
//mongodb语句
db.test.remove({"age":15})
//相当于sql语句
DELETE FROM test WHERE age = 15
```
###修改

```sql
//mongodb语句
db.test.update({"name":"abc"},{$set:{"name":"updateName"}):修改
//相当于sql语句
UPDATE test SET name = "updateName" WHERE  name = "abc"
```

###查找

```sql
//mongodb语句
db.test.find({"name","abc"})
//相当于sql语句
SELECT * FROM test WHERE name="abc"
```





 

 

 



