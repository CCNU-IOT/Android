### 在华为云服务器上部署Mysql数据库

为了实现APP连接云数据库，因此需要配置mysql的远程连接功能

##### 0. 本教程主要包括以下内容

- 在本地通过ssh连接云服务器
- 在云服务器上安装mysql数据库
- 使云数据库能够被远程连接
- 修改数据库配置信息：被多主机连接、修改时区



##### 1.服务器信息

- 华为云服务器：ubuntu16.04
- 公网IP：x.x.x.x（需要登录华为云或腾讯云查看）
- 服务器登录用户名：root
- 服务器登录密码：****



##### 2.在本机上打开`cmd`，用`ssh`连接华为云服务器

- `ssh root@<公网IP>`

- 然后输入上面的登录密码

- 登录成功界面如下：

  <img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230703004804808.png" alt="image-20230703004804808" style="zoom:70%;" />

##### 3.安装`mysql5.7`

- `sudo apt-get update`
- `sudo apt-get install mysql-server`
- 设置root密码

##### 4.进行mysql配置

- 安全配置：`sudo mysql_secure_installation`

进行如下配置：

```shell
Securing the MySQL server deployment.

Enter password for user root:

VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?
【验证密码组件可用于测试密码并提高安全性。它检查密码的强度，并允许用户仅设置足够安全的密码。您想设置“验证密码”组件吗？】
Press y|Y for Yes, any other key for No: Y (是否设置安全插件)

There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 0 (设置密码等级)

/*如果之前设置过root的密码就会出现下面的信息
Using existing password for root.

Estimated strength of the password: 50
Change the password for root ? ((Press y|Y for Yes, any other key for No) : n  (是否更改密码)
 ... skipping.
*/

/*如果之前没有设置过root的密码就会出现下面的信息
Please set the password for root here.

New password: (设置root用户的密码)

Re-enter new password:

Estimated strength of the password: 50
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
*/

By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : y	(是否删除匿名用户)
【默认情况下，MySQL安装有一个匿名用户，允许任何人登录MySQL而无需为其创建用户帐户。这仅用于测试，并使安装过程更流畅。在移入生产环境之前，应先删除它们。】
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : n	(是否不允许远程登录)
【通常，仅应允许root从'localhost'连接。这样可以确保某人无法猜测网络中的root密码。但我们这里要实现远程连接】

 ... skipping.
By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : y (是否删除测试的数据库)
【默认情况下，MySQL带有一个名为“ test”的数据库，任何人都可以访问。这也仅用于测试，应在移入生产环境之前将其删除。
删除测试数据库并访问它？ （按y | Y表示是，按其他任何键表示否）】
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y	(是否重新载入优先级表)
【重新加载特权表将确保到目前为止所做的所有更改将立即生效。现在重新加载特权表？ （按y | Y表示是，按其他任何键表示否）】
Success.

All done!
```

- 如果安装途中出现如下密码错误：（如果没有出现错误则跳过此步）

```
MySQL Failed! Error: SET PASSWORD has no significance for user ‘root’@’localhost’ as the authentication method used doesn’t store authentication data in the MySQL server. Please consider using ALTER USER
```

可参考此方法：

【https://www.nixcraft.com/t/mysql-failed-error-set-password-has-no-significance-for-user-root-localhost-as-the-authentication-method-used-doesnt-store-authentication-data-in-the-mysql-server-please-consider-using-alter-user/4233】

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230722121008058.png" alt="image-20230722121008058" style="zoom:67%;" />

- 查看数据库状态：` systemctl status mysql.service`

![image-20230703010028402](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230703010028402.png)

- 登录数据库：`mysql -u root -p`
- `show databases;`

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230703010136328.png" alt="image-20230703010136328" style="zoom:67%;" />

- 使用`mysql` 数据库：`use mysql;`
- 查看所有表：` show tables;`

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230703010318869.png" alt="image-20230703010318869" style="zoom:60%;" />

- 查看`user`表： `select user,host from user;`（可以看出只允许本地主机访问）

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230703010427992.png" alt="image-20230703010427992" style="zoom:67%;" />

- 配置mysql能被远程连接：` GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root_password' WITH GRANT OPTION;`

  - `root_password`是`root`用户的密码
  - 此时可能遇到`ERROR 1819 (HY000): Your password does not satisfy the current policy requirements`错误，则对密码规则进行修改：
    - `set global validate_password_policy=0;`
    - ` set global validate_password_length=1;`
    - `flush privileges;`

- 刷新权限：`flush privileges;`

- 检查是否配置成功：`select user,host from user;`

  <img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230722110935737.png" alt="image-20230722110935737" style="zoom: 67%;" />

##### 5.修改 `/etc/mysql/mysql.conf.d/mysqld.cnf` 配置文件

- 先退出`mysql`：`exit`
- `sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf`
- 注释掉` bind-address = 127.0.0.1`（因为127.0.0.1代表本主机），即在前面加#，如下图

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230703011237467.png" alt="image-20230703011237467" style="zoom:67%;" />

- 在`[mysqld]`后面的`Basic Settings`中修改时区为东八区：此项设置后，在连接MySQL的时候可以不用每次都手动设置时区

  <img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230722115352133.png" alt="image-20230722115352133" style="zoom:67%;" />

  【附】：[(84条消息) MySql修改时区的三种方法_forever_up422的博客-CSDN博客](https://blog.csdn.net/forever_up422/article/details/122949139)

- 最后重启数据库服务：` service mysql restart`

