### mysql 只能Sudo登录问题

Linux下安装mysql后，发现登录必须使用sudo，否则会报Access denied。

解决办法：

<!-- more -->

~~~ mysql
$ sudo mysql -uroot -p
$ use mysql
$ select user,host,plugin form user;
$ update user set plugin='mysql_native_password';
$ flush privileges;
$ exit
~~~

退出mysql，重新正常登陆即可。

### 修改mysql密码

*MySQL 5.7.6*版本以下：

~~~mysql
$ use mysql;
$ update user set password = PASSWORD('root') where user = 'root';
$ flush privileges;
~~~

*MySQL 5.7.6+*版本以上

~~~mysql
$ use mysql;
$ update user set authentication_string = PASSWORD('root') where user = 'root';
$ flush privileges;
~~~

