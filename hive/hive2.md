# hive查询语法

# 分组

![TIM截图20181115191331.png](https://upload-images.jianshu.io/upload_images/14465950-b26cb34ac68a7d27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 排序

	order by：会对输入做全局排序，因此只有一个reducer，只有一个 reduce task的结果，比如文件名是000000_0，会导致当输入规模较大时，需要较长的计算时间
	sort by：不是全局排序，其在数据进入reducer前完成排序。因此，如果用sort by进行排序，并且设置mapred.reduce.tasks>1，则 sort by只保证每个reducer的输出有序，不保证全局有序
	distribute by：根据指定的字段将数据分到不同的reducer，且分发算法是hash散列
	Cluster by：除了具有Distribute by的功能外，还会对该字段进行排序。因此，如果分桶和sort字段是同一个时，此时clustered by = distribute by + sort by如果我们要分桶的字段和要
	排序的字段不一样，那么我们就不能适用clustered by。分桶表的作用：最大的作用是用来提高 join 操作的效率


![TIM截图20181115192142.png](https://upload-images.jianshu.io/upload_images/14465950-f51444bddf9dd04c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181115192245.png](https://upload-images.jianshu.io/upload_images/14465950-aba94a3f4c65b948.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181115192040.png](https://upload-images.jianshu.io/upload_images/14465950-06609b615854a124.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181115192302.png](https://upload-images.jianshu.io/upload_images/14465950-ad55cb0b14b0f311.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181115192317.png](https://upload-images.jianshu.io/upload_images/14465950-08fc9fb73a820d64.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# join 联表查询

## 内连接inner可以省略 

![TIM截图20181115192922.png](https://upload-images.jianshu.io/upload_images/14465950-9eb3c8f8318ade3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181115202007.png](https://upload-images.jianshu.io/upload_images/14465950-e156ecfd8a6f1e2d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 左连接

![TIM截图20181115202035.png](https://upload-images.jianshu.io/upload_images/14465950-c925560bab47fec0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	left semi join
	Left semi join ：相当于join连接两个表后产生的数据中的左半部分
	in/exists关键字(1.2.1之后新特性)
	in关键字
	select * from t_a a where a.id in (select id from t_b); 
	效果等同于left semi join

## 全连接

![TIM截图20181115202016.png](https://upload-images.jianshu.io/upload_images/14465950-d36e75d54a17cdd8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 子查询

![TIM截图20181115202047.png](https://upload-images.jianshu.io/upload_images/14465950-3a03fec37f196c37.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 数据类型 

	TINYINT (1字节整数)
	SMALLINT (2字节整数)
	INT/INTEGER (4字节整数)
	BIGINT (8字节整数)
	FLOAT (4字节浮点数)
	DOUBLE (8字节双精度浮点数)
	
	BOOLEAN（布尔类型）：true  false
	
	字符串类型
	STRING
	VARCHAR(20) (字符串1-65535长度，超长截断)
	CHAR (字符串，最大长度255)
	
	时间类型
	TIMESTAMP (时间戳) (包含年月日时分秒毫秒的一种封装)
	DATE (日期)（只包含年月日）
	
## array类型字段

![TIM截图20181115202205.png](https://upload-images.jianshu.io/upload_images/14465950-7737635981e34723.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## map类型字段

![TIM截图20181115202226.png](https://upload-images.jianshu.io/upload_images/14465950-e242ac942037b7bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## struct类型字段(类似对象) 

![TIM截图20181116104903.png](https://upload-images.jianshu.io/upload_images/14465950-91e61f7d1322028b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181116104942.png](https://upload-images.jianshu.io/upload_images/14465950-bb18b9c578eeee27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
