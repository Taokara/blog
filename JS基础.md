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
### vscode写html基本操作
#### vscode中html快捷键
1. 输入html，选html:5，自动补全html框架
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_1.png)
#### 用浏览器查看html文件
1. js语法必须写在html的 `<script>` 标签中
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_2.png)

1. 下载扩展
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_3.png)
1. `Ctrl` + `s` 保存html文件
   
1. 右键用默认浏览器打开html
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_4.png)

### JS语法
#### 显示值
1. 代码
    ```
    alert("你好");            // 弹出提示 
    document.write("你好2");  // 写到页面上
    console.log("你好3");     // 写到控制台
    ```
#### 变量
1. 全局变量：js是弱类型语言，和python一样
    ```
    var a = 123;
    a = "哥哥";
    alert(a);
    ```
1. 局部变量：局部变量不能和其他变量名称重复
    ```
    let h = 123;
    ```
#### 数据类型
1. 5种
    ```
    var a = false;      // boolen
    var b = 12.12;      // number
    var c = "你好";     // string
    var d = null;       // null
    var f = undefined;  // undefined
    ```
#### 运算
1. 说明：和java一样，略
#### 逻辑语句
1. 说明：和java一样，略
#### 函数
1. 方式一
    ```
    function sum1(a,b) {  //function是方法关键字；sum1是函数名；a、b是参数
        return a + b;     //方法体
    }
    alert(sum1(3,3));     //使用方法
    ```

1. 方式二
    ```
    var sum2 = function(a,b){
        return a + b;
    }
    alert(sum2(2,2));
    ```

#### 数组
1. 代码
    ```
    var list1 = [1,2,3];

    list1[5] = 5;            //数组根据索引赋值
    list1.push(10);          //数组添加值
    list1.splice(0,2);       //数组删除值（开始位置，删除几个）
    ```
#### String
1. 代码
    ```
    var a = "hello!";

    alert(a.length);         //字符串长度
    alert(a+1);              //字符串拼接
    var b = "  hello!  ";
    alert(b.trim())          //字符串去除前后空格
    ```
#### 自定义对象
1. 代码
    ```
    var Human = {
        name:"张三",
        age:20,

        //方法
        work:function(a) {
            alert("张三干了" + a + "年程序员");
        }
    }

    alert(Human.name);        //调用自定义对象属性
    Human.work(10);           //调用自定义对象方法
    ```
#### BOM(浏览器对象模型)
1. 说明
   其实就是浏览器对象集合，包括窗口对象、浏览器对象（不常用）、屏幕对象（不常用）、历史记录对象、地址栏对象
####  window(窗口对象)
1. alert方法：警告弹窗
    ```
    window.alert("123")   //window可省略，下面的方法一样
    ```
1. confirm方法：确认弹窗
    ```
    var a = confirm("确认删除？");  //弹出确认弹窗，确认后返回true
    if(a){
        alert("已经删除")
    }
    ```
1. 定时器：方法+间隔时间（ms）
    ```
    var a = function() {
        alert("123");
    }
    setTimeout(a,3000);    //3S后执行一次a
    setInterval(a,3000);   //3S后循环执行a
    ```
#### DOM(文档对象模型)
1. 说明
   其实就是html文档对象集合，包括整个文档对象、元素对象、属性对象、文本对象、注释对象
#### document对象
1. getElementsByTagName：根据标签名称获取元素对象，获取的结果是对象数组
    ```
    var list1 = document.getElementsByTagName("crs")
    ```
1. getElementById：根据id获取元素对象
    ```
    var a = document.getElementById("id001")
    ```
#### HTML对象属性
1. 说明
   不同标签的元素对象，属性是不一样的，每种标签具体有什么属性，可以看文档：https://www.runoob.com/jsref/dom-obj-image.html
1. img元素的src属性：设置或者返回图片url
    ```
    var a = document.getElementById("img001"); //假设这里获取到的就是一张图片对象
    a.src = "https://img20795840.png";         //设置这张图片的url
    ```

#### 事件监听
1. 事件绑定：点击事件onclick，监听到后触发方法
    ```
    document.getElementById("id001").onclick = function(){
        alert("按钮被点击！");
    }
    ```
#### 常见的事件
1. 失去焦点onblur：一般用于输入框
1. 获得焦点onfocus
1. 点击onclick
1. 悬浮onmouseover
1. 确认按钮被点击onsubmit

#### 正则
1. 示例
    ```
    var a = /^[0-9]+$/;   //正则内容要写在开始结束符合之间：/^$/
    var b = "123";
    var c = a.test(b);    //校验是否符合，返回布尔
    alert(c);
    ```
   
### jQuery
1. 说明
   jQuery其实就是简化的js
#### jQuery下载并使用
1. 去官网点击这个文件：https://jquery.com/download/
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_5.png)

1. 右键另存为打开的文件
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_6.png)

1. 将保存的js文件放到项目中，可以放到静态资源中
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_7.png)

