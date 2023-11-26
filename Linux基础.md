<style>
.blogpost-body h2{
    font-size: 28px;
    font-weight: bold;
    height: 37px;
    border-bottom: 3px solid #000000;
	padding-top:0.3cm;
}
h3{
    background: linear-gradient(to right, #2a5caa 0%,#ffffff 100%);
    color: #FFFFFF;
    font-size: 18px;
    font-weight: bold;
    height: 30px;
    padding: 8px 0 5px 10px;
    text-shadow: 2px 2px 3px #222222;
}
h4{
    background: linear-gradient(to right, #99cc99 0%,#ffffff 100%);
	color: #003300;
    font-weight: bold;
    height: 25px;
    padding: 1px 0 5px 5px;
}
h5{
    background: linear-gradient(to right, #BEBEBE 0%,#ffffff 100%);
	color: #003300;
    /* font-weight: bold; */
    height: 17px;
    padding: 1px 0 5px 5px;
}
img {
display: block;
margin: auto;
}
</style>
### 云服务器
#### 连接云服务器
1. 首先要在本地安装xshell和xftp
1. 然后通过xshell连接远程linux服务器：`root`是linux系统的登录用户（不是腾讯云），`4*.***.***.**6`是云服务器的公网地址
	```
	ssh root@4*.***.***.**6
	```
### Linux基础操作
1. 复制粘贴：在xshell命令界面，通过右键进行复制粘贴命令
2. 按`tab`键进行文件名补全
3. 命令结构：`ls -R /root`：`ls`是命令， `-R`是选项（可组合，如`-Rlh`），`/root`是命令对象
4. 蓝色文件名是文件夹，绿色一般是放命令的
5. `man ls`查看帮助文档
6. `bin`是存放指令的，`sbin`是管理员用的指令，`etc`是配置文件夹，`sys`是系统文件，`usr`是安装的命令文件，`tmp`是临时文件夹。（在自己家目录下玩最安全）
    - etc/passwd  所有用户信息
7. 访问web程序：host/html文件夹下面的目录
8. 任何命令都可以添加元字符，只要逻辑上说得通。
	```
	ls && ls /home   # 元字符就是 `&&` 、`||`、`!`
	```
### Linux基础命令
#### 用户相关
1. 切换用户
	```
	su zhangsan
	```
1. 登出
	```
	exit
	```
1. 删除用户
	```
	userdel -r user1  # 前提是user1必须`登出`了才能删除
	```
1. 创建用户
	```
	# 先看是否存在用户
	cat /etc/passwd  # 展示所有用户，末尾是`bash`的才是可登录的用户

	# 查看有哪些用户组（用户必须在组下面）
	cat /etc/group

	# 创建组:65是组id，不能和已有的重复
	groupadd -g 65 testgroup

	# 创建用户:355是用户id（不能重复），主组是testgroup
	useradd -u 355 -g testgroup testuser   
	```
#### 文件基础命令
1. 显示路径
	```
	pwd
	```
1. 路径跳转
	```
	cd /etc     # 绝对路径
	cd ../      # 相对路径：往上走一层
	cd ./www    # 相对路径：去当前目录下的www文件夹下
	cd ~        # 回到家目录
	```
1. 显示目录
	```
	ls
	ls -a        # 显示所有文件（包括隐藏文件）
	ls -A        # 显示所有文件（不包括隐藏文件）
	ls -lh       # 显示详情
	ls -d        # 不展开文件夹显示
	ls *文件*     # 模糊显示
	
	```
1. 创建文档
	```
	touch test.txt
	```
1. 创建文件夹
	```
	mkdir dir1 
	mkdir -p dirt1/dir2/dirt3    # 递归创建
	```
1. 删除文件
	```
	rm test.txt 
	rm text*        # 模糊删除
	rm -rf dir1     # 无询问删除
	```
1. 拷贝文件
	```
	cp test.txt /var/
	cp test.txt /var/book.txt  # 拷贝并重命名         
	cp -r dir1 /var/           # 递归拷贝文件夹（文件夹需要递归拷贝）
	cp test1 test2  /var/      # 同时拷贝两个
	cp test1 /var/dir          # dir是文件夹，则test1放到dir文件夹下；如果dir是文档，则test1放到var文件夹下并重命名成dir
 
	# 跨主机拷贝
	scp -r root@192.168.1.20:/home/user/dir1  /home/lijunlong/
	```
1. 移动文件：规则和拷贝一致
	```
	mv dir1  /var/dir2         # 移动文件夹不需要`-r`
	```
#### 文件压缩
1. tar打包:不压缩，打包和解包都会先拷贝一份源文件
	```
	tar -cf test.tar test1 test2     # 打包：test1和test2打包成test.tar
	tar -xf test.tar                 # 解包：test
	```
1. gzip压缩:只能压缩单个文件
	```
	gzip test1        # 压缩:test1.gz
	gzip -d test1.gz  # 解压:test1
	```
1. zip压缩：压缩和解压缩都会先拷贝一份源文件
	```
	zip test.zip test1 test2    # 压缩:test1和test2压缩成test.zip
	unzip test.zip              # 解压:解压名称是源文件名称
	```
#### 文件查找
1. 示例
	```
	locate test            # 支持模糊查询，和everything软件类似，可用`updatedb`手动更新数据
 	
 	find /root -name test  # 和locate一样，但是数据是实时的，所以慢
	find /root -name *.log -mtime +10  # 查找10天前被修改的日志
	```
#### 文件权限相关
1. 变更文件主人
	```
	# 变更文档主人
	chown newuser test1.txt   # test1.txt新主人是newuser

	# 变更文件夹主人
	chown -R newuser test1    # 递归授权
	```
1. 变更操作权限
	```
	chmod 755 test1           # 文档一般是644，文件夹一般是755（加了进入文件的`1`）
	```
#### 文件导入导出
1. 导入
	```
	rz
	```
1. 导出
	```
	sz test1.sh
	```
#### 文本编辑
1. 进入编辑文档
    ```
    Vim test1       # 打开或创建并打开文档
    ```
1. 文档编辑操作
    - 按`i`进入编辑模式
    - 按`esc`返回到命令模式(不可输入命令)，按`:`进入到底行模式（命令编辑模式）
    - `^`光标去到行首，`$`去行尾
    - `yy`复制所在行，`dd`剪切所在行，`p`粘贴
    - `u`撤销
    - `/关键字`搜索（底行模式）
    - 命令编辑模式输入`wq`退出保存
#### 脚本
1. vim编辑脚本（脚本后缀是 `.sh` ）：文本接收两个入参
   ```
   #!/bin/bash
   echo "第一个入参是$1"
   echo "第二个入参是$2"
   ```
1. 调用脚本：参数可缺
   ```
   chmod 755 test1.sh       # 先给脚本文件增加个可执行的权限
   ./test1.sh 入参1 入参2    # 前面不加地址会被当做系统命令，但这个显然不在PATH路径里面，所以会提示找不到命令
   ```
1. 脚本调试：显示脚本执行的每一步
   ```
   bash -x test1.sh
   ```
1. 函数
	```
	function add {
		local result=$(($1 + $2))  # 将两个参数相加
		echo $result  # 返回结果
	}

	# 调用函数，并将返回值存储在变量中
	result2=`add 10 20`

	# 显示调用的结果
	echo "The sum is: $result2"
	```
#### 文本查找
1. 查看文本
    ```
    cat test
    cat -n test    # 显示行号
    head -5 test   # 开头5行
    tail -f test   # 文尾监视
    ```
1. 管道：再处理
    ```
    head -6 test | tail -3
	netstat -tupln | grep mysql
    ```
1. 计数：可以统计很多东西，不详述
    ```
    cat test | wc -l  # 计算行数
    ```
1. 三剑客：grep
    ```
    grep 二 test      # 显示test中的所有带“二”的行
    grep -c 二 test   # 计算匹配的行数
    grep -n 二 test   # 把行号也显示出来
    grep ^$ test      # 显示空行
    grep -v ^$ test   # 显示非空行
    ```
1. 三剑客：awk
    ```
    awk -F 二 '{print $2}' test                   # 显示test被“二”分割的每一行的第2段
    awk -F 二 '{if ($1 == "第") print $2}' test   # 显示test被“二”分割，且第1段是“第”的每一行的第2段
    ```
1. 三剑客：sed
	```
	cat /etc/passwd | sed -n '1,5p'       # `1,5p` 拷贝passwd文档中的第1到5行；`-n` 不显示passwd文档原文
	```

#### 安装
1. yum安装：联网安装（国外的库慢）
	```
	yum install tree
	yum remove tree        # 卸载
 	rpm -qa | grep tree    # 查看安装的tree
	rpm -qi mariadb        # 查看安装包的详细信息
	```
1. rpm安装：安装rpm格式的
	```
	rpm -ivh zendao_2.3.rpm
	
	# 指定位置安装，有的不能指定位置，要根据安装包的详细信息看能不能指定
	rpm -ivh --prefix=/user/root zendao_2.3.rpm
	```
1. 源码安装：配置、编码、安装，格式一般是tar.gz
    - 先解压安装包：解压后看README看安装步骤
    - 配置：一般配置文件在`config`文件中，可以指定位置，也可以不指定
	```
	./configure --prefix=/user/root
	```
    - 编码：直接在命令行输入`make`回车就会执行文件中的makefile
    - 安装：命令行输入`make install`回车即可
    - 查看命令：在安装程序的地方打开文件的`bin`文件夹，里面是程序的所有命令，直接输入这些命令即可执行
    - 配置环境变量：上面的命令只能在程序的`bin`文件夹中或者`加上路径`执行，要在任意地方不加入路径也能执行，要配置到环境变量中，让系统认识该指令
    - 通过将快捷方式放入环境变量中的`bin`文件夹实现：本质上，只要在环境变量的路径中，系统就能识别出路径中的指令
    - 通过`echo $PATH`打印出环境变量有哪些路径
    - 然后给程序的`bin`创建快捷方式
	```
	# 前面的路径是程序的bin文件，后面的路径是一个环境变量路径
	ln -s /user/root/zendao/bin  /user/bin
	```
    - 源码卸载就是把解压的文件删除就行
1. zip安装
    - 直接解压就行，卸载就删除
1. 脚本安装：有的程序可能要反复安装，跑脚本就不用手动操作了
    - 先写脚本
	```
	#!/bin/bash
	echo "开始安装阿帕奇"
	yum -y install httpd httpd-devel
	
	systemctl start httpd
	systemctl enable httpd

 	# 略
	```
1. 安装jdk：java开发的软件都需jdk环境，和windows里面一样
    - 下载jdk的rpm安装包，并通过rpm安装
    - 通过find命令找到安装地址
    - 目前的jdk没有jre文件夹，进到安装的jdk文件中要添加一个jre文件夹
    - 添加到系统配置文件中：效果和快捷方式放入环境路径效果一致
	```
	vim /etc/profile
	```
    - 在profile文档中加入这么几句
	```
	JAVA_HOME=/user/java/jdk-15.0.2
	CLASSPATH=%JAVA_HOME%/lib:%JAVA_HOME%/jre/lib
	PATH=%PATH:$JAVA_HOME%/bin:$JAVA_HOME/jre/bin
	export PATH=CLASSPATH JAVA_HOME
	```
    - 让环境变量生效
	```
	source /etc/profile
	```
    - 安装好后通过`java -version` 查看版本
### Linux系统命令
#### 进程相关
1. 动态进程（不显示不活动的）
	```
	top
	```
1. 静态进程（所有进程）
	```
	ps -ef
	```
1. 显示当前进程id
	```
	echo $$
	```
1. 查看网络情况
	```
	netstat -tupln       # 显示使用网络的进程信息，包括端口号
	```

1. 开放端口：这里开放80端口，`add`换成`remove`就是关闭
	```
	firewall -cmd --zone=public --add-port=80/tcp --permanent 
 
	# 如果报`firewall.service: Unit not found`，执行：
	yum install firewalld
	systemctl unmask firewalld
	systemctl enable firewalld
	systemctl start firewalld
	```
1. 杀进程
	```
	kill -9 8976         # 8976是pid
	```
1. 关机和重启
	```
	shutdown -h now
	reboot -h now
	```
1. 显示系统时间
	```
	date
	```
### Shell命令（不严格分类）
#### 打印 echo 
1. 示例：特殊字符要转义
	```
	echo hello
	echo $PATH         # 打印变量
	```
#### 变量
1. 普通变量：等号两边不能有空格
	```
	a="你好"
	echo ${a}           # 这种形式获取变量是最推荐的，不加括号的有坑
	b="使用a变量值$a"    # 字符串中使用变量
	c="1""2"            # 字符串拼接
	```
#### 数组
1. 示例
	```
	list1=(a b c d)         # 创建一个数组
	echo ${list1[3]}        # 取索引3的元素。echo $list1[3]打印出来是a[3]
	echo ${list1[@]}        # 打印整个数组 
	```

#### 输入 read：类似python的input
1. 示例
	```
	read -p "请输入：" name
	echo $name                 # 打印出输入的内容
	```
#### 命令替换：命令嵌套
1. 规则：反引号内的命令要先执行了，结果在用来执行外面的。也可以用 `$(命令)` 表示，注意和变量的花括号有区别。
	```
	echo `cat /etc/passwd | grep root`
	```

#### 定时任务 at & crontab
1. 只执行一次的at
	```
	at -f ~/test1.sh 22:36 
	```
	定时任务时间到了不会主动显示，会在下一个命令后显示已经执行，去它提示的mail中可以查看执行记录，记得往下翻才看得到最新执行的记录。
1. 重复执行的crontab
   给用户root设置定时任务
   ```
   crontab -e -u root
   ```
   分 时 日 月 周：每两分钟执行一次后面的打印命令
   ```
   */2 * * * * echo "ok" >> ~/test1.txt
   ```
#### 判断
1. 大小判断：`=` 等于、`!=` 不等于、`-lt` 小于、`-gt` 大于、`-le` 小于等于、`-ge` 大于等于
	```
	[ 1 = 1 ] 
	[ 1 != 1 ] || true   #可用元字符连接不同逻辑
	```
	注意：中括号和逻辑符要有空格隔开；此外执行完不会显示结果。`$?` 表示上一个命令执行结果，0表示执行成功，1是失败，可用来显示判断的结果。
   	```
	echo $?
	``` 
1. 文件判断（是否存在）：`-e` 判断文件、`-d` 判断文件夹
	```
	[ -e ./test1.sh ]
	```
#### 自定义环境变量
1. 说明
   系统的配置文档 profile 作为一个脚本，最主要的就是写了系统变量PATH，系统开机就会去运行这个脚本，产生PATH系统变量，由于我们安装的命令都在PATH路径下，所以命令才能被系统识别。
   其实整个操作系统也相当于一个软件，在根目录下也有存放命令的bin，配置文件etc等，和一个软件的目录差不多。
1. 自定义环境变量
   所以要想自己写的变量也能全局使用，我们可以把变量加入到 profile 文件中，然后让系统执行一遍 profile 
	```
	source /etc/profile
	```
#### 计算
1. 示例：运算符两边要空格
	```
	expr 3 + 4
	expr 3 \* 4      # 乘号*是特殊字符要转义
	```
#### if
1. 示例
	```
	#!/bin/bash
	if [ $1 = 10 ];then
	echo "等于10"
	else 
	echo "不等于10"
	fi
	```

#### for循环
1. 按数字循环：1到10
	```
	#!/bin/bash
	for i in {1..10}
	do
	echo $i
	done
	```
#### while循环
1. 示例：累加到10
	```
	#!/bin/bash
	a=1
	while [ $a -le 10 ]
	do
	echo $a
	a=`expr $a + 1`
	done
	```
#### 跳出循环
1. break ：跳出总循环
1 . continue：跳出当前循环，继续下一次循环

### 其他
#### 安装mariadb
1. 示例：
	```
	# 安装
	yum install mariadb mariadb-server mariadb-libs mariadb-devel
	# 启动
	systemctl start mariadb
	# 进入mariadb
	mysql
	```