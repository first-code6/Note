# 基本命令

### 1.INSERT INTO

> 指定需要插入的值

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

> 为表的所有列添加值，但是，请确保其中包括了所有的值，而且值的顺序与表中列的顺序相同。

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

> 多个值插入

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...),(value4, value5, value6, ...)
```

> SELECT INTO SELECT 从表中添加数据到表中

```sql
INSERT INTO table_name (column1, column2, column3, ...)
SELECT column1=value1, column2=value2, column3=value3 FROM table_name2
```

### 2.UPDATE

> 为索引的行修改值  **==注意：没有where的话全部的数据都会被更改！！！==**

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

> 使用INNER JOIN来批量添加LEFT JOIN

```sql
UPDATE table_name
set colum1 = A.colum1
FROM table_name1 AS A INNER JOIN table_name2 AS B
WHERE condition
```

### 3.DELETE

> 删除满足where条件的行 **==注意：没有where的话全部的数据都会被删除！！！==**

```sql
DELETE FROM table_name WHERE condition;
```

> DELETE FROM FROM JOIN 多联表删除

```sql
DELETE FROM A FROM table_name AS A
LEFT JOIN table_name1 AS B ON A.colums1 = B.colums2
WHERE A.colums = value1
```

> 多表删除：

<https://blog.csdn.net/hevenue/article/details/70264356>

### 4.DROP

> 删除整个表（与delete删除整个表是删除整个表的数据，但表依然存在，drop是直接删除整个表）

```sql
DROP TABLE Customers;
```

### 5.JOIN

> 在查询两张表时，使用两个select语句会产生两个查询结果，使用join可通过一列合并两张表

```sql
select * from boxstation as a join box type as b on a.id=b.id
```

### 6.COUNT

> 一个基本命令，可返回查询的记录数，如：

```sql
-- 查询有多少条满足条件的数据
select count(1) from aa where bb = cc
```

ps:不使用exist语句查询是否存在时可以用count查询，如果count为0则表示没有

### 7.RIGHT

> 从右往左数获取字符串

```sql
SELECT RIGHT('SQL Tutorial', 3)
-- 输出：ial
```

### 8.DB\_ID

> 查询数据库ID，可用于sql server profiler监听指定数据库

```js
SELECT DB_ID('DATA_BASE_NAME')
-- 03
```

# SELECT使用的一些筛选语句

## 1.distinct(去重)

`SELECT DISTINCT`语句用于仅返回不同的（不同的）值

例如：

```sql
-- 查询Customers里面的不重复的Country
SELECT DISTINCT Country FROM Customers;
```

# 基本类型

## 1.小数型

`decimal(7, 4)`：其中7表示共计7位，4表示小数点后4位

# 基本函数

## 1.获取刚添加的自增id（scope\_identity）

```sql
declare @id INT
INSERT INTO ...
SET @id = scope_identity()
SELECT @id
```

## 2.获取当前时间GETDATE()

```sql
declare @date datetime
set @date = GETDATE()
select @date
```

## 3.截取指定的字符串

```sql
-- 需要处理的字符串，开始位置(从一开始)，截取的长度
SUBSTRING(string, start, length)
-- 例
SUBSTRING('HELLO', 1, 2)
```

# 一.sql server字符串日期相互转换

## 1.使用函数CONVERT

```sql
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )
```

示例

```sql
Select CONVERT(varchar(100), GETDATE(), 0): 05 16 2006 10:57AM

Select CONVERT(varchar(100), GETDATE(), 1): 05/16/06

Select CONVERT(varchar(100), GETDATE(), 2): 06.05.16

Select CONVERT(varchar(100), GETDATE(), 3): 16/05/06

Select CONVERT(varchar(100), GETDATE(), 4): 16.05.06

Select CONVERT(varchar(100), GETDATE(), 5): 16-05-06

Select CONVERT(varchar(100), GETDATE(), 6): 16 05 06

Select CONVERT(varchar(100), GETDATE(), 7): 05 16, 06

Select CONVERT(varchar(100), GETDATE(), 8): 10:57:46

