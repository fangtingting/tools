## 系统数据库

1、master数据库：由系统表组成，记录了实例上所有数据库的信息，不允许任何人对它进行修改。

2、tempdb数据库：记录了用户创建的所有临时表、临时数据和临时存储过程

3、model数据库：建立新数据的模版，严禁删除model数据库，否则SQL Server系统将无法使用。

4、msdb数据库：由SQL Server Agent服务使用的数据库，该数据库多用于进行复制、作业调度以及管理警报等活动。

5、pubs数据库：实例数据库，是关于一个图书出版公司的数据库。

6、northwind数据库：实例数据库，是关于northwind贸易公司的数据库。

7、查询某个字段所在表sql

	Select a.name as Columns, b.name as TableName from syscolumns a，sysobjects b where a.id = b.id and b.type = 'U' and a.name ='Book_Code' (b.type='U' (表),  b.type='V' (视图))

## 表字段数据类型

1、数值型：Int(4字节)、Tinyint(1字节)、Decimal(n,d)(n总位数，d小数位数)等。

2、字符数据类型：char(n)(n总长度)、varchar(n)(n总长度)等。

3、日期型：datetime、date等。(timestamp：时间戳，行插入、修改时自动更新)

4、二进制类型：binary、image等。

## 创建表

	create  table 表名
	( 
		number  int  identity(1,1)(标识列)  primany key(主键)，(unique唯一性)
	 	name  varchar(20)  not null，
	 	hire_date  datetime  not null  default(getdate())(指定列默认值的常量表达式)，
	 	age  as Year(getdate())-Year(hire_date)
	)

## 修改表结构

1、添加新的字段：Alert table [表名] add [列名] 数据类型 [null | not null]

2、删除列： Alert table [表名] drop [列名]

3、修改列数据类型： Alert table [表名] alert column [列名] 新的类型 [null | not null]

4、添加主键约束：Alert table [表名] add constraint [ 约束名] primary key( [列名])

5、添加唯一约束：Alter table [表名] add constraint [ 约束名] unique([列名])

6、添加默认值：Alter table [表名] add constraint [约束名] default(默认值) for [列名]

7、添加check约束：Alter table [表名] add constraint [约束名] check (内容，可以为正则)

8、添加外键约束：Alter table [表名] add constraint [约束名]  foreign key(列名) referencese 另一表名(列名)

9、删除约束：Alter table [表名] drop constraint [约束名] 

10、重命名表：exec sp_rename '[原表名]','[新表名]'

## 查询表

	Select列名1，列名2，…
	From 表名1，表名2，…
	Where 条件表达式
	Group by 列名 having 条件
	Order by 列名 [Asc | Desc]

## 表插入数据

	Insert into 表名(列名1，列名2，…)  values(值1，值2，…)
	Insert into 表名(列名1，列名2，…) select ….(将查询结果插入)

## 更新数据

	Update 表名 set 列名1=值1，列名2=值2，… [where 条件]
	Update 表名1 set 列名=表名2.列名 from 表名1，表名2 where 条件

## 删除数据

	Delete from 表名 [where 条件]

## 视图

	Create view 视图名 as select ….
	Alert view 视图名 as select ….
	Drop view 视图名

## 字符串函数

1、case函数：case when 表达式1 then 结果表达式1 when 表达式2 then 结果表达式2 else 结果表达式 end

2、upper(字符串)：将字符串转换成大写

3、lower(字符串)：转换成小写

4、substring(字符串，开始位置，长度)：返回给定字符串的子串

5、replicate(字符串，n)：将给定字符串重复n次

6、stuff(字符串1，位置，长度，字符串2)：用字符串2替换字符串1中给定位置和长度的子串。

7、reverse(字符串)：返回给定字符串的反转字符串

8、ltrim(字符串)：返回删除左端空白符后的字符串

9、rtrim(字符串)：返回删除右端空白符后的字符串

10、patindex(‘%pattern%’，字符串)：返回给定字符串中模式串第一次出现的起始位置，没找到则返回0。

## 日期函数

1、getdate()：返回当前系统时间

2、datepart(part，date)：以整数形式返回给定日期时间值的成分。part：year、month、day、week、hour、minute、second。

3、dateadd(part，数值，date)：在给定日期时间值上增加给定成分为单位的时间

4、datediff(part，startdate，enddate)：返回结束时间和开始时间在给定成分上的差值

5、Year(date)：返回年份

6、Month(date)：返回月份

7、Day(date)：返回日期

## 数值函数

1、floor(数值)：返回小于或等于所给数值的最大整数

2、round(数值，小数位数)：返回数值并四舍五入为指定的长度或精度。

## 转换函数

1、cast(表达式 as 数据类型)：将表达式的值从一种类型转变为另一种数据类型

2、convert(数据类型，表达式)：同上

3、字符串连接符号：+

## 聚合函数

1、avg()：求平均

2、sum()：求和

3、count()：计数

4、min()：最小值

5、max()：最大值







