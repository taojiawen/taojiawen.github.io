# Linux 常用指令

### 1.重启命令

- reboot	
- shutdown -r now 立刻重启(root用户使用)
- shutdown -r 10 过十分钟自动重启(root用户使用)
- shutdown -r 20:12 在时间为20:12重启(root用户使用)
- 如果是通过shutdown命令设置重启的话,可以用shutdown -c命令取消重启
	
### 2.关机命令

- halt 立即关机
- poweroff 立即关机
- shutdown -h now 立即关机(root用户使用)
- shutdown -h 10 10分钟后自动关机
	
### 3.Linux 运行级别
	
![TIM截图20181017191402.png](https://upload-images.jianshu.io/upload_images/14465950-55274248149eb9b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4.关于主机名

- hostname 查看主机名
- hostname 新主机名 (临时修改 重启后变回原来的)
- 修改配置文件 /etc/hostname文件(永久修改)
	
### 5.ping命令

- ping 目标主机
- Ctrl + C 中止测试
	
### 6.查看网络接口信息

- ifconfig命令
- ifconfig不能用 使用 yum install net-tools
	
### 7.虚拟机网络配置图
	
![图片1.png](https://upload-images.jianshu.io/upload_images/14465950-c671b21d92d4ea4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
### 8.设置防火墙

- service firewalld status 查看防火墙状态
- systemctl stop firewalld 关闭防火墙(临时关闭)
- systemctl disable firewalld (禁止开机启动)
	
### 9./etc/hosts文件

- 保存主机名与IP地址的映射记录
- 访问时先在本地查找,找不到去DNS服务器找
	
### 10.设置SELinux

- getenforce 查看状态
- setenforce	[ Enforcing | Permissive| 1| 0 ]
  该命令可以立即改变SELinux运行状态，在Enforcing 和Permissive  之间切换，关机重启之后失效。
- 修改配置文件/etc/selinux/config，将SELINUX=enforcing修改为SELINUX=disabled重启生效
	
### 11.Linux基础命令

#### 内部命令：属于Shell解析器的一部分

#### cd 切换目录（change directory）
	- ./ :当前目录
	- ../:上层目录
	
#### pwd 显示当前工作目录（print working directory）

#### help 帮助

#### 外部命令：独立于Shell解析器之外的文件程序

#### ls 显示文件和目录列表（list）

    - -l：详细信息显示
	- -a：显示所有子目录和文件的信息，包括隐藏文件
	- -A：类似于“-a”，但不显示“.”和“..”目录的信息
	- -R：递归显示内容
	
#### mkdir 创建目录（make directoriy）

	-p: 可以创建路径全部文件夹 
	
#### cp 复制文件或目录（copy）

	- -r：递归复制整个目录树
	- -p：保持源文件的属性不变
	- -f：强制覆盖目标同名文件或目录
	- -i：需要覆盖文件或目录时进行提醒
	
#### 查看帮助文档

    - 内部命令：help + 命令（help cd）
    - 外部命令：man + 命令（man ls）
	
#### du 统计目录及文件的空间占用情况

	- -a：统计时包括所有的文件，而不仅仅只统计目录
	- -h：以更易读的字节单位（K、M等）显示信息
	- -s：只统计每个参数所占用空间总的大小
	
#### touch命令

	- 新建空文件
	- `>` 用法相同
	- echo "内容" >> 文件名 (往文件里输出,文件不存在直接创建)
	
#### file命令 查看文件类型

#### rm命令

	-f：强行删除文件，不进行提醒
	-i：删除文件时提醒用户确认
	-r：递归删除整个目录树
	
#### mv命令 移动（Move）文件或目录—— 如果目标位置与源位置相同，则相当于改名

#### which命令 显示系统命令所在目录

#### find命令 

	- -name	根据文件名查找
    - -user	根据文件拥有者查找
	- -group	根据文件所属组寻找文件
	- -perm	根据文件权限查找文件
	- -size	根据文件大小查找文件
	- -type	根据文件类型查找（f-普通文件，c-字符设备文件，b-块设备文件，l-链接文件，d-目录）
	- -o	表达式或
	- -and	表达式与
	
#### cat命令 显示出文件的全部内容

#### more命令 全屏方式分页显示文件内容

	- 按Enter键向下逐行滚动
	- 按空格键向下翻一屏、按b键向上翻一屏
	- 按q键退出
	
#### less命令 与more命令相同

#### head命令 查看文件开头的一部分内容（默认为10行）

	- head -5 查看文件开头5行
	
#### tail命令 查看文件结尾的少部分内容（默认为10行）

	- tail -5 查看文件结尾5行
	
#### wc命令 统计文件中的单词数量（Word Count）等信息

	- -l：统计行数
	- -w：统计单词个数
	- -c：统计字节数
	
#### grep命令 查找文件里符合条件的字符串

	- -c:计算匹配关键字的行数
	- -i:忽略字符大小写的差别
	- -n:显示匹配的行及其行号
	- -s: 不显示不存在或不匹配文本的错误信息
	- -h: 查询多个文件时不显示文件名
	- -l:   查询文件时只显示匹配字符所在的文件名
	- --color=auto:将找到的关键字部分加上颜色显示
	- 正则表达式简单规则
		- .  : 任意一个字符
		- a* : 任意多个a(零个或多个a)
		- a? : 零个或一个a
	    - a+ : 一个或多个a
		- .* : 任意多个任意字符
		- \. : 转义.
		- o\{2\} : o重复两次
		
#### gzip 压缩（解压）文件或目录，压缩文件后缀为gz

	- -d将压缩文件解压（decompress）
	- -l显示压缩文件的大小，未压缩文件的大小，压缩比（list）
	- -v显示文件名和压缩比（verbose）
	- -num用指定的数字num调整压缩的速度，-1或--fast表示最快压缩方法（低压缩比），-9或--best表示最慢压缩方法（高压缩比）。系统缺省值为6

#### bzip2 压缩（解压）文件或目录，压缩文件后缀为bz2 

	- -c将压缩的过程产生的数据输出到屏幕上
    - -d解压缩的参数（decompress）
	- -z压缩的参数（compress）
	- -num 用指定的数字num调整压缩的速度，-1或--fast表示最快压缩方法（低压缩比），-9或--best表示最慢压缩方法（高压缩比）。系统缺省值为6

#### tar 文件、目录打（解）包

	- -c：创建 .tar 格式的包文件
	- -x：解开.tar格式的包文件
	- -v：输出详细信息
	- -f：表示使用归档文件