Select CONVERT(varchar(100), GETDATE(), 9): 05 16 2006 10:57:46:827AM

Select CONVERT(varchar(100), GETDATE(), 10): 05-16-06

Select CONVERT(varchar(100), GETDATE(), 11): 06/05/16

Select CONVERT(varchar(100), GETDATE(), 12): 060516

Select CONVERT(varchar(100), GETDATE(), 13): 16 05 2006 10:57:46:937

Select CONVERT(varchar(100), GETDATE(), 14): 10:57:46:967

Select CONVERT(varchar(100), GETDATE(), 20): 2006-05-16 10:57:47

Select CONVERT(varchar(100), GETDATE(), 21): 2006-05-16 10:57:47.157

Select CONVERT(varchar(100), GETDATE(), 22): 05/16/06 10:57:47 AM

Select CONVERT(varchar(100), GETDATE(), 23): 2006-05-16

Select CONVERT(varchar(100), GETDATE(), 24): 10:57:47

Select CONVERT(varchar(100), GETDATE(), 25): 2006-05-16 10:57:47.250

Select CONVERT(varchar(100), GETDATE(), 100): 05 16 2006 10:57AM

Select CONVERT(varchar(100), GETDATE(), 101): 05/16/2006

Select CONVERT(varchar(100), GETDATE(), 102): 2006.05.16

Select CONVERT(varchar(100), GETDATE(), 103): 16/05/2006

Select CONVERT(varchar(100), GETDATE(), 104): 16.05.2006

Select CONVERT(varchar(100), GETDATE(), 105): 16-05-2006

Select CONVERT(varchar(100), GETDATE(), 106): 16 05 2006

Select CONVERT(varchar(100), GETDATE(), 107): 05 16, 2006

Select CONVERT(varchar(100), GETDATE(), 108): 10:57:49

Select CONVERT(varchar(100), GETDATE(), 109): 05 16 2006 10:57:49:437AM

Select CONVERT(varchar(100), GETDATE(), 110): 05-16-2006

Select CONVERT(varchar(100), GETDATE(), 111): 2006/05/16

Select CONVERT(varchar(100), GETDATE(), 112): 20060516

Select CONVERT(varchar(100), GETDATE(), 113): 16 05 2006 10:57:49:513

Select CONVERT(varchar(100), GETDATE(), 114): 10:57:49:547

Select CONVERT(varchar(100), GETDATE(), 120): 2006-05-16 10:57:49

Select CONVERT(varchar(100), GETDATE(), 121): 2006-05-16 10:57:49.700

Select CONVERT(varchar(100), GETDATE(), 126): 2006-05-16T10:57:49.827

Select CONVERT(varchar(100), GETDATE(), 130): 18 ???? ?????? 1427 10:57:49:907AM

Select CONVERT(varchar(100), GETDATE(), 131): 18/04/1427 10:57:49:920AM
```

# 二.字符串转日期

## 1.使用CAST

```sql
CAST (expression AS data_type)
```

例：

```sql
Select cast('2009-01-01' as datetime)
```

# Sql Server日期与时间函数

## 1.当前系统日期、时间

```sql
select getdate()
```

## 2. dateadd 在向指定日期加上一段时间的基础上，返回新的 datetime 值

语法：

```sql
DATEADD (datepart , number , date )
```

举个栗子：加3天

```sql
select dateadd(day,3,'2000-10-15')
```

# 三.存储过程

## 创建一个简单的存储过程并调用

```sql
create procedure 存储过程名称()

begin
      ......
end

--调用存储过程

call 存储过程名称()
```

## 标准存过程例子

```sql
--设置存储过程
USE 数据库名称
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

ALERT PROCEDURE 名字
	(
    	@数据名称 数据类型,         --传参数据
    	@test varchar(16),
    	@数据名称 数据类型 output  --输出语句
	)
AS
BEGIN
  ......
  return @数据名称
END



