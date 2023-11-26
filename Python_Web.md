### flask
#### flask搭建简单的web服务
1. 示例：运行后通过url即可访问
    ```
    from flask import Flask

    app = Flask(__name__)

    @app.route('/show/info')
    def index():
        return 'Hello, World!'

    if __name__ == '__main__':
        app.run()
    ```
1. 返回一个html文件
    ```
    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/show/info')
    def index():
        return render_template("index.html")  # 返回一个html文件

    if __name__ == '__main__':
        app.run()
    ```
    这个html文件要放在 `templates` 文件夹下（名称不能改）
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_1.png)

### bootstrap样式库
1. 说明
   其实就是一个现成的css样式库，要用的地方导入就可以了
#### 下载bootstrap
1. 项目新建静态资源文件夹：用来放一些css、js、图片、插件
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_2.png)
1. 下载bootstrap样式库，并把解压文件放入piugins文件夹
#### 使用bootstrap中的阈值css样式
1. 示例
   - 使用link标签连接plugins中的css库，其中，上面的是开发版本的连接，下面的是上线版本（注释了），区别是上线版本的写成一行，体积小。需要注意的是连接相对地址要写对，不然无效。
   - 当连上后，class属性就可以自动补全了
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_3.png)

#### 使用bootstrap官方文档中的html片段
1. 下载bootstrap，最好是v3版，里面的样式多一点，css样式库和官方html片段要匹配，不然样式匹配不上。
1.  打开官方文档组件：https://v3.bootcss.com/components/#nav
1. 拷贝html片段到body中即可使用（格式有问题的可以格式化一下）
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_4.png)
1. 在浏览器查看样式：如果样式需要微调，在F12中可以修改一些参数
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_5.png)
1. 在html文件中修改参数：上面发现的css属性微调后，在html在把刚才微调的属性修改在html文件中生效吧
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_6.png)

#### 使用图标
1. 可以去fontawesome网站获取图标样式：略

### jQuery
1. 这部分参看我写的js博文

### Django 
#### 创建Django
1. 安装Django 
    ```
    pip install django
    ```
    安装好后项目环境中会出现一个可执行文件
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_7.png)

1. 终端执行该文件：test3是Django项目名
    ```
    "C:\Users\****\apps\projects\pythonProjects\test2\.venv\Scripts\django-admin.exe" startproject test3
    ```
    由于我们是直接在vscode终端执行的，其创建的Django项目也会在我们的项目下，如果我们想换个地方(比如直接创建一个新项目)，就需要去cmd里面执行了。
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_8.png)

    会在项目中创建下面这个文件夹：
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_9.png)

1. 创建app
   一般一个项目下面都有一个app，在终端输入：
    ```
    python ./test3/manage.py startapp app1 
    ```
    创建如下:
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_10.png)

#### 启动django项目
1. 注册app
   我们在apps中可以查看我们创建的app名称（可以改）
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_11.png)

   然后在setting里面注册这个app
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_12.png)

1. 写视图函数并绑定url：这里在views里面写了一个简单的http请求响应函数
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_13.png)

   邦定函数和url
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_14.png)

1. 此外，如果url还支持动态参数：也可以用问号的方式传值
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_15.png)

    这个参数也要添加到方法中，可以不用
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_16.png)

    通过动态参数地址访问
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_17.png)


1. 启动django并访问：终端输入。注意：不是点击运行按钮启动Django！
    ```
    python ./test3/manage.py runserver
    ```
   访问：
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_18.png)

1. 返回html页面：需要在app项目下创建templates文件夹，用来放html页面
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_19.png)

1. 视图函数返回html页面
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_20.png)

#### 静态文件
1. 常规方式：不推荐
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_21.png)

1. django推荐方式
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_22.png)

   同样的jquery也可这么导入：需要注意jquery导入最好放在head中，如果这里放在onclick下，onclick就会提示 "clickMe is not defined"。
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_23.png)

    setting里面可以统一改前面地址
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_24.png)


#### html使用变量（模板语法）
1. 使用变量
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_25.png)

   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_26.png)

1. 使用列表
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_27.png)

   使用第3个元素c
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_28.png)

   循环获取
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_29.png)

1. 使用字典：根据键获取值
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_30.png)

   循环字典键值
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_31.png)

#### html模板继承
1. 被继承模板添加下面的语法
    ```
    {% block content %}{% endblock %}
    ```
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_32.png)

1. 使用模板的html继承
    ```
    {% extends 'login.html' %}

    {% block content %}
        <!-- 新页面独有的内容 -->
    {% endblock %}
    ```
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_33.png)

