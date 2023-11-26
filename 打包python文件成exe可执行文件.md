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
### 安装pyinstaller
1. 专门打包python文件的:cmd中安装
	```
	pip3 install pyinstaller
	```
### 开始打包
1. 需要一个图标文件（ico）和要打包的py文件：需要注意的是，生产的main.exe文件要通过everthing查找
	```
	pyinstaller -F -w -i D:\projectFiles\pythonFiles\pyautogui\xiayu.ico D:\projectFiles\pythonFiles\pyautogui\下雨通知\main.py
	```
### 常见报错
#### 没有对应的模块：ModuleNotFoundError: No module named 'xxx'
1. 说明：
	&emsp;这个错误是因为pyinstaller没有把py文件import的包打包进去导致的，其实pyinstaller打包的时候会生产一个spec文件，可以去里面配置要打包的内容。
1. 解决办法：
	- 首先还是执行一次打包命令：
	```
	pyinstaller -F -w -i D:\projectFiles\pythonFiles\pyautogui\xiayu.ico D:\projectFiles\pythonFiles\pyautogui\下雨通知\main.py
	```
	- 然后通过everthing查找打包main.py生成的main.spec（相当于打包的配置文件）
	- 找到后用记事本打开：这个pathex参数就是依赖包地址（为空的话就表示没有打包依赖包，就要加入地址）
	```
    pathex=['D:\\projectFiles\\pythonFiles\\pyautogui\\venv\\Lib\\site-packages'],
	```
	- 怎么找这个以来地址呢：比如我们程序中import了xlrd
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/打包python文件成exe可执行文件_1.png)
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/打包python文件成exe可执行文件_2.png)
	- 通过spec文件进行打包：不再通过上面的打包命令，直接打包spec文件即可
	```
	pyinstaller D:\projectFiles\pythonFiles\pyautogui\下雨通知\main.spec
	```
### 在win10中设置成定时任务
两个要点：
- 要使用最高权限：不然程序要使用的一些文档打不开。
![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/打包python文件成exe可执行文件_3.png)

- 把路径设置好
![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/打包python文件成exe可执行文件_4.png)