--调用存储过程
EXEC 名字 传参 , @输出数据名字 output
```

## 存储过程实例

1.存储过程

```sql
USE [Data_Base]    -- 使用数据库
GO
SET ANSI_NULLS ON    -- 设置OFF后使用查询时可用=null或者is null，如果使用ON后只能使用is null查询
GO
SET QUOTED_IDENTIFIER ON
GO
-- =============================================
-- Author:		By YXY
-- Create date: 231008
-- Description:	更新学生备注

-- SELECT * from yetest
-- SP_HELP yetest

-- SAMPLE: EXEC yesp 1,N'这里是更新后的备注',2 ， 变量名称 output

-- EXEC yesp 测试表ID,备注信息,操作模式，返回值
	--注：操作模式分为数字1，2，3，4分别代表SELECT, UPDATE, DELETE, INSERT

-- EXEC UP_COLS YETEST
-- EXEC up_settbltext yetest,N'我的测试表'
-- EXEC UP_TABLES 我的测试表

-- SELECT, UPDATE, DELETE, INSERT
-- =============================================
ALTER PROCEDURE [dbo].[yesp]    -- 存储过程名字并定义
	-- Add the parameters for the stored procedure here
	-- 添加存储过剩所需的参数params（不要忘记定义类型）
	 (
	 @yeid int,
	 @remark nvarchar(1000),
	 @model varchar(20),
	 @mesout int output		--这是输出参数
	 )

AS
BEGIN
	-- 开始存储过程内容
	-- SET NOCOUNT ON added to prevent extra result sets from
	-- interfering with SELECT statements.
	SET NOCOUNT ON;

	if @model = 'studentinfo' goto fnd_studentinfo ;
	if @model = '2' goto upd_data ;
	if @model = '3' goto del_data ;
	if @model = '4' goto in_data  ;

	goto exit_data
	
	fnd_studentinfo:
	----------
		select aa=@yeid,bb=@remark,cudate=getdate()

	--根据请求ID 查询内容
	SELECT yeid, yename, yeurl,	country, remark, rgt, mdt
	FROM yetest where yeid=@yeid;
	set @mesout = 1
	goto exit_data

	upd_data:
	----------
	--更新备注
	declare @rgt datetime = getdate()

	UPDATE yetest SET remark=@remark, rgt=@rgt WHERE YEID=@yeid;
	

	SELECT yeid, yename, yeurl,	country, remark, rgt, mdt
	FROM yetest where yeid=@yeid;
	
	set @mesout = 2
	goto exit_data

	del_data:
	----------
	--删除数据
	DELETE yetest WHERE YEID=@yeid ;
	SELECT yeid, yename, yeurl,	country, remark, rgt, mdt
	FROM yetest;
	set @mesout = 3
	goto exit_data

	in_data:
	----------
	--增添数据
	
	declare @yename nvarchar(100) = 'tony'
	declare @yeurl varchar(50) = 'www.baidu.com'
	declare @country nvarchar(100) = '中国-china'
	declare @rgtadd datetime = getdate()
	declare @mdt datetime = getdate()

	INSERT INTO yetest (yename, yeurl, country, remark, rgt, mdt) 
	VALUES (@yename, @yeurl, @country, @remark, @rgtadd, @mdt) ;
	SELECT yeid, yename, yeurl,	country, remark, rgt, mdt
	FROM yetest;
	set @mesout = 4
	goto exit_data


	exit_data:
	----------
	RETURN @mesout
	END
```

2.使用存储过程

```sql
-- 使用带有返回参数的存储过程
declare @aa INT;    -- 定义返回数据的变量
EXEC yesp 1,N'这里是更新后的备注',2 , @aa output; -- 使用存储过程，返回数据后面需接 output关键字
select @aa;    -- 查看输出变量
```

# 四.存储变量，设置变量

```sql
--使用declare语句神明一个变量
declare @username varchar(32);

--使用set语句给变量赋值
set @username = 'yxy';

