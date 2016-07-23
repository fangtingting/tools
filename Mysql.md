## Windows下忘記Mysql密碼

1、关闭Mysql:`net stop mysql`

2、找到MySQL安装目录中的my.ini文件，用记事本打开后分别找到basedir和datadir，根据你MySQL安装路径分别设置好路径，然后继续查找[mysqld]，找到后在其下面一行输入`skip-grant-tables`后保存my.ini

3、启动Mysql：`net start mysql`

4、以空密码登录Mysql

5、再关闭Mysql，第2步中查找[mysqld]，找到后在删除刚刚输入的skip-grant-tables后保存my.ini

6、打开MySQL直接按回车以空密码登录，然后修改MySQL密码

	set password for root@localhost=password('password')

## 系统数据库

1、information_schema数据库：保存着关于MySQL服务器所维护的所有其他数据库的信息。查询某个数据库某个字段所在的表sql：

	select * from information_schema.columns where table_schema='数据库名' and column_name='字段名'

2、mysql数据库：user表记录了可以访问mysql数据库用户和权限。

3、数据库备份：数据库名后加 –d参数是备份数据库结构，加 –t 参数是备份数据库数据，数据库名替换成 –A 是备份所有的数据库
	
	mysqldump –uroot –p123456 数据库名 > 备份路径

4、数据库还原
	
	mysql –uroot –p123456 数据库名 < 还原路径

## Mysql操作

1、添加新用户
	
	create user '用户名'@'%' identified by '密码'。
	//第二种方法
	insert into mysql.user(Host,User,Password) values('%','用户名',password('密码'))
	flush privileges

2、授权给用户远程登录mysql

	grant all privileges on 数据库名.* to 用户名@'%' identified by '密码' with grant option
	flush privileges

3、删除用户
	delete from mysql.user where User='用户名' and Host='%'
	
	//第二种方法
	dorp user 用户名@'%'

4、修改指定用户密码
	
	alter user用户名@'%' identified by '密码'

	//第二种方法
	update mysql.user set password=password('密码') where User=’用户名’ and Host=’%’`
	flush privileges

5、取消授权
	revoke privileges on 数据库.* from 用户名@'%'

## Mysql命令

1、use 数据库名：进入某个数据库

2、show processlist：查看连接服务器用户线程

3、show databases：显示所有数据库

4、created database 数据库名 [default character set utf8 default collate utf8_general_ci]：创建数据库

5、show tables：显示所有的表

6、describe 表名：显示表结构

7、alter database 数据库名 [default character set 编码格式 default collate 排序规则]：修改数据库

8、drop database 数据库名：删除数据库

## 创建表

	创建表：create table [数据库.]表名(
		列名1  数据类型 not null primary key,
		列名2  数据类型 null,
		...
	)

## 修改表

	alter table [数据库名.]表名 add (列名 数据类型 not null)	
	alter table [数据库名.]表名 modify(列名 数据类型 null)	
	alter table [数据库名.]表名 drop constraint <约束名> | primary key(列名,….)

## 查询表

	Select 字段1，字段2，….
	From 表1，表2，….
	Where 条件
	Group by 字段名 having 条件
	Having 过滤条件 (只有存在group by时才使用)
	Order by 字段名 [asc|desc]

## 更新表

1、单表：update 表名 set 字段名=表达式 where 条件 order by 字段名 limit 数量
 	
2、多表：update 表1，表2，…. Set 字段1=表达式，字段2=表达式，…. Where 条件

3、创建索引：create index 索引名 on 表名(列名 asc,…)
	
4、删除索引： drop index 索引名

## 删除表
	
	drop table [数据库名.]表名
	单表： delete from 表名 where 条件 order by 字段名 limit 数量
	多表： delete 表名1，表名2，…. from 表名1，表名2，…. Where 条件 

## 表插入数据

	insert into 表名(字段1，字段2，...) values(值1，值2，...)
	insert into 表名 set 字段1=表达式，字段2=表达式，...
	insert into 表名(字段1，字段2，….) select 字段1，字段2，... from ... 

## 數值函數

1、LEAST(值1，值2，….)：在多个参数下，返回值为最小值，如果有值为null，则返回值为null。

2、GREATEST(值1，值2，….)：在多个参数下，返回值为最大值，如果有值为null。则返回值为null。

3、ABS(X)：返回X的绝对值。

4、EXP(X)：返回e的X乘方值。

5、FLOOR(X)：返回不大于X的最大整数值。

6、MOD(N，M)：返回N%M取余后的整数。

7、ROUND(X，D)：返回X值保留小数点后D位，D可为负值。

8、CAST(值 as varchar)：将数字转换成字符串

9、FORMAT(X，D)：返回数值X保留D位小数后的字符串。

10、TRUNCATE(X，D)：返回值X保留小数位数D位。如果D是0，则在小数点被除去。如果D是否定的，那么D的值的整数部分的值将被截断。

## 字符串函數

1、CONCAT(字符串1，字符串2，….)：连接字符串，如果有值为null，则返回值为null

2、REGEXP ：模式匹配，匹配则返回1，否则返回0

3、SUBSTRING(字符串，开始位置，长度n)：返回从开始位置起长度为n的子字符串。

4、SPACE(n)：返回一个由n个空格组成的字符串。

5、REPEAT(字符串，重复次数n)：重复字符串n次，有值为null，则返回null。

6、REPLACE(字符串，被替换字符，替换字符)：返回替换后的字符串。

7、REVERSE(字符串)：颠倒字符串。

8、LENGTH(字符串)：返回字符串长度。

9、CONCAT_WS(分隔符，字符串1，字符串2，….)：通过分隔符连接字符串。

## 时间与日期函数

1、CURRENT_TIMESTAMP()，CURRENT_TIME()，CURRENT_DATE()，CURDATE()：返回当前时间和日期。

2、DATE(‘时间表达式’)：提取时间表达式中的日期部分。

3、DATE_ADD(起始日期，INTERVAL expr type)，DATE_SUB(起始日期，INTERVAL expr type)：从起始日期添加或者减去时间间隔值，type值可以为：year、month、day、week、hour、second。

4、ADDDATE(起始日期，天数)：有跟DATE_ADD一样的用法，这个方式是另外一种。

5、DATEDIFF(起始日期，结束日期)、TIMEDIFF(起始时间，结束时间)：返回起始和结束之间的天数或者时间。

6、DATE_FORMAT(日期，格式format)：%Y返回年份4位数，%y返回年份2位数，%M返回大写月份，%m返回数值型月份，%D返回大写日期，%d返回数值型日期，%H返回小时，%i返回分钟，%s返回秒。所以format格式有：’%Y-%m-%d’、’%Y/%m/%d’、‘%Y-%m-%d %H:%i:%s’等。

7、DAYOFMONTH(日期)：返回当月所在日期。

8、DAYOFWEEK(日期)：返回对应工作日索引(1=周日，2=周一，….7=周六)。

9、DAYOFYEAR(日期)：返回该日期对应一年中的天数。

10、DAY(日期)、HOUR(日期)、YEAR(日期)、MONTH(日期)、WEEK(日期)：提取日期的某个部分。

## 其他函数

1、GROUP_CONCAT(表达式 separator ‘分隔符’)：只要用于group by语法里。如果有null值则返回null。

2、IFNULL(表达式1，表达式2)：假如表达式1不为null，则返回表达式1，否则返回表达式2。

3、case函数：

	case value when compare_value then result when ….else result end；

	case when 条件1 then result when …..else result end。

4、MIN(表达式)、MAX(表达式)、SUM(表达式)、COUNT(表达式)：主要用于查询表sql中。




