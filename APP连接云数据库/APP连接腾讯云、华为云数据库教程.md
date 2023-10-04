### 1. 在华为云/腾讯云服务器上部署Mysql数据库

【参考文档】：《在华为云、腾讯云服务器上部署Mysql数据库》



### 2. 在本地安装Navicat

【说在前面】：

其实也可以不安装，但是安装并连接数据库后便于我们观察数据库中的数据，而且便于插入一些原始数据，也可以用于测试数据库的连接

【参考文档】：《Navicat安装教程》



### 3.使用Navicat连接腾讯云/华为云Mysql数据库

【连接教程】：

[(70条消息) 使用navicat连接腾讯云mysql数据库_腾讯云数据库允许nanvicat访问_RONG LU.的博客-CSDN博客](https://blog.csdn.net/ln82799/article/details/120242730)

- `mysql`添加远程连接权限：[Mysql连接报错：1130-host ... is not allowed to connect to this MySql server如何处理 - 陌笠人灬苼 - 博客园 (cnblogs.com)](https://www.cnblogs.com/mh-study/p/11352607.html#:~:text=如果出现： mysql> select Host%2C User%2CPassword from user%3B ERROR,from user%3B 修改user表中的Host%3Aupdate user set Host%3D'%' where User%3D'root'%3B)
- 开放服务器的`3306`端口

【注】：当配置好可以远程连接的文件后，要刷新权限，并且重启数据库服务，否则可能开放了端口，也没办法连接成功：

```shell
sudo service mysql restart
```



### 4.利用JDBC实现Android连接腾讯云/华为云上部署的数据库

【参考文档】：《利用JDBC实现Android连接腾讯云/华为云上部署的数据库》

