## Homebrew

1、安装homebrew：[http://brew.sh](http://brew.sh)

2、安装mysql

> 安装：brew install mysql

> 开启mysql：mysql.start server

> 使用mysql配置脚本，根据提示设置密码：/usr/local/opt/mysql/bin/mysql_secure_installation //mysql 提供的配置向导

## Mac下安装rvm

1、安装rvm

  curl -L https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer | bash -s stable --ruby

[https://ruby-china.org/wiki/install_ruby_guide](https://ruby-china.org/wiki/install_ruby_guide)

2、rvm命令操作：[https://ruby-china.org/wiki/rvm-guide](https://ruby-china.org/wiki/rvm-guide)

3、每次打开终端无法使用`rvm use`命令解决方法：[https://rvm.io/integration/gnome-terminal](https://rvm.io/integration/gnome-terminal)

4、修改gem源：gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/

> ruby自带的gem安装源：[https://rubygems.org/](https://rubygems.org/)

> ruby安装淘宝源：[https://ruby.taobao.org/](https://ruby.taobao.org/)

> ruby-china提供的gem源，还在试运行：[https://gems.ruby-china.org/](https://gems.ruby-china.org/)

4、Ubuntu下安装Passenger以及Nginx配置

这里会直接将Nginx安装上，由Passenger直接进行编译

[https://github.com/ruby-china/ruby-china/wiki/Ubuntu-12.04-%E4%B8%8A%E4%BD%BF%E7%94%A8-Nginx-Passenger-%E9%83%A8%E7%BD%B2-Ruby-on-Rails#%E5%AE%89%E8%A3%85-passenger](https://github.com/ruby-china/ruby-china/wiki/Ubuntu-12.04-%E4%B8%8A%E4%BD%BF%E7%94%A8-Nginx-Passenger-%E9%83%A8%E7%BD%B2-Ruby-on-Rails#%E5%AE%89%E8%A3%85-passenger)

5、Centos下安装Passenger以及Apache配置

[https://www.phusionpassenger.com/library/install/apache/install/oss/el7/](https://www.phusionpassenger.com/library/install/apache/install/oss/el7/)

6、Nginx官方文档：[https://www.nginx.com/resources/wiki/start/](https://www.nginx.com/resources/wiki/start/)

7、Mac下安装Passenger以及Nginx配置

https://www.phusionpassenger.com/library/install/nginx/install/oss/osx/

这个目录下放所有的nginx配置：/usr/local/etc/nginx/servers/

archcy文件
    
    server {
        listen       80;
        server_name  local.archcy.com;
        location / {
          proxy_pass http://127.0.0.1:5004;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header Host $http_host;
        }
      location ~ .*\.(jpg|png|gif|bmp|js|css|xml)?$ {
       #root /home/brucewu/archcy.com/public/images/;
         proxy_pass  http://www.archcy.com;
      }
    }


## mac部署rails遇到的问题

1、nokogiri安装问题：[http://www.nokogiri.org/tutorials/installing_nokogiri.html](http://www.nokogiri.org/tutorials/installing_nokogiri.html)

## mac安转oracle驱动
https://github.com/InstantClientTap/homebrew-instantclient

tnsnames.ora 文件配置

WWW =
(DESCRIPTION =
(ADDRESS_LIST =
(ADDRESS = (PROTOCOL = TCP)(HOST = 172.16.0.40)(PORT = 1521))
)
(CONNECT_DATA =
(SERVICE_NAME = reach)
)
)

PL =
(DESCRIPTION =
(ADDRESS_LIST =
(ADDRESS = (PROTOCOL = TCP)(HOST = 172.16.0.40)(PORT = 1521))
)
(CONNECT_DATA =
(SERVICE_NAME = reach)
)
)

REACH =
(DESCRIPTION =
(ADDRESS_LIST =
(ADDRESS = (PROTOCOL = TCP)(HOST = 172.16.0.40)(PORT = 1521))
)
(CONNECT_DATA =
(SERVICE_NAME = reach)
)
)

~/.bash_profile 文件里加入oracle环境变量

    export ORACLE_BASE=/usr/local/oracle
    export ORACLE_HOME=$ORACLE_BASE/product/instantclient_64/11.2.0.3.0
    export PATH=$ORACLE_HOME/bin:$PATH
    export TNS_ADMIN=$ORACLE_BASE/admin/network
    export SQLPATH=$ORACLE_HOME/sqlplus/admin
    export OCI_DIR=/usr/local/oracle/product/instantclient_64/11.2.0.3.0/lib
    export NLS_LANG="AMERICAN_AMERICA.UTF8"
    export GOPATH=/Users/bruce.wu/workspace_go
    export DYLD_LIBRARY_PATH=/usr/local/oracle/product/instantclient_64/11.2.0.3.0/lib

> source ~/.bash_profile

## brew安装imagemagick（低版本）
  
    brew install imagemagick@6
    
    C_INCLUDE_PATH=/usr/local/Cellar/imagemagick@6/6.9.9-12/include/ImageMagick-6 PKG_CONFIG_PATH=/usr/local/Cellar/imagemagick@6/6.9.9-12/lib/pkgconfig/ gem install rmagick