1. 使用jQuery语法
    - 这里我把jquery放到了静态资源下的js文件夹下
    - 需要注意jquery导入最好放在head中，如果这里放在onclick下，onclick就会提示 "clickMe is not defined"。
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_8.png)
#### 选择器
##### 直接寻找
1. 说明
   jquery选择器语法和css的一样
1. ID选择器
    ```
    $("#t1")
    ```
1. 样式选择器
    ```
    $(".c1")
    ```
1. 标签选择器
    ```
    $("h1")
    ```
1. 层级选择器：h1标签下样式是c1下的a标签
    ```
    $("h1 .c1 a")
    ```
1. 多选择器：同时选了两个 
    ```
    $("#t1,#t2")
    ```
1. 属性选择器
    ```
    $("h1[name="myname"]")
    ```
##### 间接寻找
1. 找上下
    ```
    $("#t1").prev()  # 找上一个
    $("#t1").next()  # 找下一个
    ```
1. 找父子
    ```
    $("#t1").parent()  # 找父
    $("#t1").children()  # 找子
    $("#t1").children(.p10)  # 找指定子
    $("#t1").find(".p10")  # 找指定子孙
    ```

#### 操作样式
1. 属性操作
    ```
    $("#t1").addClass("hide")  # 添加样式
    $("#t1").removeClass("hide")  # 移除样式
    $("#t1").hasClass("hide")  # 判断是否存在样式
    ```

#### 值和标签操作
1. 内容操作
    ```
    $("#t1").text()  # 获取值
    $("#t1").text("新值")  # 设置值

    $("#t1").val()  # 获取用户输入值
    $("#t1").val("新值")  # 设置用户输入值
    ```
1. 创建、添加、删除标签
    ```
    var a = $("<#t2>").text("新标签值")  # 区别就在与多了：<>

    $("#t1").append(a)  # 添加一个新的标签在#t1

    $("#t1").remove()  # 删除标签
    ```
#### 事件
1. 绑定事件：点击事件
    ```
    $("#t1").click(function() {
        alert("按钮被点击！");
    })
    ```
#### jquery加载时机
1. 说明：
   我们的js代码都在`<script>`标签中，直接写的话，它加载的时间是在整个html页面加载完成后才执行，如果需要早点加载，可以把所有的jquery放在一个函数里，这样html加载完框架就可以执行了。
    ```
    <script>
        $(function() {
            # 这里写其他的jquery代码
        });
    </script>
    ```
### VUE3
1. 说明
    jQuery更像一个三方库，简化了js，因此做不到前后端分离。而VUE则是可以单独做成前端项目，像django一样，所以是一种前端框架。
#### MVVM思想
1. 说明
   也即model-view-viewModel，model就是script中的数据，view就是html显示的各种元素，viewModel就是保持model和view数据时刻同步。其中vm是vue自带能的能力，自动遍历model数据，同步到view中。
#### VUE使用
##### vue导入
1. 说明
   这里先介绍把VUE像jquery一样导入使用，用以说明其基本语法
1. 下载
   访问VUE官网，去使用文档找到其js连接，访问连接下载js
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_9.png)

##### VUE常用指令
1. 说明
   VUE中有许多指令用来替代原生js的内容、属性等，格式如 `v-XXX`，下面分别介绍。 
##### 获取内容
1. 双花括号显示数据：其实也可以用 v-text
    ```
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <!-- 引入VUE -->
        <script src="../static/js/vue-3.3.4.js"></script>
    </head>
    <body>
        <!-- 双花括号使用script中的参数 -->
        <div id="app">
            <p>{{ message }}</p>
        </div>

        <!-- 在script中创建参数 -->
        <script>
        Vue.createApp({
            data() {
            return {
                message: '要显示的内容!'
            }
            }
        }).mount('#app');  // 绑定元素，子元素也可以使用其参数
        </script>
    </body>
    ```
    查看该页面只能直接打开该html，不能通过路由地址打开，不然参数的值在html页面中无法显示，原因未知。
2. v-model和v-html显示数据
    - v-model用于显示没有直接内容展示的标签中，比如输入
    - v-html用于显示含html标签的内容
    ```
    <body>
        <div id="app">
            <!-- v-model显示数据 -->
            <input type="text" v-model="message">  
            <!-- v-html显示数据 -->
            <p v-html="img"></p>
        </div>

        <script>
        Vue.createApp({
            data() {
            return {
                message: '要显示的内容!',
                img: '<img src="../static/img/1.png">'
            }
            }
        }).mount('#app');
        </script>
    </body>
    ```
    效果如下：
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JS基础_10.png)
##### 获取属性
1. 通过 `:属性名` 获取vue中的属性
    ```
    <div id="app">
    <!-- 获取属性 -->
    <img :src="img1">
    </div>
    <script>
    Vue.createApp({
        data() {
        return {
            img1: '../static/img/1.png'
        }
        }
    }).mount('#app');
    ```

