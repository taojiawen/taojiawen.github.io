# 完整hadoop分布式

### 准备工作

虚拟机 hadoop 用户 visudo

yum install -y (vim net-tools)

/home/hadoop 下有 hadoop.gz jdk.gz

systemctl stop firewalld

作为namenode

克隆三个作为datanode

### 开始配置

配置namenode为伪分布式参照上一篇

[环境搭建](http://taojiawen.github.io/hadoop/config)

vim ~/hadoop-2.7.3/etc/hadoop/slaves

加入datanode ip地址

datanode同样配置为单节点hadoop

只要 datanode 路径与 namenode 一致 可以

scp -r 想传的文件 用户名@ip地址:目标地址

把namenode的配置传给DataNode

sudo vim /etc/hosts 把ip namenode ip datanode(datanode别名需要不同) 写入

此时就可以在namenode开启datanode的dfs和yarn 但是需要反复输入密码

so

ssh-keygen生成密钥(过程回车即可)

ssh-copy-id 用户名@IP地址 把公钥发给datanode

ssh-copy-id localhost 设置本地免密

到这里已经生成并追加完成

ps

authorized_keys:存放远程免密登录的公钥,主要通过这个文件记录多台机器的公钥

id_rsa : 生成的私钥文件

id_rsa.pub ： 生成的公钥文件

know_hosts : 已知的主机公钥清单

![1.jpg](https://upload-images.jianshu.io/upload_images/14465950-db7a7be76e591951.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 




