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

## mac部署rails遇到的问题

1、nokogiri安装问题：[http://www.nokogiri.org/tutorials/installing_nokogiri.html](http://www.nokogiri.org/tutorials/installing_nokogiri.html)

