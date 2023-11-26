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
#### 括号补全
1. 说明：正常情况vscode输入print等代码不会加上括号，`sttings.json` 添加此配置后会补全，记得保存
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode编辑python代码相关设置_1.png)
#### 代码补全
1. 说明：有很多补全的工具，AI的好用些
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode编辑python代码相关设置_2.png)

	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode编辑python代码相关设置_3.png)
#### python（解释器）版本
1. 说明：
	我们不同的项目可能需要不同的python版本，所以一般我们需要安装不同的python版本，如何配置看这个视频：[python多版本配置](https://www.aliyundrive.com/s/nJ3SzfSGcaf "python多版本配置")
#### 虚拟环境
1. 说明：
	我们安装了python3.7（解释器）后，所有项目的安装包都会安装到主环境里面，我们希望一个项目有自己的一个环境，这就是虚拟环境，如何配置看这个视频：[pyhon虚拟环境](https://www.aliyundrive.com/s/XJus7JFmZWT "pyhon虚拟环境")
2. vscode选择解释器
	当我们有不同版本的解释器（包括虚拟的），我们执行代码就可以选择用哪个解释器执行，本项目有虚拟环境肯定选本虚拟环境，下图带星号的就是：
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/vscode编辑python代码相关设置_4.png)
#### 引用自定义包
1. 说明：
	所谓自定义包就是在本项目文件夹A下的文件夹B，文件夹B新建一个 `__init__.py` 文件后既是一个自定义包，如果A下的其他模块要引用B中的模块，通过 `from 包名.模块名 import *` 即可。但有时候vscode一直提示找不到这个包，网上常见的方式是在 `launch.json` 配置文件中添加包的地址解决，但感觉有点麻烦。但自从我安装虚拟环境后，这个问题就自动解决了，原因不详，我在虚拟机中新安装的vscode也不存在这个问题。