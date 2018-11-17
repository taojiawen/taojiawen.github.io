
## MapReduce与Yarn
* yarn负责资源的调度：用户程序向yarn 申请资源,yarn负责分配资源
* 主管角色：resourceManager 提供具体运算：nodeManager



![image.png](https://upload-images.jianshu.io/upload_images/14466577-b12497419da39f1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466577-7df488507e0485df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![1.png](https://upload-images.jianshu.io/upload_images/14466577-6336c6df63810e4e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 总结

![TIM截图20181112100140.png](https://upload-images.jianshu.io/upload_images/14465950-707b67c26e2327cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 集群运行

	步骤：

	将mapreduce程序打包成jar包
	改namenode和datanode的hostname名字为namenode,datanode1/2/3
	向namenode和datanode的/etc/hosts内添加集群信息（同完全分布式）
	配置namenode和datanode的yarn-site.xml(ip为)

![TIM截图20181107100119.png](https://upload-images.jianshu.io/upload_images/14465950-8ce3eaba3419ea71.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)