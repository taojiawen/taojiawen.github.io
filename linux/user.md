# Linux 用户

## 配置文件

- 保存用户信息的文件：/etc/passwd	
- 保存密码的文件：/etc/shadow
- 保存用户组的文件：/etc/group
- 保存用户组密码的文件：/etc/gshadow
- 用户配置文件：/etc/default/useradd

## 用户在系统中是分为角色的，通过UID来识别角色

	root用户，系统唯一，可以操作系统任何文件和命令，拥有最高权限，UID=0 
	虚拟用户(系统账户)，不具有登录系统能力，但却是系统运行不可缺少的用户。如：bin、daemon、ftp、mail等，UID为1---499之间
	普通真实用户，可以登录系统，权限有限，靠管理员创建，UID为500—60000之间

## 系统账户

- 1 – 99：由distributions自行创建的系统账号
- 100 – 499：若用户有系统账号需求时，可以使用的UID

### 为了更好的管理用户，出现组group的概念

	基本组（私有组） 当用户创建文件和文件夹时，默认属于私有组
	附加组（公共组）

# 用户管理

## 用户管理配置文件

### 用户账号文件--/etc/passwd

![TIM截图20181018212652.png](https://upload-images.jianshu.io/upload_images/14465950-55fd4b1d6bd150af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
### 用户密码文件--/etc/shadow

![TIM截图20181018212830.png](https://upload-images.jianshu.io/upload_images/14465950-6b6c32df1a1ae3c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 用户管理命令

### useradd 添加用户命令

- -u 指定组ID（uid）
- -g 指定所属的组名（gid）
- -G 指定多个组，用逗号“，”分开（Groups）
- -c 用户描述（comment）
- -e 失效时间（expire date）

### passwd 设置密码

- -d：清空用户的密码，使之无需密码即可登录
- -l：锁定用户帐号
- -S：查看用户帐号的状态（是否被锁定）
- -u：解锁用户帐号
- -x:    最大密码使用时间（天）
- -n:    最小密码使用时间（天）

### usermod 修改已有用户属性

- -l 修改用户名 （login）usermod -l a b（b改为a）
- -g 添加组 usermod -g sys tom
- -G添加多个组 usermod -G sys,root tom
- –L 锁定用户账号密码（Lock）
- –U 解锁用户账号（Unlock）

### userdel 删除用户命令
 
- -r 删除账号时同时删除目录（remove）

# 组管理

## 组管理配置文件

### 用户组文件：/etc/group

![TIM截图20181018213530.png](https://upload-images.jianshu.io/upload_images/14465950-79f4784095090891.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 用户组密码文件： /etc/gshadow

![TIM截图20181018213625.png](https://upload-images.jianshu.io/upload_images/14465950-ef96b6e3c26003df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 组命令管理

### groupadd 添加组账号

-g 指定gid
 
### groupmod 修改组

- -g：设置想要使用的GID
- -o：使用已经存在的GID
- -n：设置想要使用的群组名称

### gpasswd 设置组帐号密码（极少用）、添加/删除组成员

- -a：向组内添加一个用户
- -d：从组内删除一个用户成员
- -M：定义组成员列表，以逗号分隔

### groupdel 删除组账号

	 注意：只能删除那些没有被任何用户指定为主组的组。
		   显示用户所属组

### groups 查看当前组

		   