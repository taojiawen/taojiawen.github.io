# HDFS读写原理篇

## hdfs的工作机制

	特点如下：

	能够运行在廉价机器上，硬件出错常态，需要具备高容错性
	流式数据访问，而不是随机读写
	面向大规模数据集，能够进行批处理、能够横向扩展
	简单一致性模型，假定文件是一次写入、多次读取
	缺点：

	不支持低延迟数据访问
	不适合大量小文件存储（因为每条元数据占用空间是一定的）
	不支持并发写入，一个文件只能有一个写入者
	不支持文件随机修改，仅支持追加写入
	
	HDFS中的block、packet、chunk

	block 
	这个大家应该知道，文件上传前需要分块，这个块就是block，一般为128MB，当然你可以去改，不顾不推荐。因为块太小：
	寻址时间占比过高。块太大：Map任务数太少，作业执行速度变慢。它是最大的一个单位。

	packet 
	packet是第二大的单位，它是client端向DataNode，或DataNode的PipLine之间传数据的基本单位，默认64KB。

	chunk 
	chunk是最小的单位，它是client向DataNode，或DataNode的PipLine之间进行数据校验的基本单位，默认512Byte，因为用作
	校验，故每个chunk需要带有4Byte的校验位。所以实际每个chunk写入packet的大小为516Byte。由此可见真实数据与校验值数
	据的比值约为128 : 1。（即64*1024 / 512）

	例如，在client端向DataNode传数据的时候，HDFSOutputStream会有一个chunk buff，写满一个chunk后，会计算校验和并写
	入当前的chunk。之后再把带有校验和的chunk写入packet，当一个packet写满后，packet会进入dataQueue队列，其他的Data
	Node就是从这个dataQueue获取client端上传的数据并存储的。同时一个DataNode成功存储一个packet后之后会返回一个ack 
	packet，放入ack Queue中。

	概述
	
	1.HDFS集群分为两大角色：NameNode、DataNode  (Secondary Namenode)
	2.NameNode负责管理整个文件系统的元数据
	3.DataNode 负责管理用户的文件数据块
	4.文件会按照固定的大小（blocksize）切成若干块后分布式存储在若干台datanode上
	5.每一个文件块可以有多个副本，并存放在不同的datanode上
	6.Datanode会定期向Namenode汇报自身所保存的文件block信息，而namenode则会负责保持文件的副本数量
	7.HDFS的内部工作机制对客户端保持透明，客户端请求访问HDFS都是通过向namenode申请来进行
	
	写详细步骤：

	客户端向NameNode发出写文件请求。
	检查是否已存在文件、检查权限。若通过检查，直接先将操作写入EditLog，并返回输出流对象。 
	（注：WAL，write ahead log，先写Log，再写内存，因为EditLog记录的是最新的HDFS客户端执行所有的写操作。如果后续真
	实写操作失败了，由于在真实写操作之前，操作就被写入EditLog中了，故EditLog中仍会有记录，我们不用担心后续client读
	不到相应的数据块，因为在第5步中DataNode收到块后会有一返回确认信息，若没写成功，发送端没收到确认信息，会一直重试，
	直到成功）client端按128MB的块切分文件。client将NameNode返回的分配的可写的DataNode列表和Data数据一同发送给最近的
	第一个DataNode节点，此后client端和NameNode分配的多个DataNode	构成pipeline管道，client端向输出流对象中写数据。
	client每向第一个DataNode写入一个packet，这个packet便会直接在pipeline里传给第二个、第三个…DataNode。 
	
	（注：并不是写好一个块或一整个文件后才向后分发）
	每个DataNode写完一个块后，会返回确认信息。 
	（注：并不是每写完一个packet后就返回确认信息，个人觉得因为packet中的每个chunk都携带校验信息，没必要每写一个就汇
	报一下，这样效率太慢。正确的做法是写完一个block块后，对校验信息进行汇总分析，就能得出是否有块写错的情况发生）
	写完数据，关闭输输出流。
	发送完成信号给NameNode。 
	（注：发送完成信号的时机取决于集群是强一致性还是最终一致性，强一致性则需要所有DataNode写完后才向NameNode汇报。
	最终一致性则其中任意一个DataNode写完后就能单独向NameNode汇报，HDFS一般情况下都是强调强一致性）

![图片02.png](https://upload-images.jianshu.io/upload_images/14465950-12548792688c83f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	读
	
	1、跟namenode通信查询元数据，找到文件块所在的datanode服务器
	2、挑选一台datanode（就近原则，然后随机）服务器，请求建立socket流
	3、datanode开始发送数据（从磁盘里面读取数据放入流，以packet为单位来做校验）
	4、客户端以packet为单位接收，现在本地缓存，然后写入目标文件

![图片01.png](https://upload-images.jianshu.io/upload_images/14465950-5fdf7eafd1d2e319.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




