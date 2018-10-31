# NAMENODE工作机制

###  NAMENODE职责

	负责客户端请求的响应
	元数据的管理（查询，修改）
	
### 元数据管理

	namenode对数据的管理采用了三种存储形式：
	内存元数据(NameSystem)
	磁盘元数据镜像文件
	数据操作日志文件（可通过日志运算出元数据）
	
	内存中有一份完整的元数据(内存meta data)
	磁盘有一个“准完整”的元数据镜像（fsimage）文件(在namenode的工作目录中)
	用于衔接内存metadata和持久化元数据镜像fsimage之间的操作日志（edits文件）
	注：当客户端对hdfs中的文件进行新增或者修改操作，操作记录首先被记入edits日志文件中，
	当客户端操作成功后，相应的元数据会更新到内存meta.data中
	
### 元数据的checkpoint

	每隔一段时间，会由secondary namenode将namenode上积累的所有edits和一个最新的fsimage
	下载到本地，并加载到内存进行merge（这个过程称为checkpoint）如果secondary namenode
	有最新的fsimage 就不用下载了

	fsimage - 它是在NameNode启动时对整个文件系统的快照
	edit logs - 它是在NameNode启动后，对文件系统的改动序列
	
	只有在NameNode重启时，edit logs才会合并到fsimage文件中，从而得到一个文件系统的最新
	快照。但是在产品集群中NameNode是很少重启的，这也意味着当NameNode运行了很长时间后，
	edit logs文件会变得很大。在这种情况下就会出现下面一些问题：
	edit logs文件会变的很大，怎么去管理这个文件是一个挑战。
	NameNode的重启会花费很长时间，因为有很多改动要合并到fsimage文件上。如果NameNode挂掉
	了，那我们就丢失了很多改动因为此时的fsimage文件非常旧。
	因此为了克服这个问题，我们需要一个易于管理的机制来帮助我们减小edit logs文件的大小和
	得到一个最新的fsimage文件，这样也会减小在NameNode上的压力。这跟Windows的恢复点是非常
	像的，Windows的恢复点机制允许我们对OS进行快照，这样当系统发生问题时，我们能够回滚到
	最新的一次恢复点上。
	
