## ubuntu安装MongoDB

默认的mongodb会将数据库文件存储在“/var/lib/mongo”目录中，而日志文件存储在“/var/log/mongo”文件中。而默认的用户为mongodb，如果你想改变用户来运行你的数据库服务，当然同时需要增加这两个目录的用户权限，否则可能会没有权限写入和读取。查看mongodb.conf文件可以设置数据默认存放路径。(设置远程连接, 默认安装的话只允许127.0.0.1的IP连接,修改/etc/mongodb.conf,注释记录：#bind_ip = 0.0.0.0)

	$ sudo apt-get install mongodb

## MongoDB

1、MongoDB详解：[http://www.mongodb.org/](http://www.mongodb.org/)

2、rails中用Mongoid操作MongoDB，[Mongoid详解](https://docs.mongodb.org/ecosystem/tutorial/ruby-mongoid-tutorial/#ruby-mongoid-tutorial)



