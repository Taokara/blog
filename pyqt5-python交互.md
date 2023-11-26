1. 安装pyqt5，算是框架，直接在pycharm库里面搜pyqt5就行了
2. 安装可视化设计器Qt Designer，这个去官网下载就可以了，不过最好找个中文版的下载。
3. 在pycharm上配置插件，好让pycharm和安装的Qt Designer联动
   - 添加插件Qt Designer
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_1.png)
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_2.png)
    - 添加插件Pyuic（这个是安装pyqt5库就一起安装的，用来把Qt Designer图像化设计的UI界面转化成py文件）：1是项目地址，因为我们一开始建立项目选择新环境，所以新环境安装的库是在项目下面的，所以这个2是在项目下的；3是Qt Designer生成的文件，4是要转化成的py文件；5是py文件要存放的地址，这里的变量意思是存放在当前目录。
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_3.png)
4. 在Qt Designer上面设计UI：
   - 界面控件
    布局和按钮：布局具有规范化，控制多个控件格局的作用，没有控件，带文字的控件，文字容易显示不完全；按钮就是按钮
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_4.png)

    输入控件：
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_5.png)

    显示控件：
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_6.png)

    属性：软件名和图标
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_7.png)

    信号与槽：说白了就是触发与动作，这里面能做的很简单，一般不用这个，要自己写的才能比较复杂
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_8.png)

5. 生成py文件
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_9.png)
   需要手动加上这句话才完整，不然生成的图形化界面和设计的不一致
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_10.png)
   启动器：运行这个才能生成界面，只用改红线
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_11.png)
6. 添加信号与槽
   - 在setupUi方法下，添加下面的语句：1是控件，2是动作，3是信号，4是后续动作
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_12.png)
    在这个方法中，我们输入或者勾选的，都会产生内容，比如text或者被勾选ischecked等等，就可以对其进行判断，这里面我还调用了个LenCon()方法，这个才是我要实现的内容核心，比如这个函数就是根据你选择的参数进行一个字符串的生成。不过在产生的py文件中编辑有个问题，下次调整了控件之后会导致重新生成，之前添加的会被覆盖，应该搞成装饰器或者继承比较好。
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_13.png)

    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/pyqt5-python交互_14.png)