![图片03.png](https://upload-images.jianshu.io/upload_images/14465950-7694f9100bfc98ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###	checkpoint操作的触发条件配置参数

	dfs.namenode.checkpoint.check.period=60  #检查触发条件是否满足的频率，60秒
	dfs.namenode.checkpoint.dir=file://${hadoop.tmp.dir}/dfs/namesecondary
	#以上两个参数做checkpoint操作时，secondary namenode的本地工作目录
	dfs.namenode.checkpoint.edits.dir=${dfs.namenode.checkpoint.dir}

	dfs.namenode.checkpoint.max-retries=3  #最大重试次数
	dfs.namenode.checkpoint.period=3600  #两次checkpoint之间的时间间隔3600秒
	
###	checkpoint的附带作用
	
	namenode和secondary namenode的工作目录存储结构完全相同，所以，当namenode故障退出需要
	重新恢复时，可以从secondary namenode的工作目录中将fsimage拷贝到namenode的工作目录，以
	恢复namenode的元数据
	
### 元数据目录说明
	在第一次部署好Hadoop集群的时候，我们需要在NameNode（NN）节点上格式化磁盘：
	$HADOOP_HOME/bin/hdfs namenode -format
	格式化完成之后，将会在$dfs.namenode.name.dir/current目录下如下的文件结构
	current/
	|-- VERSION
	|-- edits_*
	|-- fsimage_0000000000008547077
	|-- fsimage_0000000000008547077.md5
	`-- seen_txid
	其中的dfs.name.dir是在hdfs-site.xml文件中配置的，默认值如下：
	
	<property>
	  <name>dfs.name.dir</name>
	  <value>file://${hadoop.tmp.dir}/dfs/name</value>
	</property>

	hadoop.tmp.dir是在core-site.xml中配置的，默认值如下
	<property>
	  <name>hadoop.tmp.dir</name>
	  <value>/tmp/hadoop-${user.name}</value>
	  <description>A base for other temporary directories.</description>
	</property>

	dfs.namenode.name.dir属性可以配置多个目录，
	如/data1/dfs/name,/data2/dfs/name,/data3/dfs/name,....。各个目录存储的文件结构和内容都
	完全一样，相当于备份，这样做的好处是当其中一个目录损坏了，也不会影响到Hadoop的元数据，
	特别是当其中一个目录是NFS（网络文件系统Network File System，NFS）之上，即使你这台机器
	损坏了，元数据也得到保存。
	下面对$dfs.namenode.name.dir/current/目录下的文件进行解释。
	1、VERSION文件是Java属性文件，内容大致如下：
	#Fri Nov 15 19:47:46 CST 2013
	namespaceID=934548976
	clusterID=CID-cdff7d73-93cd-4783-9399-0a22e6dce196
	cTime=0
	storageType=NAME_NODE
	blockpoolID=BP-893790215-192.168.24.72-1383809616115
	layoutVersion=-47

	其中
	
　　（1）、namespaceID是文件系统的唯一标识符，在文件系统首次格式化之后生成的；
　　（2）、storageType说明这个文件存储的是什么进程的数据结构信息
		（如果是DataNode，storageType=DATA_NODE）；
　　（3）、cTime表示NameNode存储时间的创建时间，由于我的NameNode没有更新过，所以这里的记录值
		为0，以后对NameNode升级之后，cTime将会记录更新时间戳；
　　（4）、layoutVersion表示HDFS永久性数据结构的版本信息， 只要数据结构变更，版本号也要递减，
		此时的HDFS也需要升级，否则磁盘仍旧是使用旧版本的数据结构，这会导致新版本的NameNode无
		法使用；
　　（5）、clusterID是系统生成或手动指定的集群ID，在-clusterid选项中可以使用它；如下说明

	a、使用如下命令格式化一个Namenode：
	$HADOOP_HOME/bin/hdfs namenode -format [-clusterId <cluster_id>]
	选择一个唯一的cluster_id，并且这个cluster_id不能与环境中其他集群有冲突。如果没有提供
	cluster_id，则会自动生成一个唯一的ClusterID。
	b、使用如下命令格式化其他Namenode：
	$HADOOP_HOME/bin/hdfs namenode -format -clusterId <cluster_id>
	c、升级集群至最新版本。在升级过程中需要提供一个ClusterID，例如：
	$HADOOP_PREFIX_HOME/bin/hdfs start namenode --config $HADOOP_CONF_DIR  -upgrade -clusterId
	<cluster_ID>
	如果没有提供ClusterID，则会自动生成一个ClusterID。
　　（6）、blockpoolID：是针对每一个Namespace所对应的blockpool的ID，上面的这个BP-893790215-192.
	168.24.72-1383809616115就是在我的ns1的namespace下的存储块池的ID，这个ID包括了其对应的NameNode
	节点的ip地址。
　　
	2、$dfs.namenode.name.dir/current/seen_txid非常重要，是存放transactionId的文件，format之后是0，
	它代表的是namenode里面的edits_*文件的尾数，namenode重启的时候，会按照seen_txid的数字，循序从头
	跑edits_0000001~到seen_txid的数字。所以当你的hdfs发生异常重启的时候，一定要比对seen_txid内的数
	字是不是你edits最后的尾数，不然会发生建置namenode时metaData的资料有缺少，导致误删Datanode上多
	余Block的资讯。

	3、$dfs.namenode.name.dir/current目录下在format的同时也会生成fsimage和edits文件，及其对应的md5
	校验文件。


	补充：seen_txid 
	文件中记录的是edits滚动的序号，每次重启namenode时，namenode就知道要将哪些edits进行加载
	