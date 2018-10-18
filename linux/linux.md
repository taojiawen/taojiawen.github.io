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
- 内部命令：属于Shell解析器的一部分
- cd 切换目录（change directory）
	- ./ :当前目录
	- ../:上层目录
- pwd 显示当前工作目录（print working directory）
- help 帮助
	外部命令：独立于Shell解析器之外的文件程序
    ls 显示文件和目录列表（list）
    - -l：详细信息显示
	- -a：显示所有子目录和文件的信息，包括隐藏文件
	- -A：类似于“-a”，但不显示“.”和“..”目录的信息
	- -R：递归显示内容
- mkdir 创建目录（make directoriy）
	-p: 可以创建路径全部文件夹 
- cp 复制文件或目录（copy）
	- -r：递归复制整个目录树
	- -p：保持源文件的属性不变
	- -f：强制覆盖目标同名文件或目录
	- -i：需要覆盖文件或目录时进行提醒
- 查看帮助文档
    - 内部命令：help + 命令（help cd）
    - 外部命令：man + 命令（man ls）
- du 统计目录及文件的空间占用情况
	- -a：统计时包括所有的文件，而不仅仅只统计目录
	- -h：以更易读的字节单位（K、M等）显示信息
	- -s：只统计每个参数所占用空间总的大小
- touch命令
	- 新建空文件
	- > 用法相同
	- echo "内容" >> 文件名 (往文件里输出,文件不存在直接创建)
- file命令 查看文件类型
- rm命令
	-f：强行删除文件，不进行提醒
	-i：删除文件时提醒用户确认
	-r：递归删除整个目录树





