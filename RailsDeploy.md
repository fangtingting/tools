## 安装Rvm

1、[安装rvm以及gemset使用方法](https://ruby-china.org/wiki/rvm-guide)

2、[每次打开终端无法使用`rvm use`命令解决方法](https://rvm.io/integration/gnome-terminal)

3、[ruby自带的gem安装源](https://rubygems.org/)

4、[ruby安装淘宝源](https://ruby.taobao.org/)

5、[ruby-china提供的gem源，还在试运行](https://gems.ruby-china.org/)


## 安装Passenger跟Nginx

1、[Ubuntu安装Passenger以及在nginx里的配置](https://github.com/ruby-china/ruby-china/wiki/Ubuntu-12.04-%E4%B8%8A%E4%BD%BF%E7%94%A8-Nginx-Passenger-%E9%83%A8%E7%BD%B2-Ruby-on-Rails#%E5%AE%89%E8%A3%85-passenger)

> 这里会直接将Nginx安装上，由Passenger直接进行编译
> [Nginx官方安装文档](https://www.nginx.com/resources/wiki/start/)

    # nginx配置
    server {
      listen 80;
      server_name test.archcy.com;
      rails_env production;
      root /home/reach/webs/archcy/public;
      passenger_enabled on;

      # 反向代理
      location ~ .*\.(jpg|png|gif|bmp|js|css|xml)?$ {
       #root /home/brucewu/archcy.com/public/images/;
         proxy_pass  http://www.archcy.com;
      }
    }
    
2、[Centos下安装Passenger以及在Apache里的配置](https://www.phusionpassenger.com/library/install/apache/install/oss/el7/)


