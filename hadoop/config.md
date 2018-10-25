# 单节点Hadoop

### 配置

防火墙关闭 
	systemctl stop firewalld
    systemctl disable firewalld 
    systemctl status firewalld
	
JDK
	下载
	解压
	配置环境变量
	
hadoop配置
	下载hadoop包
	解压
	配置环境变量(bin\sbin)
	
生效配置文件
	. etc/profile
	
![TIM截图20181025195618.png](https://upload-images.jianshu.io/upload_images/14465950-0d39d3c60e9f8ab3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 伪分布式

	cd hadoop-2.7.3/etc/
	
![TIM截图20181025153957.png](https://upload-images.jianshu.io/upload_images/14465950-879bc9f454adccd8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	(1)hadoop-env.sh 
	$JAVA_HOME路径设置成/.../jdk

	(2)core-site.xml    
	临时文件
		<property>  
			<name>hadoop.tmp.dir</name>  
			<value>/.../hadoop/tmp</value>
		</property>  
		<property>  
			<name>fs.defaultFS</name>  
			<value>hdfs://namecode ip:9000</value>  
		</property> 

	(3)hdfs-site.xml
		可有可无
		<property>    
			<name>dfs.replication</name>    
			<value>1</value>    
		</property> 

	   
		<property>    
			<name>dfs.namenode.name.dir</name>    
			<value>file:/.../hadoop/dfs/name</value>    
		</property>    
		<property>    
			<name>dfs.datanode.data.dir</name>    
			<value>file:/.../hadoop/dfs/data</value>    
		</property>

	(4)yarn-site.xml

		<property>  
			<name>mapreduce.framework.name</name>  
		<value>yarn</value>  
		</property>  
	  
		<property>  
			<name>yarn.nodemanager.aux-services</name>  
			<value>mapreduce_shuffle</value>  
		</property>  


	(5)mapred-site.xml（cp mapred-site.xml.templete）

		<property>
			<name>mapreduce.framework.name</name>
			<value>yarn</value>
		</property>

	格式化HDFS
	(1)hadoop namenode -format
	Storage:.....successfully 
	
![TIM截图20181025154313.png](https://upload-images.jianshu.io/upload_images/14465950-80cdf2c83f6bbbbe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
	启动HADOOP服务
	start-all.sh
	关闭hadoop服务
	Stop-all.sh