## Docker基础
### Docker基本知识
1. docker是什么
	&emsp;&emsp;docker容器相当于是虚拟机，但是共用一套系统的底层核心，且去掉了对硬件的模拟，所以比虚拟机小得多，且启动快得多。容器采用沙箱机制，相互之间不会有任何接口。
2. docker结构
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Docker基础_1.png)
	**registry（仓库）：**和代码远程仓库一样（叫做dockerhub），只是放的不是代码，是应用镜像`images`。
	**doker_host（服务器）：**相当于是我们的主机，里面也有镜像`images`，是我们从远程下载下来的，镜像有什么用呢？镜像相当于是个模板，当我们要创建容器`containers`，假设启动一个tomcat应用，我们不需要每次都去远仓库下载，只要我们下载了一次在本地，后面主机就能根据这个镜像生成应用，用在容器里。此外，这个主机还有一个docker的守护进程`docker daemon`，所谓守护进程其实就是后台程序，进行数据命令信息监控的，比如httpd、phpd这种末尾带d的，都是守护进程。docker守护进程的作用就是监控客户端`client`发来的指令，并执行。
	**client（控制台）：**其实就是在命令行输入命令，操作容器，通过socket与主机守护进程通讯。
### Docker安装
1. 直接看官方文档
	https://docs.docker.com/engine/install/centos/
	大致步骤是：
	卸载旧版本：不管下载过没有
	```
	yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
	```
	安装
	```
	yum install -y yum-utils
	```
	设置镜像的仓库：阿里云的，国外的慢
	```
	yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo 
	```
	更新yum软件包索引
	```
	yum makecache fast
	```
	安装docker相关的配置：ce代表社区版
	```
	yum install docker-ce docker-ce-cli containerd.io
	```
	启动Docker
	```
	systemctl start docker
	# 查看当前版本号，是否启动成功
	docker version
	# 设置开机自启动
	systemctl enable docker
	```
### Docker卸载
1. 卸载依赖
	```
	yum remove docker-ce docker-ce-cli containerd.io
	```
1. 删除资源：/var/lib/docker是docker的默认工作路径
	```
	rm -rf /var/lib/docker
	```
### Docker镜像加速
1. 说明：
	&emsp;&emsp;我们虽然配置了国内的dockerhub，但是其实还可以加速。如果你配置的是腾讯的镜像库，你的云服务器也是在腾讯云上，就可以通过腾讯的镜像加速生成的地址替换原来的公有镜像地址实现进一步加速。阿里云也是一样的。不过我觉得麻烦没弄。
### Docker指令流程
1. 执行`docker run hello_world`过程：我们运行hello_world这个镜像，命令发给守护进程，守护进程检查本地有无该镜像，没有就去远程仓库下载，远程都没有就报错，有就下载并执行命令。
## Docker命令
### 基础命令
1. 如下：
	```
	docker version          #查看docker的版本信息
	docker info             #查看docker的系统信息,包括镜像和容器的数量
	docker 命令 --help       #帮助命令(可查看可选的参数)
	```
### 镜像命令
1. 查看镜像：红框内的就是镜像名
	```
	docker images
	# 可选参数
	docker images -a/--all           # 列出所有镜像
	docker images -q/--quiet         # 只显示镜像的id
	```
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Docker基础_2.png)

1. 查看搜索：也就是在dockerhub网站的搜索框里面搜索
	```
	docker search mysql   # 这里示例mysql
	# 可选参数
	docker search mysql -f/--filter=STARS=3000     # 搜索收藏数大于3000的镜像源
	```
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Docker基础_3.png)

	在dockerhub网站搜索：
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Docker基础_4.png)
1. 下载镜像：根据上面搜索到的NAME
	```
	docker pull mysql         # 默认最新（latest）版本
	docker pull mysql:5.7     # 指定版本：版本必须是库里有的
	```
1. 删除镜像：有运行的容器删不了
	```
	# 删除指定的镜像id
	docker rmi -f  镜像id
	# 删除多个镜像id
	docker rmi -f  镜像id 镜像id 镜像id
	# 删除全部的镜像id
	docker rmi -f  $(docker images -aq)
	```
### 容器命令
1. 运行容器：容器关闭相当于睡眠，不影响唤醒和内部数据
	```
	docker pull centos      # 这里示例centos镜像生成容器
	docker run -d centos    # 后台方式运行，需要注意的是容器后台运行必须要有前台进程，不然容器会关闭
	docker run -it centos   # 使用交互方式运行,进入容器查看内容(关闭退出是`exit`，不关闭退出是快捷键Ctrl + p + q)
	docker run -it centos /bin/bash    # 进入entos容器后运行bash，即运行一个前台进程
	docker run -p 3344:80 centos    # 指定容器的端口(`-p 主机端口:容器端口`)
	docker run -d --name mycentos centos   # 取名mycentos
	```
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Docker基础_5.png)
1. 查看容器
	```
	docker ps        # 显示正在运行的容器
	docker ps -q     # 显示正在运行的容器的id
	docker ps -a     # 显示所有容器
	docker ps -n=2   # 显示最近创建的2个容器（可以是其他数量）
	```
1. 删除容器
	```
	docker rm 容器id                  # 不能删除在在运行的容器，除非加`-f`
	docker rm -f $(docker ps -q)     # 删除所有正在运行的容器
	docker rm -f $(docker ps -aq)    # 删除所有容器
	```
1. 启动和关闭容器
	```
	docker start 容器id              # 启动容器
	docker stop 容器id               # 关闭容器
	docker restart 容器id            # 重启容器
	docker kill 容器id               # 强制关闭容器（关闭报错的时候可以用）
	```
1. 查看容器日志
	```
	docker run -d centos /bin/sh -c "while true;do echo hello!;sleep 5;done"  # 首先运行centos容器，并执行一个不停打印的脚本，用来产生日志
	docker logs -tf 容器id          # 查看所有日志,`-t`显示时间，`-f`实时显示
	docker logs -tail 10 容器id     # 查看最后10条日志（一般要和上面的合起来用）
	```
1. 查看容器内的进程
	```
	docker top 容器id
	```
1. 查看容器元数据
	```
	docker inspect 容器id
	```
1. 进入容器：两种
    - 进入容器但新进程
	```
	docker exec -it 容器id /bin/bash   # 有点像同一个电脑双开了一个软件
	docker attach 容器id               # 进入的就是容器中运行的进程
	```
1. 从容器中拷贝数据到主机
	```
	docker cp 容器id:/home/test.txt /root # 前面是容器内文件路径，后面是主机路径
	```