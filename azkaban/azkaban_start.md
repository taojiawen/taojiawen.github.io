# azkaban����

1.����ѹ������ѹ�ŵ�һ���ļ����ºù���

2.MySQL��ִ��sql���

![TIM��ͼ20181121095802.png](https://upload-images.jianshu.io/upload_images/14465950-147874b28ef63e80.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.1���ݿ������ɱ�

![TIM��ͼ20181121110815.png](https://upload-images.jianshu.io/upload_images/14465950-e858e16797a25f42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.ssl����(�����ס����Ҫ��)

![TIM��ͼ20181121100554.png](https://upload-images.jianshu.io/upload_images/14465950-0f326339302f4333.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.���ɵ�keystore�ŵ�web��

	keytool -keystore keystore -alias jetty -genkey -keyalg RSA

![TIM��ͼ20181121100729.png](https://upload-images.jianshu.io/upload_images/14465950-7da6fec589fd01b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.����web����proprerties�ļ�

![TIM��ͼ20181121100915.png](https://upload-images.jianshu.io/upload_images/14465950-7561fa2d57dbb63d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.1�޸�ʱ��

	Asia/Shanghai

![TIM��ͼ20181121101440.png](https://upload-images.jianshu.io/upload_images/14465950-0f7455ab06289c6c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.2�޸�MySQL����

![TIM��ͼ20181121101419.png](https://upload-images.jianshu.io/upload_images/14465950-c2f197b403e46fab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.3�޸�ssl����(֮ǰ���õ�����)

![TIM��ͼ20181121101535.png](https://upload-images.jianshu.io/upload_images/14465950-bf1c4e256d2da974.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6.����web����users�ļ�

	<user username="admin" password="admin" roles="admin,metrics" />

![TIM��ͼ20181121101945.png](https://upload-images.jianshu.io/upload_images/14465950-88ed1667da9ac818.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7.����executorִ����

![TIM��ͼ20181121102117.png](https://upload-images.jianshu.io/upload_images/14465950-dd22192e0964e068.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7.1����proprerties�ļ�

![TIM��ͼ20181121102257.png](https://upload-images.jianshu.io/upload_images/14465950-0925540140587b18.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8.����executor����

![TIM��ͼ20181121102341.png](https://upload-images.jianshu.io/upload_images/14465950-0b4756e0745d7847.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8.1�ڴ����ļ����²���ִ��

![TIM��ͼ20181121102502.png](https://upload-images.jianshu.io/upload_images/14465950-0a895d8cff31b512.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8.2 ��executor��Ŀ¼�������·��ִ��

![TIM��ͼ20181121102703.png](https://upload-images.jianshu.io/upload_images/14465950-b387f8e6b520dd93.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

9.����web����

![TIM��ͼ20181121102818.png](https://upload-images.jianshu.io/upload_images/14465950-2ba059b80e970a6e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM��ͼ20181121102908.png](https://upload-images.jianshu.io/upload_images/14465950-291550f248e0d082.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

ps ���������ɹ�

![TIM��ͼ20181121103022.png](https://upload-images.jianshu.io/upload_images/14465950-72ae8eccdc67921a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

10.���������(ע����HTTPS �˿�8443)

![TIM��ͼ20181121103122.png](https://upload-images.jianshu.io/upload_images/14465950-329eafe8a328f864.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

10.1��¼����������������õĳ����û�

![TIM��ͼ20181121103142.png](https://upload-images.jianshu.io/upload_images/14465950-e5dd78a90ff04c67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

11.�½�����

![TIM��ͼ20181121113841.png](https://upload-images.jianshu.io/upload_images/14465950-9afc6ecaa23bc97f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

12.�ϴ�����

![TIM��ͼ20181121111640.png](https://upload-images.jianshu.io/upload_images/14465950-70bb046701079f25.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

12.1�ϴ��ı�����zip��ʽ��ѹ����(.job�ļ�)

![TIM��ͼ20181121111750.png](https://upload-images.jianshu.io/upload_images/14465950-48989b713ee8c5ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

13.ִ�й���

![TIM��ͼ20181121112030.png](https://upload-images.jianshu.io/upload_images/14465950-b53a9a3dfd7953b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM��ͼ20181121112132.png](https://upload-images.jianshu.io/upload_images/14465950-63b9969384573ea3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

14.�鿴����

![TIM��ͼ20181121112300.png](https://upload-images.jianshu.io/upload_images/14465950-04e85bc105f27c4b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

����1(����)

		start.job
		
		type=command
		command=echo start
		
		end.job
		
		type=command
		dependencies=start
		command=echo end
		
����2(����hdfs)

		hdfs.job

		type=command
		command=hadoop fs -mkdir /azkaban
		
	ִ��������ļ��� 	
	
![TIM��ͼ20181121115051.png](https://upload-images.jianshu.io/upload_images/14465950-3c819c61c32f696a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
		
		
		