--将user表中id=1的名称赋值给username
set @username = (select * from user where id = 1);
select @username = username from user where id = 1;
```

# 五. 备注信息

## 备注表信息, 查找表信息

### 1.对表列进行备注方便查找表名

对表名进行备注

```sql
EXEC up_settbltext 【表名】,N'我的测试表'   --大写N表示是可以接受多国语言的字符串格式
```

### 2.查询表备注获取表名

查询备注为我的测试表的表明

```sql
EXEC UP_TABLES 我的测试表
```

# 六.将旧表的数据复制到新表上

```sql
--SELECT * INTO SHUANGTEST FROM yetest
--SELECT * INTO <new table name> FROM <old table name>
```

# 七.存储过程

## 1.存储过程使用if，else语句

在存储过程使用if语句

```sql
if a > 0
begin
    select * from user
end
```

在存储过程中使用if else语句

```sql
if a > 0
begin
    select * from user
end
else
begin
    select * from user_name
end
```

# 八.INNER JOIN

# 九.DISTINCT

`SELECT DISTINCT`语句用于仅返回不同的（不同的）值

例如：

```sql
-- 查询Customers里面的不重复的Country
SELECT DISTINCT Country FROM Customers;
```

# 十.多表查询

```sql
	-- 第一种方法
	SELECT A.cmpny, A.useFormId, useFormName=max(A.useFormName), useFormDes=max(A.useFormDes), 
	frTime=max(A.frTime), toTime=max(A.toTime), rmk=max(A.rmk), openYn=max(A.openYn), A.groupId, count( distinct B.userid), aa=count(distinct 		    
	C.reg_id)
	--select  *
	from formAdmin as A 
	left join formUsrGrp as B on a.groupId=B.groupId
	left join formSubmit as C on a.useFormId=c.useFormId
	group by A.cmpny,A.useFormId, A.groupId



	
	select * from formAdmin

	select * from formSubmit

	select * from formUsrGrp

-- 第二种方法

	select * from
	(
	select A.useFormId, smsum=count(distinct B.reg_id) 
	from formAdmin as A
	left join formSubmit as B on a.useFormId=b.useFormId
	group by A.useFormId
	) as aa
	left outer join
	(
	select  A.useFormId, allobj=count(b.cmpny)
	from formAdmin as A 
	left join formUsrGrp as B on a.groupId=b.groupId
	group by A.useFormId
	) as bb on aa.useFormId=bb.useFormId


-- 第三种方法

	with cte as (
		select A.useFormId,groupId=max(A.groupId), smsum=count(distinct B.reg_id) 
	from formAdmin as A
	left join formSubmit as B on a.useFormId=b.useFormId
	group by A.useFormId
	)
	select A.useFormId,A.groupId, A.smsum,allobj=count(b.cmpny)
	from cte as A 
	left join formUsrGrp as B on a.groupId=b.groupId
	group by A.useFormId,A.groupId, A.smsum

```

# 十一.创建临时表

## 1.一般方法

```sql
create table #tempone
(
    cmpny varchar(2),
    roleid varchar(10),
    menuid varchar(10),
    rmk nvarchar(200)
)

insert into #tempone
select cmpny, roleid, menuid, rmk from rolesGroup
select * from #tempone

drop table #tempone
```

因为每次都需要输入大量的建表数据，所以当数据不多时可以使用以下快速方法

## 2.快速方法

```sql
select cmpny, roleid, menuid, rmk
into #temptwo
from rolesGroup

select * from #temptwo
drop table #temptwo
```

> 注意！！！使用完临时表后需要drop释放掉临时表，不然会占用内存

# 十二.CTE公用表表达式

CTE(Common Table Expression) 公用表表达式，它是在单个语句的执行范围内定义的临时结果集。

只在查询期间有效。它可以自引用，也可在同一查询中多次引用，实现了代码段的重复利用。

```sql
WITH cte(CategoryID,CategoryName,ParentID,CategoryLevel)
AS (
　　SELECT CategoryID
　　　　　　,CategoryName
　　　　　　,ParentID
　　　　　　,CategoryLevel
　　FROM Category(NOLOCK)
　　WHERE Status = 1 and parentid = 23
)
select * from cte;

-- 或者

