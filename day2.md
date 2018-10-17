git命令

git clone 仓库地址

git add 文件路径,=让创建出来的文件告诉git仓库要添加

git commit -m "要提交的内容是什么  -- 提交日志" 将我们做的操作提交到本地git仓库

git push -u origin master （第一遍这么写，目的是设置以后默认都是往master分支上提交代码）

git push 用完以后这么写就可以


echo "Hello World" >> aaa.md 把Hello World 写进aaa.md 有的话直接写进去,没有的话先创建后写

堆 先进先出

栈 先进后出

Li.md ll echo hhh github   1.1	

ll echo aaa local    1.2

git stash

存在栈中 1.2

local 1.1

git pull

git stash pop 出栈

local hhh aaa 代码冲突

git多人合作

git init 初始化git仓库(.git文件夹的生成)


刚开始初始化出来的git仓库是不知道要推送的远端git仓库是谁的

所以需要我们通过该命令告诉他跟哪个远程仓库连接

1.github 创建一个用于多人合作的git仓库

2.推送1.0版本的代码,内容到我们的仓库当中

3.默认情况下那个账号创建的仓库只有本人能提交东西,如果想要多人开发需要邀请别人成为协作者
