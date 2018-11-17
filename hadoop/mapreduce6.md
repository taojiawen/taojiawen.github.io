# join

## reduce端的join

#### 将关联的添加作为map端的key,将两表满足join条件的数据并携带来源发往一个reducetask，在reduce中进行数据串联

#### 实例：获取商品的完整数据

* 商品goods表：goodsId goodsname stockcount(库存) ..

![image.png](https://upload-images.jianshu.io/upload_images/14466577-a4fcb67255f1aa25.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  
* 订单order表:orderId .. goodsId count(购买数量)
  
  ![image.png](https://upload-images.jianshu.io/upload_images/14466577-69345206ed8b24dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 

#### JoinBean类

	因为创建一个完整信息，所以表中属性同时包括order,good两表中所有的属性,而且为基本javabean类  
	输出需要toString()
	因为之后要用到reduce，需要用到序列化与反序列化，进行文件的存入与读取，类还作为key，所以只实现Writable接口就好  
  
![image.png](https://upload-images.jianshu.io/upload_images/14466577-e5e7e1a9864cd071.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466577-544dba00d5eda8bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
       
	根据map和reduce端需要创建的方法
  
![image.png](https://upload-images.jianshu.io/upload_images/14466577-bc3a5cb2e817a5ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### mapper区

![image.png](https://upload-images.jianshu.io/upload_images/14466577-b71e10fd6d136c2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  
	结果：goodsId-order：1-多  goodsId-goods:1-1
 
   ![image.png](https://upload-images.jianshu.io/upload_images/14466577-6225b713ddfdfdce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   ![image.png](https://upload-images.jianshu.io/upload_images/14466577-5e364b352d2b30c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* reduce  

   ![image.png](https://upload-images.jianshu.io/upload_images/14466577-086ca3a0302699ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### driver区

	结果：

   ![image.png](https://upload-images.jianshu.io/upload_images/14466577-cefda1789668db70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	总结

  ![image.png](https://upload-images.jianshu.io/upload_images/14466577-1aa9b9f5e1655c35.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	缺点：reduce处理压力大，map运算负载很低，利用率不高，在reduce端容易数据倾斜
	解决方法：[map端的join](https://dsm9966.github.io/notebook/mapReduce/22)