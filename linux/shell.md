# shell

## shell基础

### shell基本格式

	#!/bin/bash
	echo “hello world!”
	
### shell执行方式

- sh方式
- source方式 (source命令也称为“点命令”，也就是一个点符号.)
- 直接执行该脚本文件
	./test.sh (注意，一定要写成 ./test.sh，而不是 test.sh)
	
## Base简介

	Bash（ Bourne Again SHell）是GNU计划的一个组件，与Unix上
	的Bourne Shell完全兼容，是其增强版本；支持命令行输入、操
	作历史、快捷键、输入输出重定向、管道、变量等功能。
	
### history

	在Bash中输入history指令可以查询用户的过往操作历史命令会默
	认保存1000条，可以在环境变量配置文件中/etc/profile进行修改
	History表存储在内存中，在用户logout时会记录入用户家目录的
	.bash_history文件中，在下次login时载入
	
	-c：清除历史命令
	-w：把缓存中的历史命令写入历史命令保存文件  保存位置：
		~/.bash_history

### tab

	在bash中，命令与文件补全是非常方便与常用的功能,我们只需要
	在输入命令或者文件时，按“Tab”就会自动补全。
	连续两下[Tab] 可以输出以前面字母开头的所有命令
	
### alias(别名)

![TIM截图20181023094215.png](https://upload-images.jianshu.io/upload_images/14465950-79843df0f7c5ba6a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	用户可以键入alias指令，来查询当前已经定义的alias列表；
	用户也可以用unalias来取消一条别名记录；
	
### | 管道符
	
	将左侧的命令输出结果，作为右侧命令的处理对象
	例如 [root@master ~]# cat test.txt | wc -l

### 通配符

	* 代表 0 个到无穷多个任意字符 
	？ 代表一定有一个任意字符
	[] 代表一定有一个在括号内的字符(非任意字符)。例如 [abcd] 代
	表一定有一个字符， 可能是 a, b, c, d 这四个任何一个 。
	[ - ]若有减号在中括号内时，代表在编码顺序内的所有字符。例如
	[0-9] 代表 0 到 9 之间的所有数字，因为数字的语系编码是连续的！
	[^]若中括号内的第一个字符为指数符号 (^) ，那表示反向选择，例
	如 [^abc] 代表 一定有一个字符，只要是非 a, b, c 的其他字符就
	接受的意思.
	
### 常用热键

	Ctrl + d  输入已结束
	Ctrl + c   键盘中断请求
	Ctrl + s  暂停屏幕输出
	Ctrl + q  恢复屏幕输出
	Ctrl + l  清屏，相当于clear
	Tab     自动补完命令行与文件名
	Ctrl + u  删除当前光标前的所有字符
	Ctrl + k  删除当前光标后的所有字符
	
### cut 截取命令

	功能说明：显示文件中的某一列
	语法： cut  <选项>   文件
	常用选项
	-d:指定分隔符
	-f:依据 -d 的分隔字符将一段信息分割成为数段，用 -f 取出第几段的意思
	-c:指定几个字符对应的列
	例如 将PATH变量取出，找出第三和第五个路径
	[root@master ~]# echo $PATH | cut -d ':' -f 3,5 /usr/sbin

## shell编程

### shell中的变量

	Linux Shell中的变量分为“系统变量”和“用户自定义变量”，可以通过set命令
	查看那系统变量
	系统变量：$HOME、$PWD、$SHELL、$USER等等
	显示当前shell中所有变量 : set

#### 自定义变量

	格式：变量名=变量值
	规则
	变量与变量内容以一个等号来连结
	等号两侧不能有空格
	变量名以字母或下划线开头，区分大小写，建议全大写
	STR="hello world"
	A=9
	unset A 撤销变量 A
	readonly B=2 声明静态的变量 B=2 ，不能 unset
	export 变量名 可把变量提升为全局环境变量，可供其他shell程序使用

#### 赋值时使用引号

	双引号：允许通过$符号引用其变量值
	单引号：禁止引用其他变量值，$视为普通字符
	反撇号：命令替换，提取命令执行后的输出结果，也可用$(命令)
	从键盘输入内容变为赋值
	read -p(提示语句)-n(字符个数) -t(等待时间)
	将命令的返回值赋给变量 A=$(ls -la)
	
#### 特殊变量

	$#：表示参数的个数，常用于循环
	$*：参数的内容
	$$：当前shell进程的pid值
	$?：前一命令返回的状态值（0为正常）
	$0 表示当前脚本名称
	$1 第一个参数
	$N 第N个参数

### 算数运算
	
	格式：expr  变量1   运算符  变量2  [运算符 变量3] ...
	例如
	计算（2+3）x4的值
	[root@master~]# expr $(expr 2 + 3) \* 4

### test命令

	测试特定的表达式是否成立，当条件成立时，测试语句的返回值为0，
	否则为其他数值
	test  条件表达式
	[  条件表达式  ]
	
#### 文件测试

	格式：[  操作符  文件或目录  ]    注意condition前后要有空格
	常用的测试操作符
	-d：测试是否为目录（Directory）
	-e：测试目录或文件是否存在（Exist）
	-f：测试是否为文件（File）
	-b:  该文件是否存在且为一个块设备文件
	-c:  该文件是否存在且为一个字符设备文件
	-S: 该文件是否存在且为一个Socket文件
	-p:  该文件是否存在且为一个FIFO(pipe)文件
	-L:  该文件是否存在且为一个链接文件
	
![TIM截图20181023141100.png](https://upload-images.jianshu.io/upload_images/14465950-f229ced67d31e13f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181023141441.png](https://upload-images.jianshu.io/upload_images/14465950-76f9c29da17bc146.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181023142116.png](https://upload-images.jianshu.io/upload_images/14465950-de272803eaa0dc1d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 文件权限测试

	格式：[  操作符  文件或目录  ]
	常用的测试操作符
	-r：测试当前用户是否有权限读取（Read）
	-w：测试当前用户是否有权限写入（Write）
	-x：测试当前用户是否有权限执行（eXcute）
	-u： 测试该文件是否存在且具有suid属性
	-g： 测试该文件是否存在且具有sgid属性
	 -k： 测试该文件是否存在且具有sticky bit属性
	-s ：测试该文件是否存在且为非空文件

![TIM截图20181023142825.png](https://upload-images.jianshu.io/upload_images/14465950-71028f993db4acfe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 数值比较

	格式：[  整数1  操作符  整数2  ]
	常用的测试操作符
	-eq：等于（Equal）
	-ne：不等于（Not Equal）
	-gt：大于（Greater Than）
	-lt：小于（Lesser Than）
	-le：小于或等于（Lesser or Equal）
	-ge：大于或等于（Greater or Equal）

![TIM截图20181023143656.png](https://upload-images.jianshu.io/upload_images/14465950-0bb64b3e0cc85d3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181023143834.png](https://upload-images.jianshu.io/upload_images/14465950-5c92a0b2ed629521.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 字符串比较

	格式
	[  字符串1  =  字符串2 ]
	[  字符串1  !=  字符串2 ]
	[  -z  字符串 ]字符串内容为空
	常用的测试操作符
	=：字符串内容相同
	!=：字符串内容不同，! 号表示相反的意思
	
![TIM截图20181023144654.png](https://upload-images.jianshu.io/upload_images/14465950-78a2d16dfa5d9dc5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181023144941.png](https://upload-images.jianshu.io/upload_images/14465950-34fa5a57e51070e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181023150026.png](https://upload-images.jianshu.io/upload_images/14465950-f2d01b6fcc5b20f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### if语句结构

![TIM截图20181023210941.png](https://upload-images.jianshu.io/upload_images/14465950-07c44f9597529451.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181023211007.png](https://upload-images.jianshu.io/upload_images/14465950-24252ca4d14fb630.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181023211029.png](https://upload-images.jianshu.io/upload_images/14465950-3aa6beab70838beb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### case语句结构

![TIM截图20181023211103.png](https://upload-images.jianshu.io/upload_images/14465950-dc94f5a0d917ca91.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### for语句结构

![TIM截图20181023211134.png](https://upload-images.jianshu.io/upload_images/14465950-f61e41b0dbab9d7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![TIM截图20181023211148.png](https://upload-images.jianshu.io/upload_images/14465950-4cabc80b377478ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### while语句的结构

![TIM截图20181023211228.png](https://upload-images.jianshu.io/upload_images/14465950-dc446e1c3ded2f9b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Shell自定义函数

![TIM截图20181023211259.png](https://upload-images.jianshu.io/upload_images/14465950-eaa27522a52ff11c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[shell 括号](https://blog.csdn.net/liweigao01/article/details/78669674)
	


	
	