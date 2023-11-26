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
### Anaconda安装
1. Anaconda说明
	因为我们在进行机器学习过程需要下载很多三方库，但这些库通常存在版本联系，自己去安装好python再下载这些包很麻烦，所以Anaconda相当于是一个包含python和各种库的集合体（所以需要卸载自己的python）
1. Anaconda下载
	[Anaconda历史版本下载地址](https://repo.anaconda.com/archive/ "Anaconda历史版本下载地址")
	Anaconda3-5.2.0-Windows-x86_64.exe版本对应python3.6，比较稳定。
2. Anaconda安装
	默认安装即可，安装注意跳过安装VSCode（安装好后能看到Anaconda Prompt并打开就表示安装好了）
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_1.png)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_2.png)
1. 配置环境变量
	因为Anaconda有很多程序，比如pip。
	在环境变量中加入Anaconda的几个环境变量：具体地址可能不一样，主要是这几个文件夹
	```
	D:\anaconda
	D:\anaconda\Scripts\
	D:\anaconda\Library\bin
	D:\anaconda\Library\mingw-w64\bin
	```
### CUDA和显卡驱动安装
1. 说明：
	- 显卡只是加速计算，没有显卡一样可以。
	- 显卡涉及两个安装，一个是显卡驱动，一个是CUDA，后者现在是和pytorch一键安装，所以只需要安装显卡驱动即可。
2. 安装驱动：
	通过一些安全软件就可以安装好，在任务管理里面看得到就表示驱动安装好了。
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_3.png)
	需要注意的是，在cmd中通过nvidia-smi命令查看显卡信息，显卡版本要高于390，否者就要去官网下载高版本的
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_4.png)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_5.png)
	设置优先使用独显。
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_6.png)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_7.png)
### 环境
1. 说明：
	- 不同项目可能依赖的环境不一样（和python项目差不多），所以我们需要创建不同的环境。
	- Anaconda自带的conda指令就可以创建不同的环境（Anaconda Prompt里面使用）
1. 创建新环境：
	创建环境指令：conda create -n lijunlong python=3.7
	指令说明：创建一个叫lijunlong的环境，在python3.7版本上
	激活环境指令：conda activate lijunlong
	指令说明：激活后base切换成lijunlong（下图是pytorch）
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_8.png)
	展示环境包指令：pip list
	指令说明：用于显示有哪些依赖包、库（pytorch也是一个包，如果在列表中没有，就需要去安装）
### 安装pytorch
1. 说明：
	因为国外的库容易连不上，报http错误，所以首先替换国内镜像库：
	添加清华镜像：
	```
	conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
	conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
	conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
	conda config --set show_channel_urls 
	```
	删除channels 中的defaults：
	```
	conda config --remove channels defaults
	```
	然后去`.condarc`文件下看看变没有。
1. 没有英伟达显卡：首先去pytorch官网，按图选择，需要选择None，且运行展示命令
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_9.png)
1. 有英伟达显卡：CUDA要选择自己显卡适配的，可以去网上查，然后同样把命令拿到Anaconda Prompt中需要的环境中执行(这里有个坑，如果你的Anaconda路径有中文，那就会提示找不到环境)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_10.png)
1. 如果安装过程提示如下，导致安装失败，直接删除提示的文件重新安装即可。
	```
	WARNING conda.gateways.disk.delete:unlink_or_rename_to_trash(140): Could not remove or rename D:\anaconda\pkgs\pytorch-1.6.0-py3.7_cuda101_cudnn7_0.tar.bz2. Please remove this file manually (you may need to reboot to free file handles)
	WARNING conda.gateways.disk.delete:unlink_or_rename_to_trash(140): Could not remove or rename D:\anaconda\pkgs\pytorch-1.6.0-py3.7_cuda101_cudnn7_0\Lib\site-packages\torch\lib\torch_cuda.dll. Please remove this file manually (you may need to reboot to free file handles)
	....
	TypeError'not all arguments converted during string formatting'
	```
1. 安装成功后我们通过`pip list`查看安装的torch
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_11.png)
		然后我们继续验证cuda是否可以被torch使用：
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_12.png)
### 使用pytorch
1. 说明：
	- 使用pytorch自然需要python编辑器，我们就可以使用pycharm，但是我们需要的环境是我们上面提到的conda环境
	- 除了pycharm，jupyter也是一个python编辑器，是专门针对pytorch的，所以也要掌握
1. 通过pycharm使用pytorch：
	首先新建一个工程
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_13.png)
	环境也是一个python文件：这个位置也有可能是在Anaconda3下面的envs
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_14.png)
	新建好工程后，在python console里面输入如下指令查看环境是否ok
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_15.png)
1. 通过jupyter使用pythorch
	要使用jupyter，首先查看该环境下是否安装相关依赖：通过`conda list`查看
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_16.png)
	重要的是这个包
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_17.png)
	如果没有，需要安装：`conda install nb_conda`
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_18.png)
	安装好启动jupyter：
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_19.png)
	进入jupyter环境：选我们安装了torch的环境（启用jupyter的环境）
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_20.png)
	如果我们看到环境报错，可以查看报错详情：这里显示的是Kernel error，具体报的是“win32api”错误，我们需要安装win32api
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_21.png)
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_22.png)
	回到刚才的环境，安装win32api：`pip install pypiwin32`，然后再次启动jupyter即可
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_23.png)
	执行命令：jupyter输入一行按shift + enter执行一行
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pytorch环境搭建_24.png)