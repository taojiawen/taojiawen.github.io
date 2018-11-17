# 内置函数

## 求平均数

![TIM截图20181115190752.png](https://upload-images.jianshu.io/upload_images/14465950-ec108ea8a3b70f54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 条件控制函数

	IF
	select id,if(age>25,'working','worked') from t_user;

	select moive_name,if(array_contains(actors,'吴刚'),'好电影',’烂片儿’) 
	from t_movie;

	case when 
	语法：
	CASE   [ expression ]
		   WHEN condition1 THEN result1
		   WHEN condition2 THEN result2
		   ...
		   WHEN conditionn THEN resultn
		   ELSE result
	END
	
![TIM截图20181116142859.png](https://upload-images.jianshu.io/upload_images/14465950-01b59579275e1742.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### contain函数

![TIM截图20181116142918.png](https://upload-images.jianshu.io/upload_images/14465950-e7d450d69bfc1ad9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 类型转

	select cast("5" as int) ;
	select cast("2017-08-03" as date) ;
	select cast(current_timestamp as date);

![TIM截图20181116143239.png](https://upload-images.jianshu.io/upload_images/14465950-953ab20dbc4672f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)	
	
### 数学运算函数

	select round(5.4);   ## 5  四舍五入
	select round(5.1345,3) ;  ##5.135
	select ceil(5.4) ; // select ceiling(5.4) ;   ## 6  向上取整
	select floor(5.4);  ## 5  向下取整
	select abs(-5.4) ;  ## 5.4  绝对值
	select greatest(id1,id2,id3) ;  ## 6  单行函数
	select least(3,5,6) ;  ##求多个输入参数中的最小值 
	
![TIM截图20181116143214.png](https://upload-images.jianshu.io/upload_images/14465950-37606514899b4d96.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
### 字符串函数

	substr(string str, int start)   ## 截取子串
	substring(string str, int start)

![TIM截图20181116143153.png](https://upload-images.jianshu.io/upload_images/14465950-7474f533b34f2976.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	
### 时间函数

	select current_timestamp;  返回值类型：timestamp，获取当前的时间戳(详细时间信息)
	select current_date;    返回值类型：date，获取当前的日期
	
	unix时间戳转字符串格式——from_unixtime
	from_unixtime(bigint unixtime[, string format])
	
	如果不带参数，取当前时间的秒数时间戳long--(距离格林威治时间1970-1-1 0:0:0秒的差距) 
	select unix_timestamp();

	unix_timestamp(string date, string pattern)
	示例： select unix_timestamp("2017-08-10 17:50:30");
	select unix_timestamp("2017-08-10 17:50:30","yyyy-MM-dd HH:mm:ss");

	## 将字符串转成日期date
	select to_date("2017-09-17 16:58:32");
	
![TIM截图20181116143130.png](https://upload-images.jianshu.io/upload_images/14465950-265ce2a7c4cbb0ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 集合函数

![TIM截图20181116143529.png](https://upload-images.jianshu.io/upload_images/14465950-9200feaad68d48cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181116143451.png](https://upload-images.jianshu.io/upload_images/14465950-70a93f4debf2ff63.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### map函数

![TIM截图20181116144942.png](https://upload-images.jianshu.io/upload_images/14465950-ac4db3237ad6535f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181116143857.png](https://upload-images.jianshu.io/upload_images/14465950-ce0eb9e378e0b798.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181116143651.png](https://upload-images.jianshu.io/upload_images/14465950-b848f9f1c73bacb3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### collect_set() :将某个字段在一组中的所有值形成一个集合（数组）返回
### 行转列函数：explode()
	两表互转

![TIM截图20181116162828.png](https://upload-images.jianshu.io/upload_images/14465950-b9f999c01fd558ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181116162116.png](https://upload-images.jianshu.io/upload_images/14465950-46b641d3d52211f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181116160806.png](https://upload-images.jianshu.io/upload_images/14465950-86252a8038e34b81.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181116160427.png](https://upload-images.jianshu.io/upload_images/14465950-00764eeb5cebc410.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### count()：求一个组中的满足某条件的数据条数

![TIM截图20181116151239.png](https://upload-images.jianshu.io/upload_images/14465950-612af35a8bd6fa31.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### json解析函数：表生成函数

![TIM截图20181116170249.png](https://upload-images.jianshu.io/upload_images/14465950-cf92b16d036e8bfc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 窗口分析函数

![TIM截图20181116175408.png](https://upload-images.jianshu.io/upload_images/14465950-cc1256ea63401b0c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### sum() over()——级联求和

![TIM截图20181116192640.png](https://upload-images.jianshu.io/upload_images/14465950-1f90c5b4bcd40c14.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



