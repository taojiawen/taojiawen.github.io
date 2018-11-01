# DATANODE的工作机制

### 概述

	1、Datanode工作职责：
	
	存储管理用户的文件块数据
	定期向namenode汇报自身所持有的block信息（通过心跳信息上报）
	（这点很重要，因为，当集群中发生某些block副本失效时，集群如何恢复block初始副本数量的问题）

	<property>
		<name>dfs.blockreport.intervalMsec</name>
		<value>3600000</value>
		<description>Determines block reporting interval in milliseconds.</description>
	</property>

	2、Datanode掉线判断时限参数:
	
	datanode进程死亡或者网络故障造成datanode无法与namenode通信，namenode不会立即把该节点判定为
	死亡，要经过一段时间，这段时间暂称作超时时长。HDFS默认的超时时长为10分钟+30秒。如果定义超时
	时间为timeout，则超时时长的计算公式为：
	
		timeout  = 2 * heartbeat.recheck.interval + 10 * dfs.heartbeat.interval。
		而默认的heartbeat.recheck.interval 大小为5分钟，dfs.heartbeat.interval默认为3秒。
		需要注意的是hdfs-site.xml 配置文件中的heartbeat.recheck.interval的单位为毫秒，
		dfs.heartbeat.interval的单位为秒。所以，举个例子，如果heartbeat.recheck.interval设置为
		5000（毫秒），dfs.heartbeat.interval设置为3（秒，默认），则总的超时时间为40秒。

	<property>
			<name>heartbeat.recheck.interval</name>
			<value>2000</value>
	</property>
	<property>
			<name>dfs.heartbeat.interval</name>
			<value>1</value>
	</property>