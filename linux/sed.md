#sed命令

###格式:sed 选项 动作 filename

###选项

	 -n (使用安静(silent)模式。被处理的行才会在命令行打印)

###动作

- a 往下一行新增
![TIM截图20181022191629.png](https://upload-images.jianshu.io/upload_images/14465950-8d3310f411f2a7fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- i	往上一行新增
	用法与a类似
- c 替换(1,5c会将这一块区域整个替换，不会每行都替换) 

![TIM截图20181022192711.png](https://upload-images.jianshu.io/upload_images/14465950-64c6ea4e8813ff98.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- d 删除

![TIM截图20181022110522.png](https://upload-images.jianshu.io/upload_images/14465950-18293410c4bd731a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- p 输出 (多和 -n 一起使用)
- w 写入 sed 'w 要被写入的文件(目标文件)' 读取内容的文件(源文件)只要是w向文件
	中进行写入就会将目标文件之前的内容全部干掉
- r 读取 sed '2r 要读取的文件' 加入数据的文件(目标文件)

- s 替换经常配合正则进行操作

![TIM截图20181022111819.png](https://upload-images.jianshu.io/upload_images/14465950-602a09a2072d7c33.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 高级操作
	 | 管道符,使用该符号配合其他命令
	 {} 可以让sed执行多个动作,只是动作之间要用";"分号隔开
	 &替换 
 	 &相当于占位符的作用 就是我们 s/查询条件/查询到的内容
	 可以在s/查询条件/要替换成的内容中进行使用,实现追加的效果
	 \u转成大写可以配合我们的&来实现将匹配内容转换成大写的操作
	 
![TIM截图20181022114542.png](https://upload-images.jianshu.io/upload_images/14465950-fac7da2c2f3adebd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	 
	 ()分组功能
	 获取分组的内容
	 首先分组的序号是从1开始的并且按照从左到右的顺序排的
	 要获取使用\分组的序号来获取,例如\1就是占位符
	 
![TIM截图20181022141939.png](https://upload-images.jianshu.io/upload_images/14465950-0307d235885b9e42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