WITH cte
AS (
　　SELECT CategoryID
　　　　　　,CategoryName
　　　　　　,ParentID
　　　　　　,CategoryLevel
　　FROM Category(NOLOCK)
　　WHERE Status = 1 and parentid = 23
)
select * from cte;
```

# 十三.OPENJOSN

在sqlserver中，可以接收json数据（转换为字符串后的JSON数据）

有不带with的默认显示方式，和带With的自定义显示方式两种

```sql
-----默认显示
DECLARE @json NVARCHAR(MAX)
 
SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';
 
SELECT *
FROM OPENJSON(@json);

-----自定义显示（注意：后方的缩影想为根元素时使用 $ 即可）
DECLARE @json NVARCHAR(MAX)
SET @json =   
  N'[  
       {  
         "Order": {  
           "Number":"SO43659",  
           "Date":"2011-05-31T00:00:00"  
         },  
         "AccountNumber":"AW29825",  
         "Item": {  
           "Price":2024.9940,  
           "Quantity":1  
         }  
       },  
       {  
         "Order": {  
           "Number":"SO43661",  
           "Date":"2011-06-01T00:00:00"  
         },  
         "AccountNumber":"AW73565",  
         "Item": {  
           "Price":2024.9940,  
           "Quantity":3  
         }  
      }  
 ]'  


SELECT * FROM  
 OPENJSON ( @json )  
WITH (   
              Number   varchar(200) '$.Order.Number' ,  
              Date     datetime     '$.Order.Date',  
              Customer varchar(200) '$.AccountNumber',  
              Quantity int          '$.Item.Quantity'  
 )


```

SQL官方教程：<https://learn.microsoft.com/zh-cn/sql/t-sql/functions/openjson-transact-sql?view=sql-server-ver16>

# 十四.索引（可大幅增加查询速度）

## 1.创建索引

```sql
CREATE INDEX idx_index_name_colums
ON table_name (column1, column2, ...);
```

## 2.删除索引

```sql
DROP INDEX index_name
ON table_name;
```

# 十五.事务处理（错误回调）

## 1.COMMIT

一段事务活动的结束，提交sqlserver内容

```sql
BEGIN TRANSACTION   -- 开始一段事务活动
.....SQL.....
COMMIT TRANSACTION
```

## 2.ROLLBACK

返回到指定sqlserver语句之前

```sql
SAVE TRANSACTION delete1
......SQL......
ROLLBACK TRANSACTION delete1 -- 一般加error判断如下列所示


