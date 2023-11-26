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
### git说明
git安装之后就可以链接代码托管平台，实现代码托管。如果不习惯git自带的命令进行代码的上传，可以安装TortoiseGit这个图形化界面进行代码上传，TortoiseGit只是替代了git本身的图形化界面，没有git是不行的。

### git安装和仓库clone（本地没有工程）
1. 先安装windows版本的Git，到处都有镜像资源
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_1.png)
2. 安装TortoiseGit（不要改安装地址，不然用不了汉化包），还有汉化包，直接官网下载；安装好之后右键点击文件夹就会出现
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_2.png)
	汉化包使用：安装好后在设置里面选择语言
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_3.png)
	注意：如果右键小乌龟或者clone显示`找不到指定文件`，只需要重启一下电脑就可以了
3. 此时还不能直接使用TortoiseGit的右键`clone`来拉取平台的代码，需要先配置ssh才有权限。安装好TortoiseGit会有一个PuTTYgen的小程序，用来产生密钥的（如果不安装TortoiseGit，在cmd命令行也可以用命令生成）
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_4.png)
	首先点击`产生`生成密钥，这个过长鼠标要乱动（估计密钥和鼠标运动轨迹有关）；进度条跑完复制红框中的密钥到gitee上的密钥里
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_5.png)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_6.png)

	然后回到刚才的PuTTYgen，点击`保存私钥`，名称随意。保存的密钥需要存到Pageant这个小程序中，也是安装TortoiseGit产生的
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_7.png)
	打开Pageant我们需要添加我们刚才保存的私钥（添加之后，正常情况下我们克隆的时候就不需要勾选“加载Putty密钥”了，但是Pageant保存的密钥会掉！我也不清楚原因，这个时候我们要么从新上传密钥到Pageant，要么在克隆的时候勾选“加载Putty密钥”，并选择ppk密钥文件。）
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_8.png)
	然后我们就可以去clone仓库了。
4. 首先我们需要在gitee先建一个仓库，然后复制ssh地址(需要注意的是如果改了仓库名这种，有可能会改ssh，所以要修改tortoise上的远程地址)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_9.png)
5. 然后我们新建一个本地文件夹，右键clone会让我们输入ssh地址。这样，我们就可以拉取代码和推送代码了。
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_10.png)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_11.png)

### 本地有工程，关联一个新的仓库
1. 首先右键该工程文件夹在本地创建版本库
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_12.jpg)

2. 然后去gitee创建远程仓库

1. 然后提交代码
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_13.jpg)
	提交全部：
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_14.png)
1. 然后进行推送：
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_15.jpg)
	设准远程（相当于clone那一步）：
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_16.png)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/git使用_17.png)
	
	然后继续完成刚才的推送就行了。

### 代码上传
1. 当我们改了本地代码，需要上传，第一步永远是拉远程，再提交（提交记得备注），再推送，不细说