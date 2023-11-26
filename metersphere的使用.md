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

## 接口测试

### 接口测试基本设置

#### 新建一个场景

1. 新建一个场景并填写基本信息
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_1.png)
 &emsp;
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_2.png)

#### 配置环境

1. 入口
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_3.png)
 &emsp;
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_4.png)

1. 配置http项：注意是https还是hhtp
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_5.png)

1. 配置数据库：没有sql请求不需要配置
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_6.png)

#### 请求预设

1. 共享cookie：和jmeter的一样，但如果有csrf认证或者其他需要后面接口提供cookie的，可以不勾选。
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_7.png)
 我这里需要csrf认证，第一个接口提供csrf_token，返回的cookie我不需要，所以不勾选，不然会覆盖后面登录接口的cookie，所以我的cookie是通过参数传递的
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_8.png)
 &emsp;
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_9.png)
1. 失败继续：这个不多说
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_10.png)

#### 场景变量

1. 普通变量：入口
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_11.png)
 添加变量：关闭窗口自动保存
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_12.png)
 使用变量：`${变量名}`  
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_13.png)
1. 列表变量：只有一个值要写成`1,`  
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_14.png)
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_15.png)
 主要用在for循环，这里用变量不用加`${}`  
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_16.png)
1. csv文件变量：这里的变量名称无所谓，到时候取值看的是csv文件的行名称作为变量；其次是如果文件带中文，要GBK编码
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_17.png)

### 添加请求
#### 自定义请求
1. 入口：这个需要注意的是，要点击空白处才会出现，点击某个请求了再点击这个出来的就是断言提取这些操作  
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_18.png)
1. 把下面几个填了：请求体内部可以直接使用变量，和jmeter一样  
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_19.png)
 请求头有特殊参数的，要传入，比如上面说的不贡献cookie，就要自己传  
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_20.png)
1. 请求处理：断言  
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_21.png)  
 选择jsonpath断言：比正则方便  
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_22.png)
 如果你跑过一次了，也可以选择获取推荐断言，就不用手输了。  
 jsonpath的使用可以在这个网站试试：[jsonpath测试](http://www.e123456.com/aaaphp/online/jsonpath/ "http://www.e123456.com/aaaphp/online/jsonpath/")
1. 请求处理：提取
  ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_23.png)
  和断言操作类似，点击复制可以直接把提取的变量粘贴使用。

#### 导入
1. 当一个场景用法固定，我们就可以把这个场景作为公共的请求场景，比如登录、增删改查一些数据等等。有一个前提是导入的场景不可修改，要修改的话就只能复制。此外导入的场景也要选择环境才能运行。略

#### 循环
1. 次数循环：略
2. for循环：列表变量讲了，这里不讲
3. while循环：
 首先需要通过自定义脚本设置循环初始值：  
  ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_24.png)  
 再设置循环条件：循环时间是总循环时间，超过这个时间就算没有循环完也要终止  
  ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_25.png)
 循环值累加：注意变量都是文本格式，需要转换类型  
  ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_26.png)
#### jsonpath语法
1. 在断言和参数提取的时候，可能需要用到jsonpath语法，网上有说明，这里给个基本示例：获取data下的content列表中name等于myname的id，有时候这里的变量 `${myname}` 可能需要加上引号 `"${myname}"` 才生效，原因可能和数据类型有关。
    ```
    $.data.content[?(@.name==${myname})].id
    ```
## 单接口封装
1. 说明：
    这里说下我的一个思路，我们通常需要对单接口进行封装，以便我们在进行集成测试的时候引用这些接口，这样方便统一管理。又知道集成测试分成正向测试和反向，所以我们的场景一定要能兼容这两种情况。
### 单接口
1. 单接口参数尽量变量化
1. 在接口请求上添加一个自定义脚本说明出入参和入参设置，然后不启用该脚本
1. 引用环境
1. 不设置断言
### 环境管理
1. 说明：为了尽量让单接口解耦，所以我单接口封装尽量简单，同时为了场景灵活多变，我把集成测试中出现的变化尽量都放在了环境中（虽然感觉还是有很多问题，目前能想到最灵活维护还算轻松的方式）
#### 请求头的灵活性
1. 在环境中通过条件启动设置差异化的http配置，可实现不同请求http配置不一样，解决了比如登录不需要token，其他请求需要token的问题
#### 请求体的灵活性
1. 我们引用单接口的时候需要自己添加一个自定义脚本并复制单接口中的说明脚本进行修改。目前只适合逻辑性的异常场景，对于请求结构性的异常场景是不适合的。
#### 断言的灵活性
1. 在环境中设置全局性的断言，且断言值设置为变量。这里其实默认了返回值的格式必须固定了。
1. 在环境通用设置中设置断言变量和值，值默认是正向断言值，但我们需要异常断言的时候，只需要在单接口脚本中重设断言变量进行覆盖就行了。

## 自定义脚本
### 自定义脚本基础规则
1. ms的自定义脚本支持beanshell、python、groovy（java）、js，当我们选择其中一种语法，其实就是选择了该语法和beanshell的混合语法，比如我们使用python，则脚本既能输入python语法也能输入beanshell语法，但是某一行只能使用其中一种，需记住beanshell语法都是 `;` 号结尾。

### 变量

#### 列表变量常识

1. 获取列表元素或者整个列表：方式是`列表变量名_index`，图中a和b都是获取第一个元素，all是获取整个列表
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_27.png)

 如果我们项把index作为变量，有两种方式，一种就是通过`${变量}`的方式，还有一种是把整个`列表变量名_index`作为变量：上下两种方式效果一样
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_28.png)

#### 创建列表变量&添加元素

1. 创建列表变量
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_29.png)
1. 往列表变量中添加元素
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_30.png)

#### 获取列表变量元素

1. 先设置列表变量：这里创建了一个列表变量dataTypeList，后面的 `_${数字}` 是在列表变量中的index
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_31.png)

 如果我们需要控制index，可以加入循环变量：注意，下面注释的那种方式 `i` 不生效，原因暂不清楚。
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_32.png)
1. 循环列表变量：循环的变量可以通过两种方法获取，推荐上一种，下面的只适合非列表变量。
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_33.png)
1. 直接获取列表变量：不需要循环的时候可以用这种方式
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_34.png)

 要控制获取列表变量的index，可以加入java变量：
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_35.png)
1. 补充：通过字符串创建列表，这样更方便
 先通过脚本传入特定格式的文本变量：
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_36.png)

 再转化成列表变量：
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_37.png)

### 自定义脚本问题汇总

#### json转义错误

1. 如果一个脚本参数是json，正常情况下直接转义作为参数即可，但如果json参数本身里面还要转义，多重转义会导致数据格式错误。这个时候就需要一些特殊的转义方式：比如转义一次再`\\\`换成`\\\\\\`，具体情况要根据json内部参数转义次数而定
 ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/metersphere的使用_38.png)

#### python语法糖
1. ms自定义脚本不能使用python语法糖，比如格式化字符串的`f`，只能用`format`。
