一、安装MongoDB

　　1.环境配置：

　　　　i.操作系统：CentOS release 6.8 (Final) 

[root@iZ2ze2pbbffhmn53ao4tuaZ bin]# cat /etc/redhat-release
　　　　ii.计算机类型：x86_64

[root@iZ2ze2pbbffhmn53ao4tuaZ bin]# uname -m
　　2.下载对应的MongoDB 版本

[root@iZ2ze2pbbffhmn53ao4tuaZ bin]# wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel62-3.6.4.tgz
　　3.解压MongoDB 数据库

[root@iZ2ze2pbbffhmn53ao4tuaZ opt]# tar -zxvf mongodb-linux-x86_64-rhel62-3.6.4.tgz
　　4. 启动MongoDB

[root@iZ2ze2pbbffhmn53ao4tuaZ bin]# mkdir -p /data/db    # 创建数据库数据存放目录
[root@iZ2ze2pbbffhmn53ao4tuaZ opt]# cd /opt/mongodb/bin  

[root@iZ2ze2pbbffhmn53ao4tuaZ bin]# ./mongod  # 启动Mongo Server服务，默认端口:27017，默认允许本地连接
二、配置账号和密码

　　1.开启认证

　　　MongoDB 默认安装完成以后，只允许本地连接，同时不需要使用任何账号密码就可以直接连接MongoDB，这样就容易被黑，让支付一些比特币，所以为了避免这些不

必要的麻烦，所以我们需要给Mongo设置一个账号密码；

[root@iZ2ze2pbbffhmn53ao4tuaZ bin]# ./mongod --auth  # 启用认证
　　2.创建管理员用户

> use admin
switched to db admin
> db.createUser({user:"admin",pwd:"password",roles:["root"]})
Successfully added user: { "user" : "admin", "roles" : [ "root" ] }
　　3.认证登录

> db.auth("admin", "password")
　　4.MongoDB role 类型

数据库用户角色（Database User Roles）
　　　　read：授予User只读数据的权限
　　　　readWrite：授予User读写数据的权限

数据库管理角色（Database Administration Roles）：
　　　　dbAdmin：在当前dB中执行管理操作
　　　　dbOwner：在当前DB中执行任意操作
　　　　userAdmin：在当前DB中管理User

备份和还原角色（Backup and Restoration Roles）：
　　　　backup
　　　　restore

跨库角色（All-Database Roles）：
　　　　readAnyDatabase：授予在所有数据库上读取数据的权限
　　　　readWriteAnyDatabase：授予在所有数据库上读写数据的权限
　　　　userAdminAnyDatabase：授予在所有数据库上管理User的权限
　　　　dbAdminAnyDatabase：授予管理所有数据库的权限

集群管理角色（Cluster Administration Roles）：
　　　　clusterAdmin：授予管理集群的最高权限
　　　　clusterManager：授予管理和监控集群的权限，A user with this role can access the config and local databases, which are used in sharding and replication, respectively.
　　　　clusterMonitor：授予监控集群的权限，对监控工具具有readonly的权限
　　　　hostManager：管理Server

　　5.添加数据库用户

> use flowpp
switched to db flowpp
> db.createUser({user: "flowpp", pwd: "flopww", roles: [{ role: "dbOwner", db: "flowpp" }]})   # 创建用户flowpp,设置密码flopww，设置角色dbOwner
　　6.查看系统用户

复制代码
> use admin
switched to db admin
> db.system.users.find()  # 显示当前系统用户
{ "_id" : "admin.admin", "user" : "admin", "db" : "admin", "credentials" : { "SCRAM-SHA-1" : { "iterationCount" : 10000, "salt" : "9jXmylyRAK22TZmzv1Thig==", "storedKey" : "z76cVrBjX/CTFmn5RujtU+dz7Nw=", "serverKey" : "JQGonM84iDMI1nIXW7FdyOE55ig=" } }, "roles" : [ { "role" : "root", "db" : "admin" } ] }
{ "_id" : "flowpp.flowpp", "user" : "flowpp", "db" : "flowpp", "credentials" : { "SCRAM-SHA-1" : { "iterationCount" : 10000, "salt" : "KvocqWZA9E2tXBHpKpdAeQ==", "storedKey" : "50Kxc3LEgCSVN1z16S8g4A6jVp8=", "serverKey" : "0RSnsxd/7Yzmqro/YOHf/kfbHCk=" } }, "roles" : [ { "role" : "dbOwner", "db" : "flowpp" } ] }
复制代码
　　7.删除用户

复制代码
1.切换admin ，删除用户flowpp ，删除失败
> use admin
switched to db admin
> db.dropUser("flowpp")
false
2.切换flowpp ，删除用户flowpp，删除成功
> use flowpp
switched to db flowpp
> db.dropUser("flowpp")
true
复制代码
说明：

　　删除用户的时候需要切换到用户管理的数据库才可以删除；