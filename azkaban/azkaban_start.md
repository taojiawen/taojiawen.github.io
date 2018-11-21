# azkaban 工作流调度器

## azkaban配置

### 1.三个压缩包解压放到一个文件夹下好管理

### 2.MySQL下执行sql语句

![TIM截图20181121095802.png](https://upload-images.jianshu.io/upload_images/14465950-147874b28ef63e80.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2.1数据库里生成表

![TIM截图20181121110815.png](https://upload-images.jianshu.io/upload_images/14465950-e858e16797a25f42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.ssl配置(密码记住后面要用)

![TIM截图20181121100554.png](https://upload-images.jianshu.io/upload_images/14465950-0f326339302f4333.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4.生成的keystore放到web下

	keytool -keystore keystore -alias jetty -genkey -keyalg RSA

![TIM截图20181121100729.png](https://upload-images.jianshu.io/upload_images/14465950-7da6fec589fd01b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5.配置web配置proprerties文件

![TIM截图20181121100915.png](https://upload-images.jianshu.io/upload_images/14465950-7561fa2d57dbb63d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5.1修改时区

	Asia/Shanghai

![TIM截图20181121101440.png](https://upload-images.jianshu.io/upload_images/14465950-0f7455ab06289c6c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5.2修改MySQL配置

![TIM截图20181121101419.png](https://upload-images.jianshu.io/upload_images/14465950-c2f197b403e46fab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5.3修改ssl配置(之前设置的密码)

![TIM截图20181121101535.png](https://upload-images.jianshu.io/upload_images/14465950-bf1c4e256d2da974.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 6.配置web配置users文件

	<user username="admin" password="admin" roles="admin,metrics" />

![TIM截图20181121101945.png](https://upload-images.jianshu.io/upload_images/14465950-88ed1667da9ac818.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 7.配置executor执行器

![TIM截图20181121102117.png](https://upload-images.jianshu.io/upload_images/14465950-dd22192e0964e068.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 7.1配置proprerties文件

![TIM截图20181121102257.png](https://upload-images.jianshu.io/upload_images/14465950-0925540140587b18.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 8.启动executor服务

![TIM截图20181121102341.png](https://upload-images.jianshu.io/upload_images/14465950-0b4756e0745d7847.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 8.1在错误文件夹下不能执行

![TIM截图20181121102502.png](https://upload-images.jianshu.io/upload_images/14465950-0a895d8cff31b512.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 8.2 在executor根目录下用相对路径执行

![TIM截图20181121102703.png](https://upload-images.jianshu.io/upload_images/14465950-b387f8e6b520dd93.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 9.启动web服务

![TIM截图20181121102818.png](https://upload-images.jianshu.io/upload_images/14465950-2ba059b80e970a6e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181121102908.png](https://upload-images.jianshu.io/upload_images/14465950-291550f248e0d082.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

ps 服务启动成功

![TIM截图20181121103022.png](https://upload-images.jianshu.io/upload_images/14465950-72ae8eccdc67921a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 10.浏览器访问(注意用HTTPS 端口8443)

![TIM截图20181121103122.png](https://upload-images.jianshu.io/upload_images/14465950-329eafe8a328f864.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 10.1登录名密码就是我们设置的超级用户

![TIM截图20181121103142.png](https://upload-images.jianshu.io/upload_images/14465950-e5dd78a90ff04c67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 11.新建工程

![TIM截图20181121113841.png](https://upload-images.jianshu.io/upload_images/14465950-9afc6ecaa23bc97f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 12.上传工作

![TIM截图20181121111640.png](https://upload-images.jianshu.io/upload_images/14465950-70bb046701079f25.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 12.1上传的必须是zip格式的压缩包(.job文件)

![TIM截图20181121111750.png](https://upload-images.jianshu.io/upload_images/14465950-48989b713ee8c5ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 13.执行工作

![TIM截图20181121112030.png](https://upload-images.jianshu.io/upload_images/14465950-b53a9a3dfd7953b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181121112132.png](https://upload-images.jianshu.io/upload_images/14465950-63b9969384573ea3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 14.查看详情

![TIM截图20181121112300.png](https://upload-images.jianshu.io/upload_images/14465950-04e85bc105f27c4b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 通过command命令来执行
	
	type=command
	command=真正要执行的命令

### 例子1(依赖 两个文件一起压缩 可以有先后顺序 依赖的job先执行完再执行自身 dependencies=job的名称)

	start.job
		
	type=command
	command=echo start
		
	end.job
		
	type=command
	dependencies=start
	command=echo end
		
### 例子2(执行hdfs命令)

	hdfs.job

	type=command
	command=hadoop fs -mkdir /azkaban
		
#### 执行命令工作文件夹 	
	
![TIM截图20181121115051.png](https://upload-images.jianshu.io/upload_images/14465950-3c819c61c32f696a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
### 例子3(执行MapReduce job中设置要执行的命令 job和jar包一起压缩)
		
	wordcount.job
		
	type=command
	command=hadoop jar hadoop-mapreduce-examples-2.6.1.jar wordcount /acinput /acoutput
	
### 例子4(执行hive命令)

	hive-e.job
	
	type=command
	command=hive -e 'select * from datatao.orders';

#### 执行结果
	
![TIM截图20181121145149.png](https://upload-images.jianshu.io/upload_images/14465950-b6cd04ee481579f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)		
		
		