IF @@ERROR <> 0 ROLLBACK TRANSACTION delete1
```

## 3.合起来一起应用

网站：<https://blog.csdn.net/vaivxuanzi/article/details/124861513>

```sql
BEGIN TRANSACTION
INSERT INTO Customers(cust_id, cust_name)
VALUES(1000000010, 'Toys Emporium');
SAVE TRANSACTION StartOrder;
INSERT INTO Orders(order_num, order_date, cust_id)
VALUES(20100,'2001/12/1',1000000010);
IF @@ERROR <> 0 ROLLBACK TRANSACTION StartOrder;
INSERT INTO OrderItems(order_num, order_item,prod_id, quantity, item_price)
VALUES(20100, 1, 'BR01', 100, 5.49);
IF @@ERROR <> 0 ROLLBACK TRANSACTION StartOrder;
INSERT INTO OrderItems(order_num, order_item,prod_id, quantity, item_price)
VALUES(20100, 2, 'BR03', 100, 10.99);
IF @@ERROR <> 0 ROLLBACK TRANSACTION StartOrder;
COMMIT TRANSACTION
```

# 十六.自定义错误抛出

在SQL SERVER 中，我们可以使用`RAISERROR`自定义一个错误并且抛出，

教程：<https://blog.csdn.net/WuLex/article/details/109574115>

其中接受5各参数：

**第一个参数：`{ msg_id | msg_str | @local_variable }`**\
`msg_id`：表示可以是一个`sys.messages`表中定义的消息代号；\
使用 `sp_addmessage` 存储在 `sys.messages` 目录视图中的用户定义错误消息号。\
用户定义错误消息的错误号应当大于 `50000`。

`msg_str`：表示也可以是一个用户定义消息，该错误消息最长可以有 2047 个字符；\
（如果是常量，请使用N’xxxx’，因为是`nvarchar`的）\
当指定 `msg_str` 时，`RAISERROR` 将引发一个错误号为 `5000` 的错误消息。

`@local_variable`：表示也可以是按照 `msg_str` 方式的格式化字符串变量。

**第二个参数：`severity`**\
用户定义的与该消息关联的严重级别。（这个很重要）\
任何用户都可以指定 0 到 18 之间的严重级别。\
`[0,10]`的闭区间内，不会跳到`catch`；\
如果是\[11,19],则跳到`catch`；\
如果\[20,无穷)，则直接终止数据库连接；

**第三个参数：`state`**\
如果在多个位置引发相同的用户定义错误，\
则针对每个位置使用唯一的状态号有助于找到引发错误的代码段。

**第四个参数：`argument`**\
用于代替 `msg_str` 或对应于 `msg_id` 的消息中的定义的变量的参数。

**第五个参数：`option`**\
错误的自定义选项，可以是下表中的任一值：\
`LOG` ：在错误日志和应用程序日志中记录错误；\
`NOWAIT`：将消息立即发送给客户端；\
`SETERROR`：将 `@@ERROR` 值和 `ERROR_NUMBER` 值设置为 `msg_id` 或 `50000`；

简单使用：

```sql
RAISERROR(N'你好，这是一个错误', 11, 1)
```
# 游标

[SqlServer游标的创建与使用 - 熊泽-学习中的苦与乐 - 博客园](https://www.cnblogs.com/xiongze520/p/14633171.html#_label1)

## 游标的定义

游标（Cursor）是处理数据的一种方法，为了查看或者处理结果集中的数据，游标提供了在结果集中一次一行或者多行前进或向后浏览数据的能力

它使用户可逐行访问由SQL Server返回的结果集。使用游标(cursor)的一个主要的原因就是把集合操作转换成单个记录处理方式。

用SQL语言从数据库中检索数据后，结果放在内存的一块区域中，且结果往往是一个含有多个记录的集合。

游标机制允许用户在SQL server内逐行地访问这些记录，按照用户自己的意愿来显示和处理这些记录。

我们可以把游标当作一个指针，它可以指定结果中的任何位置，然后允许用户对指定位置的数据进行处理。

## 游标基础示例
```sql
--声明（创建）游标对象（标准游标）
declare 
MyCursor cursor 
for SELECT  s.Name,sc.ClassName FROM a_Students s
INNER JOIN a_StudentClass sc ON s.ClassId=sc.ClassId;

--声明两个变量接收从游标中取出的值
declare @Name varchar(50),@ClassName varchar(50);    
begin
    --打开游标
    open MyCursor;

    --移动游标取值
    fetch next from MyCursor into @Name,@ClassName;
    --这里对游标的状态进行判断，如果为0，证明游标中有值
    while @@FETCH_STATUS = 0
        BEGIN
            print(@Name);
            print(@ClassName);
            --让游标继续往后移动
            fetch next from MyCursor into @Name,@ClassName
        end

--关闭游标
CLOSE MyCursor

--释放游标
DEALLOCATE MyCursor

end

```

## 游标注意事项

游标用于按顺序遍历结果集。

但一般情况下，应尽量避免使用游标，可使用while或者for loop替代

原因：

1.  游标违背了关系模型，即按集合来考虑问题的思想；
2. 游标逐行对纪录进行操作，会带来额外的开销，使用游标的解决方案通常比使用集合的解决方案要慢得多；
3. 使用游标的解决方案，需要用很多代码来描述对游标的操作，因此代码更长，可读性更差，也更难以维护。

如果要使用，一定记住要记住：

1. 用完之后一定要关闭和释放，尽量不要在大量数据上定义游标；
2. 尽量不要使用游标上更新数据；
3. 尽量不要使用insensitive, static和keyset这些参数定义游标；
4. 如果可以，尽量使用FAST_FORWARD关键字定义游标；
5. 如果只对数据进行读取，当读取时只用到FETCH NEXT选项，则最好使用FORWARD_ONLY参数。