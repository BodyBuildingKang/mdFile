

# CentOS8 docker 安装

##  切换到root 用户下



##   第一步 卸载旧的安装包

 yum remove docker \

​         docker-client \

​         docker-client-latest \

​         docker-common \

​         docker-latest \

​         docker-latest-logrotate \

​         docker-logrotate \

​         docker-engine

​         

##   第二步  安装需要的安装包

yum install -y yum-utils

##    第三步 设置镜像的仓库

 yum-config-manager \

  --add-repo \

  https://download.docker.com/linux/centos/docker-ce.repo  --默认是国外的

\#如果没有vpn 建议安装阿里云的   

yum-config-manager \

 --add-repo \

 http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

##    更新yum 索引安装包

yum makecache fast （CentOS8 没有fast参数 需要去掉）

##    安装docker相关的

 yum install docker-ce docker-ce-cli containerd.io (可能会出错，多试几次)

##    启动docker 服务

 systemctl start docker

##   查看docker 是否安装完成

 docker --version

 \#通过hello world 来验证

 docker run hello-world

##   查看所有的docker 镜像

 docker images

##   注意点

1. ### 配置daemon.json

2. 必须在root权限 才能连接成功

3. 

#  Docker卸载

##  卸载依赖

yum remove docker-ce docker-ce-cli containerd.io

##  删除资源

rm -rf /var/lib/docker

# docker相关指令

docker基本命令：

1. 查看所有镜像 docker images

2. 删除镜像(会提示先停止使用中的容器) docker rmi 镜像name/镜像id

3. 查看所有容器 docker ps -a

4. 查看容器运行日志 docker logs 容器名称/容器id

5. 停止容器运行 docker stop 容器name/容器id

6. 终止容器后运行 docker start 容器name/容器id

7. 容器重启 docker restart 容器name/容器id

8. 删除容器 docker rm  -f 容器name/容器id 

9. 删除镜像
   1. docker rmi -f 镜像id (可以根据 docker images 查询)
   2. docker rmi -f $(docker images) --删除所有镜像

10. 查询docker 的详细信息 docker stats dockerid

11. 停止一个正在运行的容器 
    1. docker stop 此方式常常被翻译为优雅的停止容器
    2. docker stop 容器ID或容器名 
    3. 参数 -t：关闭容器的限时，如果超时未能关闭则用kill强制关闭，默认值10s，这个时间用于容器的自己保存状态 
    4. docker stop -t=60 容器ID或容器名
    5. docker kill  【docker kill 容器ID或容器名 :直接关闭容器】
    6. 由此可见stop和kill的主要区别:stop给与一定的关闭时间交由容器自己保存状态，kill直接关闭容器

想更进一步了解处理机制的可以看下面这篇文章，比较详细但是需要其他方面的 

11. 停用全部运行中的容器:  docker stop $(docker ps -q) 

12. 删除全部容器：docker rm $(docker ps -aq) 

13. 一条命令实现停用并删除容器：docker stop $(docker ps -q) & docker rm $(docker ps -aq)



