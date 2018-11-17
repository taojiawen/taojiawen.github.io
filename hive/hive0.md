# Hive简介 

	Hive是基于Hadoop的一个数据仓库工具(离线)，可以将结构化的数据文件
	映射为一张数据库表，并提供类SQL查询功能。

## 为什么使用Hive

	直接使用hadoop所面临的问题 
	人员学习成本太高 
	项目周期要求太短 
	MapReduce实现复杂查询逻辑开发难度太大  
	操作接口采用类SQL语法，提供快速开发的能力。 
	避免了去写MapReduce，减少开发人员的学习成本。 
	功能扩展很方便。
	
# Hive的特点

	可扩展 
	Hive可以自由的扩展集群的规模，一般情况下不需要重启服务。

	延展性 
	Hive支持用户自定义函数，用户可以根据自己的需求来实现自己的函数。

	容错 
	良好的容错性，节点出现问题SQL仍可完成执行。
	
![图片112.png](https://upload-images.jianshu.io/upload_images/14465950-631b453e7c335eec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# hive安装

	标准安装：将mysql作为元数据库
	
	安装MySQL
	
	sudo yum -y install wget
	wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
	sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
	sudo yum -y install mysql-server
	sudo yum -y install mysql
	systemctl start mysqld
	mysql -u root -p(没密码)

	修改密码：需root登录 初始没有密码
	UPDATE mysql.user SET authentication_string=PASSWORD('6757DUgu') where USER='root';
	MySQL> UPDATE mysql.user SET Password=PASSWORD('新密码') where USER='root’;
	MySQL> flush privileges;
	MySQL> exit
		
	设置远程访问数据库：
	登录后输入：
	mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'youmysqlpassword' WITH GRANT OPTION;
	mysql>FLUSH PRIVILEGES
	
	如果忘记密码：
	用命令编辑/etc/my.cnf配置文件，即：vim /etc/my.cnf 或者 vi /etc/my.cnf

	service mysqld restart
	
	上传一个mysql的驱动jar包到hive的安装目录的lib中
	
	mysql-connector-java-5.1.34 放到~/hive/lib
	
	/etc/profile 配置HIVE_HOME

	touch ~/hive/conf/hive-site.xml
	
	连接MySQ配置
	插入如下 密码为MySQL密码

	<configuration>
		<property>
			<name>javax.jdo.option.ConnectionURL</name>
			<value>jdbc:mysql://127.0.0.1:3306/hivedb?createDatabaseIfNotExist=true</value>
		</property>
		<property>
			<name>javax.jdo.option.ConnectionDriverName</name>
			<value>com.mysql.jdbc.Driver</value>
		</property>
		<property>
			<name>javax.jdo.option.ConnectionUserName</name>
			<value>hadoop</value>
		<property>
			<name>javax.jdo.option.ConnectionPassword</name>
			<value>hadoop</value>
		</property>
	</configuration>

	hadoop-2.7.3/etc/hadoop/yarn-site.xml
	
	插入如下 ip为hive所在节点
	
	  <property>

		<name>yarn.resourcemanager.address</name>

		<value>172.18.24.195:8032</value>

	  </property>

	  <property>

		<name>yarn.resourcemanager.scheduler.address</name>

		<value>172.18.24.195:8030</value>

	  </property>

	  <property>

		<name>yarn.resourcemanager.resource-tracker.address</name>

		<value>172.18.24.195:8031</value>

	  </property>