#### 监听事件
1. 通过 `@事件名` 监听vue事件：vue事件可以使用createApp下面的参数
   - `@click` 表示点击事件
   - `img1=()` 表示给img1参数赋值括号中的内容
   - `img1==='A'?'B':'C'` 表示img1如果等于A，则是B，否则是C。所以点击效果就是在BC之间切换。
    ```
    <body>
        <div id="app">
        <!-- 使用vue事件 -->
        <img :src="img1" @click="img1=(img1==='../static/img/1.png'?'../static/img/2.png':'../static/img/1.png')"> 
        </div>
        <script>
        Vue.createApp({
            data() {
            return {
                img1: '../static/img/1.png',
            }
            }
        }).mount('#app');
        </script>
    </body>
    ```
#### 监听类中的函数
1. 这里点赞二使用的Vue对象中的方法进行点赞数累加
    ```
    <div id="app2">
        <button @click="num1+=1"> 点赞一{{num1}}</button>
        <button @click="dianzan"> 点赞二{{num2}}</button>
    </div>
    <SCript>
        var vm=Vue.createApp({
        data() {  // 属性
            return {
            num1: 0,  // 属性一
            num2: 0,  // 属性二
            };
        },
        methods:{   // 方法
            dianzan(){  // 方法一
            this.num2+=1;
            }
        }
        }).mount("#app2");
    </SCript>
    ```
#### 操作样式
##### class和style设置
1. 这里属性中的class格式为 `:class=` ；使用style，格式为 `:style=` 
    ```
    <head>
        <style>
        .cla1 {
            color: #5c7cc2;
        }
        .cla2 {
            background-color: rgb(88, 158, 103);
        }
        </style>
    </head>
    <body>
        <div id="app2">
        <li :class="c1">1、使用属性指定的样式</li>
        <li :class="[c1, c2]">2、使用属性指定的两种样式</li>
        <li :class="c3" @click="c3.cla1=false">3、通过事件设置属性中的样式是否生效</li>
        <li :style="sty1">4、不使用head中的样式，而是使用属性中的样式</li>
        </div>
        <SCript>
        var vm=Vue.createApp({
            data() {
            return {
                c1: "cla1",
                c2: "cla2",
                c3: {
                cla1: true
                },
                sty1: {
                color: '#5c7cc2'
                }
            };
            },
        }).mount("#app2");
        </SCript>
    </body>
    ```

##### 给class和style配条件
1. 需要注意的是
```
<head>
    <style>
      .cla1 {
        color: yellow;
      }
    </style>
</head>
<body>
  <div id="app1">
    <div>
      <span @click="title=1">点击修改title值</span>
    </div>
    <div>
      <span :style="title === 1 ? sty1 : {  } ">1、根据title值设置style</span>
      <span :class="{cla1: title==1}">2、根据title值设置class样式</span>
    </div>
  </div>
    <SCript>
      var vm=Vue.createApp({
        data() {  // 属性
          return {
            title: 0,
            sty1: {
              color: "yellow",
            }
          };
        },
      }).mount("#app1");
    </SCript>
</body>
```
1. 补充：
   需要注意的是 `:class=` 后面接的是 `{}` 包裹的是css里面的样式和条件；接变量名就是获取的属性；如果像接变量名配条件就需要写成上面style那样的三元表达式，三元表达式里面没有样式用 `{}` 表示，要样式，只能用属性，不能直接用css样式。
   此外，接的是 `{}` 时，可以有多个样式，用逗号隔开。

#### 条件指令v-if
1. 使用 `v-if` 来使得元素条件显示，类似的还有 `v-show` 
    ```
    <body>
    <div id="app1">
        <div v-if="num1==1">第一层循环1</div>
        <div v-else>
        第一层循环2
        <p v-if="num1==2">第二层循环1</p>
        <p v-if="num1==3">第二层循环2</p>
        </div>
        <button @click="num1+=1"> 修改属性值{{num1}}</button>
    </div>
        <SCript>
        var vm=Vue.createApp({
            data() {  // 属性
            return {
                num1: 0,
            };
            },
        }).mount("#app1");
        </SCript>
    </body>
    ```
#### 列表指令v-for
1. 使用 `v-for` 来循环列表属性的值，需要序号，可以加一个key，如 `people,key in list1`
```
<body>
  <div id="app1">
    <table>
      <tr>
        <th>姓名</th>
        <th>年龄</th>
      </tr>
      <!-- 循环列表属性list1 -->
      <tr v-for="people in list1">   
        <td>{{people.name}}</td>
        <td>{{people.age}}</td>
      </tr>
    </table>
  </div>
    <SCript>
      var vm=Vue.createApp({
        data() {  // 属性
          return {
            list1: [   // json格式
              {"name":"小明", "age":"18"},
              {"name":"小白", "age":"15"},
              {"name":"小亮", "age":"17"},
            ]
          };
        },
      }).mount("#app1");
    </SCript>
</body>
```