#### 请求和响应
1. 一个登录页面
   - 第一行是提交后要访问的地址和请求方式
   - 第二行是django会设置一个csrf_token隐藏提交值，让下一个页面确定我们是来自这个页面的(csrf认证只限于post请求，get请求不需要)
   - 第三四行是提交值的key
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_34.png)

1. 视图登录方法
    ```
    def login(request):
        # 根据请求方式返回不同页面
        if request.method == 'GET':
            return render(request, 'login.html')
        else:
            username = request.POST.get('user')  # 根据提交key获取值
            password = request.POST.get('password')

            # 校验输入内容
            if username == 'admin' and password == '123':
                return HttpResponse('登录成功')
            else:
                return HttpResponse('登录失败')
    ```

#### ORM（数据库简化操作）
1. 说明
    其实就是封装了一层pymysql这种三方库（这里用mysqlclient），减少写sql语句。
1. 首先安装mysqlclient
   windows安装一般会报错，可以去下载其wheel文件进行安装（https://pypi.org/project/mysqlclient/#files），其中cp37代表python版本3.7，如果没找到就去历史版本中找。
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_35.png)

1. 安装wheel文件
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_36.png)

1. django连接数据库
    在setting.py中修改数据库连接如下：
    ```
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'test_database1',
            'USER': 'root',
            'PASSWORD': '123456',
            'HOST': '127.0.0.1',
            'PORT': '3306',
        }
    }
    ```

#### ORM_创建表
1. 这里创建一个user表，有3个字段
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_37.png)

1. 首先在app下面的models.py文件中写连个表类：
    ```
    class department(models.Model):
        id = models.AutoField(primary_key=True)
        name = models.CharField(max_length=32)

    class User(models.Model):
        name = models.CharField(max_length=32)
        password = models.CharField(max_length=32)
        age = models.IntegerField(default=0)
        # 外键：关联department部门的id字段，后面几个参数表示删除关联表的数据后对应user表外键为空
        depar = models.ForeignKey(to="department", to_field="id", null=True, blank=True, on_delete=models.SET_NULL)
    ```
1. 然后在cmd执行下面两个命令
    ```
    python ./test3/manage.py makemigrations

    python ./test3/manage.py migrate
    ```
1. 数据库中出现该表，且自动生成一个id字段。还有一些其他表是django相关的，不管。

#### 表的增删改查
1. 示例：到时候运行浏览器访问就能写入数据了
    ```
    def orm(request):
        # 增
        User.objects.create(name='admin', password='123456', age=10)

        # 删
        User.objects.filter(id = 1).delete() 
        # User.objects.all().delete()

        # 查
        all = User.objects.all()   # 查询到的是一个对象列表
        for i in all:
            print(i.id, i.name, i.password, i.age)
        User.objects.filter(name = 'admin').first()  # 获取列表第一个对象

        return HttpResponse("成功")
    ```

#### ModelForm创建控件
1. 说明
   我们自己写输入控件，还要自己写前端校验规则和后端校验规则，比较麻烦，ModelForm可以根据我们创建的数据库字段自动生成输入控件，能自动进行前后端校验
1. 视图函数代码示例
    ```
    from django import forms
    from app1 import models  # 还是要从app下导入

    # 创建一个继承ModelForm的类
    class UserModelForm(forms.ModelForm):
        # 创建内部类
        class Meta:
            model = models.User   # 调用models中的User类
            fields = ["name", "password"]   # 使用User类中的两个字段
        
        # 给ModelForm控件设置属性
        def __init__ (self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            for name, field in self.fields.items():  # name是字段名，field是控件对象
                # 不给password控件设置属性
                if name == "password":
                    continue
                field.widget.attrs = {"class": "form-control"} # 这个属性是Bootstrap中的


    def login(request):
        if request.method == 'GET':
            # html页面使用ModelForm类
            form = UserModelForm()
            return render(request, 'login.html', {'form': form})
        
        # 当请求是POST时
        form = UserModelForm(request.POST)
        # 如果提交的数据有效则保存
        if form.is_valid():
            form.save()
            return HttpResponse("success")
        else:
            return HttpResponse("error")
    ```

    html中使用ModelForm参数：
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_38.png)

#### 前端校验
1. 页面返回错误提示
    ```
    def login(request):
        if request.method == 'GET':
            form = UserModelForm()
            # GET请求，form参数还没有错误提示
            return render(request, 'login.html', {'form': form})
        
        form = UserModelForm(request.POST)
        if form.is_valid():
            form.save()
            return HttpResponse("success")
        else:
            # 当POST请求参数错误时，form参数带有错误信息
            return render(request, 'login.html', {'form': form})
    ```

