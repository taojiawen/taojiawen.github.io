#awk 行读取命令
### 格式 awk 选项 command file
	 
	 -F 设置分隔符 默认根据" "空格来分割
	 NR 行号
	 NF (根据分隔符)列数
	 print
	 printf
	 
![TIM截图20181022160030.png](https://upload-images.jianshu.io/upload_images/14465950-d47a1c7588b3df01.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	 
![TIM截图20181022160836.png](https://upload-images.jianshu.io/upload_images/14465950-8eda3b7ecccd987a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	 
![TIM截图20181022161448.png](https://upload-images.jianshu.io/upload_images/14465950-6bd974988e61b931.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	 
	 
	 
	 要使用正则: ~/正则表达式/
	 
![TIM截图20181022162523.png](https://upload-images.jianshu.io/upload_images/14465950-959e379ba214288b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	 
	 如果用!~就是对正则匹配的内容取非
	 
![TIM截图20181022162704.png](https://upload-images.jianshu.io/upload_images/14465950-0cf11a22fa950fd2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	 
	 awk扩展格式
	 awk 选项 'BEGIN{} command END{}' file
	 
![TIM截图20181022163906.png](https://upload-images.jianshu.io/upload_images/14465950-af5eaad30e198d97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181022165050.png](https://upload-images.jianshu.io/upload_images/14465950-1f68e7f0c3cf3655.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181022171821.png](https://upload-images.jianshu.io/upload_images/14465950-bd0b795bcf7d815d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181022171121.png](https://upload-images.jianshu.io/upload_images/14465950-022c34c6eb66a68e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181022165250.png](https://upload-images.jianshu.io/upload_images/14465950-35bbf776268a47fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
