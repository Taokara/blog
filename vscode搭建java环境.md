<style>
h3{
    background: #2a5caa;
    box-shadow: 0px 1px 6px 1px rgba(10, 10, 0, 0.5);
    color: #FFFFFF;
    font-size: 18px;
    font-weight: bold;
    height: 30px;
    padding: 8px 0 5px 10px;
    text-shadow: 2px 2px 3px #222222;
}
h4{
    background: linear-gradient(to right, #d0d0d0 0%,#ffffff 100%);
    font-size: 5px;
    height: 25px;
    padding: 1px 0 5px 5px;
}
</style>
### 首先安装JDK环境
略
### VSCODE下载java插件
略
### 下载并配置MAVEN
1. 去官网下载maven
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_1.png)
1. 配置maven环境变量   
    把下载的maven解压后放到自己喜欢的地方
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_2.png)
    新建maven_home变量
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_3.png)
    path添加maven bin
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_4.png)
    检查下
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_5.png)
1. vscode设置maven全局路径：进入设置搜maven
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_6.png)
1. 修改maven配置，切换成阿里云的仓库，速度快很多
   参看：https://www.cnblogs.com/hellohui/p/16671489.html

### 创建maven项目
1. 进入控制面板
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_7.png)

   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_8.png)
    两个任选一个
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_9.png)
    选择版本
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_10.png)
    这个要等一下，知道让你输入版本号，版本号输入1.0即可
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode搭建java环境_11.png)
   最后提示成功后需要重新打开该文件夹。