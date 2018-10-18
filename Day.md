# First Day
## Afternoon
### Linux的一些基础命令
	1. pwd 查看当前位置
	2. cd 路径   进入路径
	3. cd ~  进入当前用户的家目录
	4. cd /  回到root的根目录
	5. ls  查看当前路径下所有文件
	6. mkdir 文件夹名称    创建文件夹
	7. touch 文件名称      创建文件
	8. echo "内容" >> 文件名称     讲内容写进文件中如果文件不存在的话先创建后写入
	9. rm -rf 文件名称      删除此文件（如果文件名称为 * 则删除此目录下所有文件）

### Git命令
	1. ssh-keygen -t rsa -C "邮箱"   生成ssh 密钥，输入命令后，连按三个回车即可生成ssh 密钥  
	2. git clone + ssh路径  克隆ssh的密钥
	3. touch lpl.md 创建格式为目的的文件
	4. git status 命令用于显示工作目录或暂存区状态
	5. git add lpl.mp 讲lpl.md 添加到暂存区
	6. git commit -m "forst commit" 放到名为"first commit"的本地库中
	7. git config --global user.email "2578987146@qq.com"  登录邮箱
	   git config --global user.name "0LiBingYang0"		   登录用户名
	8. git push -u origin master  提交文件到服务器