1. 页面html显示错误信息：获取name的第1个错误（因为可能有很多错误，不能都展示）
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_39.png)

    上面的错误提示是英文，显示中文需要修改setting.py的编码语言
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_40.png)

1. 添加前端校验
   上面的校验规则都来自数据库的设置，如果我们需要单独设置前端规则，可在ModelForm类中添加
    ```
    class UserModelForm(forms.ModelForm):

        # 给name字段增加前端校验规则
        name = forms.CharField(min_length=3)

        class Meta:
            model = models.User 
            fields = ["name", "password"]  
    ```

#### 鉴权_中间件
1. 说明
   - 我们使用cookie和session进行鉴权，当用户登录后，django会给用户cookie里添加一个session码，同时django中也会保存这个session和用户信息，当用户访问其他页面，携带该session码访问服务器，django服务会识别这个session然后允许其访问。
   - 上面说的鉴权方式，正常使用的话就需要每个视图函数都进行鉴权，较麻烦，这里通过中间件进行，所谓中间件就是在请求来的时候，会优先访问的函数，可进行鉴权等操作。
1. 登录页生产session
    ```
    def login(request):
        if request.method == 'GET':
            form = UserModelForm()
            return render(request, 'login.html', {'form': form})
        
        # 当请求是POST时
        form = UserModelForm(request.POST)
        # 如果提交的数据有效
        if form.is_valid():

            # 提交的数据进行数据库查询
            user = models.User.objects.filter(**form.cleaned_data).first()
            # 如果没查到就提示错误
            if not user:
                # 添加一个错误到form对象
                form.add_error("password", "账户或密码错误")
                return render(request, 'login.html', {'form': form})
            # 查询到数据就生成session并和用户信息一起存储
            request.session["info"] = {'name': user.name, 'id': user.id}
            # 重定向新的页面
            return redirect("/orm/")
        
        # 数据无效还是回到登陆页面
        return render(request, 'login.html', {'form': form})
    ```
1. 中间件鉴权
   一个类就是一个中间件，其方法就是请求来时要调用的函数，通过请求中携带的session与数据库中的对比判断是否可以访问
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_41.png)

   数据库session的位置
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_42.png)

1. 中间件添加到设置：这样才能生效
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_43.png)

1. 登录后获取用户信息
   我们生成因为把用户信息放入了session中，而session又在info中，而info有来自请求request，所以在可以在页面直接使用：
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_44.png)

#### 注销用户
1. 注销视图函数：记得在url模块添加地址
    ```
    def logout(request):
        # 清除数据库session
        request.session.clear()

        # 重定向到登录页
        return redirect('/login')
    ```
1. 在页面上添加注销地址
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_45.png)

#### ajax_局部刷新
1. 说明
   form提交的表单，会刷新整个页面，而ajax提交数据是局部刷新，不影响不需要刷新的内容。
1. 使用ajax提交get数据
   - 新建一个新的视图函数用来接收提交的数据：中间的打印是把提交来的参数打印出来
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_46.png)
   url中添加该视图函数
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_47.png)
   - 在html页面添加ajax提交：首先我们创建了一个按钮用来触发一个叫clickMe的事件，事件内容是ajax提交，ajax参数需要含要提交的地址、请求类型、参数。如果提交成功，就执行success后面的函数，其中res是提交成功后的返回值，我们上面视图函数返回的是一个“成功！”，这里把它输出到控制台。
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_48.png)
    这个时候点击按钮页面不会全部刷新了，只会在网络中增加一条请求：
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_49.png)

1. 使用ajax提交post数据
   - 因为post请求需要csrf认证，但ajax携带csrf较繁琐，可以在视图函数中免除csrf认证
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_50.png)

1. 使用jquery绑定事件
   - 上面的直接把事件写到DOM里面的方式不好维护，我们使用绑定元素的方式方便维护
   - 1是绑定事件，当框架加载后就会执行；2是绑定的函数；3是绑定id的ajax点击函数
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_51.png)

1. 参数来自页面输入框
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_52.png)

#### 返回json
1. 说明
   一般返回是json，所以我们需要在视图函数将字典转换成json返回
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_53.png)
1. html页面获取json
   - 要添加一个datatype，不然只能识别成字符串。识别成json后可通过 `.XX` 的形式获取json内容 
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/Python_Web_54.png)