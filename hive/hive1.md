# hive的使用

![TIM截图20181114101304.png](https://upload-images.jianshu.io/upload_images/14465950-a146acba8f91ce15.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114101356.png](https://upload-images.jianshu.io/upload_images/14465950-9490206d14c42dd5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# hive表 

## 删除表(内部表是完整删除,外部表则只删除MySQL上元文件)

![TIM截图20181113174341.png](https://upload-images.jianshu.io/upload_images/14465950-b8c1092a2a42ccbf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 清空表

![TIM截图20181113174319.png](https://upload-images.jianshu.io/upload_images/14465950-eac93af0d08a5c2d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 建一个内部表

![TIM截图20181114092114.png](https://upload-images.jianshu.io/upload_images/14465950-ae960c3146820482.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 展示表结构

![TIM截图20181114092204.png](https://upload-images.jianshu.io/upload_images/14465950-53638b9024596902.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 向表中插入数据(原文件移动到表目录下)

![TIM截图20181114102420.png](https://upload-images.jianshu.io/upload_images/14465950-151f9a5f8f09b2ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 向一个表内插入一样的文件自动改名

![TIM图片20181114094357.png](https://upload-images.jianshu.io/upload_images/14465950-f014dbc937656580.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 建一个外部表

![TIM截图20181114094807.png](https://upload-images.jianshu.io/upload_images/14465950-115885454addce38.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 无法清空外部表

![TIM截图20181114095233.png](https://upload-images.jianshu.io/upload_images/14465950-2196413844b0fa92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 直接创建表时引入数据(路径是存数据文件的文件夹)

![TIM截图20181114100116.png](https://upload-images.jianshu.io/upload_images/14465950-e1117dcbec0c3b2d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114100029.png](https://upload-images.jianshu.io/upload_images/14465950-7ded49eba3d9eb78.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 不设置分割建表插入数据

![TIM截图20181114102514.png](https://upload-images.jianshu.io/upload_images/14465950-74e026fec9f1198a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114102919.png](https://upload-images.jianshu.io/upload_images/14465950-33e9737bd8860fbf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 总结

![TIM截图20181114102143.png](https://upload-images.jianshu.io/upload_images/14465950-49efe7d35f3dc149.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 建一个分区表

![TIM截图20181114111359.png](https://upload-images.jianshu.io/upload_images/14465950-c4679e323ad70a1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 直接向分区表插入数据

![TIM截图20181114111748.png](https://upload-images.jianshu.io/upload_images/14465950-22d61b5e7010709e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 正确插入

![TIM截图20181114112033.png](https://upload-images.jianshu.io/upload_images/14465950-4a672fe5b9b1752b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 分区表目录结构

![TIM截图20181114112143.png](https://upload-images.jianshu.io/upload_images/14465950-7f98382dbfb1d2f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114112131.png](https://upload-images.jianshu.io/upload_images/14465950-ab8c8de8a03ae5b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 分区表方便查询

![TIM截图20181114112546.png](https://upload-images.jianshu.io/upload_images/14465950-b4729b25ecc853e2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114112648.png](https://upload-images.jianshu.io/upload_images/14465950-e122e43a96e0705e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114112817.png](https://upload-images.jianshu.io/upload_images/14465950-544e931a3150c284.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 查看表分区

![TIM截图20181114112855.png](https://upload-images.jianshu.io/upload_images/14465950-f50c815ef238c68e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 建一个两层分区的表插入数据

![TIM截图20181114113254.png](https://upload-images.jianshu.io/upload_images/14465950-2cc322dfa0089ae1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114113820.png](https://upload-images.jianshu.io/upload_images/14465950-ba4a382386475013.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114113836.png](https://upload-images.jianshu.io/upload_images/14465950-bc1b02345984db13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 修改表

## 修改表名

![TIM截图20181114140814.png](https://upload-images.jianshu.io/upload_images/14465950-5afe69a0264f995b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 添加表字段

![TIM截图20181114140929.png](https://upload-images.jianshu.io/upload_images/14465950-0fd7247e8fedde61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 修改表字段名

![TIM截图20181114141052.png](https://upload-images.jianshu.io/upload_images/14465950-f85e89305be84d69.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 重置表字段

![TIM截图20181114141316.png](https://upload-images.jianshu.io/upload_images/14465950-b8732a0d576b4669.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 给一个表添加分区

### 普通表

![TIM截图20181114141717.png](https://upload-images.jianshu.io/upload_images/14465950-c652a79f67eeefef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 分区表

![TIM截图20181114142028.png](https://upload-images.jianshu.io/upload_images/14465950-6201bea8c211ecc5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 删除表分区(注意满足条件的都会删除,所以多层分区只删一个要写全条件)

![TIM截图20181114143139.png](https://upload-images.jianshu.io/upload_images/14465950-20a358e0df9ce5b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 向表里插入一条数据(通过MapReduce)

![TIM截图20181114144344.png](https://upload-images.jianshu.io/upload_images/14465950-e24bf44d208476f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 如果出现如下情况说明hive配置出问题了

![TIM图片20181114144719.png](https://upload-images.jianshu.io/upload_images/14465950-224bc7a4dc7fdda7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 使用内置函数

![TIM截图20181114145924.png](https://upload-images.jianshu.io/upload_images/14465950-85ee820eab5192c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## insert 插入数据存储文件

![TIM截图20181114150321.png](https://upload-images.jianshu.io/upload_images/14465950-1a0dbd2b0b0e2c6b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 通过查询其他表数据向表里插入数据

![TIM截图20181114162418.png](https://upload-images.jianshu.io/upload_images/14465950-61b1a03b2363e9c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 用已有表数据建新表

![TIM截图20181114162947.png](https://upload-images.jianshu.io/upload_images/14465950-c45d9ca0f8a088a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 向分区表内直接插入数据报错

![TIM截图20181114171907.png](https://upload-images.jianshu.io/upload_images/14465950-5beb2a5b05cce363.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 设置动态分区插入数据(最后一字段默认作为分区)

![TIM截图20181114172142.png](https://upload-images.jianshu.io/upload_images/14465950-b54b6555686a3249.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181114210034.png](https://upload-images.jianshu.io/upload_images/14465950-3ccd1c1aae7e88e0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 总结

![TIM截图20181114175313.png](https://upload-images.jianshu.io/upload_images/14465950-05c162f925dfaad6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


