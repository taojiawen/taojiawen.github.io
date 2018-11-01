# HDFS应用开发篇

### HDFS的java操作

#### 搭建开发环境

	1.把 hadoop-eclipse-plugin-2.7.3 插件导入eclipse目录下plugin中
	(如不好用,再导入dropins 还不好用请换个workspace)成功如下图:
	
![TIM截图20181101201928.png](https://upload-images.jianshu.io/upload_images/14465950-94453698d9ea5beb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
![微信图片_20181101202741.png](https://upload-images.jianshu.io/upload_images/14465950-bbb15f4d750fc91b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181101203031.png](https://upload-images.jianshu.io/upload_images/14465950-f626a2739398aec2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181101203156.png](https://upload-images.jianshu.io/upload_images/14465950-4d09f905534439b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181101203316.png](https://upload-images.jianshu.io/upload_images/14465950-a2f2a1d111f458ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181101203340.png](https://upload-images.jianshu.io/upload_images/14465950-7f6609652e75e8c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	2.建一个Java工程
	
![TIM截图20181101204007.png](https://upload-images.jianshu.io/upload_images/14465950-52469fbda8db0033.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![微信截图_20181101204052.png](https://upload-images.jianshu.io/upload_images/14465950-dc86eb40c4358cb3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 现在就可以开始使用Java操作HDFS了

### JUnit测试 单元测试

![TIM截图20181101205301.png](https://upload-images.jianshu.io/upload_images/14465950-e2674bc27606a08c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181101205416.png](https://upload-images.jianshu.io/upload_images/14465950-3cece0582f4cee76.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181101205431.png](https://upload-images.jianshu.io/upload_images/14465950-30de9c5b471ac0ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181101205532.png](https://upload-images.jianshu.io/upload_images/14465950-a8a690fa039fadcf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181101205702.png](https://upload-images.jianshu.io/upload_images/14465950-6798f3417c9c86e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	还有@before和@after 作用就是在test执行之前或之后执行