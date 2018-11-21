
# Sqoop数据迁移

## 配置

### 1.解压压缩包

### 2.配置文件(需自己cp)

![TIM截图20181121160831.png](https://upload-images.jianshu.io/upload_images/14465950-07265abcf9c2aead.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181121160758.png](https://upload-images.jianshu.io/upload_images/14465950-d40c9dcfbf9fd2f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.mysql驱动包mysql-connector-java-5.1.34.jar放到lib目录下

## Sqoop命令

![TIM截图20181121161256.png](https://upload-images.jianshu.io/upload_images/14465950-16bddaae59ccf434.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 从关系型数据库导入数据到hdfs 在bin/目录下执行演示(因为没指定存在哪个目录下 所以默认存在/user/用户名/表名)

	./sqoop import \
	--connect jdbc:mysql://172.18.24.195:3306/sqooptest \
	--username root \
	--password hadoop \
	--table users \
	--m 1
	
	(加\换行不执行)

### 自定义指定存储位置增加配置--target-dir /要存放的路径(不能存在)数据以","分割


	--target-dir /sqooptable/users 


### 设置分隔符  --fields-terminated-by

	--fields-terminated-by '\t' 


### 设置查询字段 --columns

	--columns name,pwd

### 往hive中导入数据 --hive-import(没指定存在默认库里 表名还是关系型数据库中表名)

	--hive-import

### 指定库名表名 --hive-table

	--hive-table datatao.usertao

### 使用查询结果导入 使用--query 必须在where后加$CONDITIONS 不能再设置--table

	--query 'select id,name from users where $CONDITIONS'