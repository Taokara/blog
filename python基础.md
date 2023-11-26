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
</style>
## vscode使用python
### 导入三方库
1. 说明
	有时候vscode并不能通过快捷键安装三方库，我们要自己通过pip安装，但是pip默认安装到python默认的site-packages文件夹下，而我们创建的项目是新建了个虚拟环境venv，python的环境和虚拟环境是隔离的，所以我们安装的时候要指定安装路径，同时还可以指定版本和仓库源
	```
	pip install --target=D:\projectFiles\pythonFiles\tools\venv\Lib\site-packages opencv-python==4.2.0.34  -i  https://pypi.doubanio.com/simple
	```

## 数据类型
### 字符串string
1. 字符串拼接
	```
	a = "天下"
	b = a + "会"    # 天下会
	c = a * 2       # 天下天下
	```
1. 长度
	```
	a = "一二三四五六七八九十"
	b = len(a)      # 10
	```

1. 包含判断in：还有个`not in`
	```
	a = "一二三四五六七八九十"
	b = "五" in a   # True
	```
1. 开头包含判断`startswith`：还有个`endswith`
	```
	a = "一二三"
	b = a.startswith("一")     # True
	c = a.endswith("三")       # True

	#指定开始位置
	c = a.startswith("二",2)   # True
	```
1. 两端删除`strip`
	```
	a = "一一二三一四五一一"
	b = a.strip("一")          # 二三一四五；不限数量
	```
1. 计数`count`：可指定范围，规则和切片一致
	```
	a = "一二二三"
	b = a.count("二")          # 2
	c = a.count("二", 2, 3)    # 1
	```
1. 替换`replace`
	```
	a = "一二三一四五"
	b = a.replace("一","1")    # 1二三1四五
	```
1. 根据索引查找`find`：
	```
	a = "一二三四五"
	b = a.find("三")    # 2
	b = a.find("六")    # -1；没找到
	```
1. 根据索引查找`index`：
	```
	a = "一二三四五"
	b = a.index("三")   # 2
	c = a.index("六")   # 报错；没找到
	```
1. 插入`join`
	```
	a = "一二三"
	b = "|".join(a)     # 一|二|三
	```
1. 分割`split`
	```
	a = "一、二、三"
	b = a.split("、")       # ['一', '二', '三']
	b = a.split("、", 1)    # ['一', '二、三']；分割一次
	```
1. 大小写转化`lower`和`upper`
	```
	a = "abcDEF"
	b = a.lower()      # abcdef
	c = a.upper()      # ABCDEF
	```
1. 去重生成无序列表 `set`
	```
	a = "aabbcc"
	set(a)  # ["b","c","a"]
	```
---
1. 方法组合使用
	```
	a = "一、二、三"
	b = a.replace("、", "|").join("12")  # 1一|二|三2
	```
---
1. 切片：永远从左边作为起点
	```
	a = "一二三四五六七八九十"

	# 从0开始，右开区间
	b = a[2]          # 三
	c = a[0:1]        # 一

	# 取到最左最右
	d = a[0:]         # 一二三四五六七八九十
	f = a[:1]         # 一

	# 步长
	e = a[0:5:2]      # 一三五
	g = a[5:0:-2]     # 六四二
	h = a[::-1]       # 十九八七六五四三二一
	```
---
1. 格式化字符串
	```
	a = "8"
	b = "夏天"
	c = f"你好，{a}月的{b}"      # 你好，8月的夏天
	```
1. 转义
	```
	# 换行符
	a = "一二三四五\n六七八九十"  # 两行显示

	# 去转义
	a = r"一二三四\n五六七八九十" # 转义符失效
	```
### 列表list
1. 长度`len`
	```
	lst1 = ["一", "二", "三"]
	a = len(lst1)     # 3
	```
1. 最大最小值`max`和`min`：一般只能比较数值列表
	```
	lst1 = [1, 2, 3, 4, 5]
	a = max(lst1)     # 5
	a = min(lst1)     # 1
	```
1. 逆列表`reverse`
	```
	lst1 = ["一", "二", "三"]
	lst1.reverse()
	print(lst1)              # ['三', '二', '一']
	```
1. 排序`sort`：这个可以设置复杂的规则
	```
	lst1 = [(2, 2), (3, 4), (4, 1), (1, 3)]

	# 排序规则：单个元素处理
	def takeSecond(elem):
	    return elem[1]

	# key表示单个元素处理规则，reverse表示降序排
	lst1.sort(key=takeSecond,reverse=True)  # 使用第二个元素大小倒序排列

	print(lst1）    # [(3, 4), (1, 3), (2, 2), (4, 1)]
	```
1. 合并：等同`extend`，但`extend`合并字符串会变成单字符
	```
	lst1 = ["一", "二", "三"]
	a = lst1 + ["四", "五"]   # ['一', '二', '三', '四', '五']
	```
1. 添加元素append
	```
	lst1 = ["一", "二", "三"]
	lst1.append("四")
	lst1              # ['一', '二', '三', '四']
	```
1. 替换
	```
	lst1 = ["一", "二", "三"]
	lst1[2] = "四"
	lst1              # ['一', '二', '四']
	```
1. 元素插入`insert`
	```
	lst1 = ["一", "二", "三"]
	lst1.insert(2, "四")
	lst1              # ['一', '二', '四', '三']
	```
1. 插入`join`：和字符串的一样，这里只是把列表当作字符串
	```
	lst1 = ["一", "二", "三"]
	a = "|".join(lst1)        # 一|二|三
	```
1. 判断包含`in`：还有`not in`
	```
	lst1 = ["一", "二", "三"]
	a = "二" in lst1  # True
	```
1. 通过索引查元素
	```
	lst1 = ["一", "二", "三", "四", "五", [1, 2, 3]]
	a = lst1[1]      # 二

	#倒查
	b = lst1[-2]     # 五

	#多层查
	c = lst1[5][1]   # 2
	```
1. 通过元素查索引`index`：没找到报错
	```
	lst1 = ["一", "二", "三"]
	a = lst1.index("二")      # 1
	```
1. 通过索引删除：不给索引删除末尾
	```
	lst1 = ["一", "二", "三"]
	a = lst1.pop(1)  # 二；返回删除的元素
	lst1             # ['一', '三']
	```
1. 通过元素删除：有重复的就删除第一个
	```
	lst1 = ["一", "二", "三"]
	lst1.remove("二")
	lst1             # ['一', '三']
	```
1. 切片：和字符串的一致，略讲
	```
	lst1 = ["一", "二", "三", "四", "五"]
	a = lst1[2:4]    # ['三', '四']
	```
1. 注意：列表被引用指向同一个列表对象，其他变量引用后操作会影响原列表
	```
	list1 = ["dog", "cat", "elephant"]
	list2 = list1
	list2.remove("dog")
	print(list1)  #  ["cat", "elephant"]
	```
	其实字符串也是同一个对象，但是由于字符串创建后就不能修改了（比如 `s1[0] = 'H'` 这样的操作是不允许的），所有操作其实都是拷贝成新的对象了，所有就不存在这个问题。
	```
	list2 = list1[:]  # 这样引用就不会影响原列表
	```
### 元组tuple：不可修改，查询和列表一样
1. 代码
	```
	tup1 = (1,)      # 一个元素要加`,`
	```
### 字典dict
1. 根据key查询value：没查询到报错
	```
	dic1 = {"No1":"1", "No2":"2", "No3":"3"}
	a = dic1["No1"]            # 1
	```
1. 根据key查询value`get`：没查询到返回None
	```
	dic1 = {"No1":"1", "No2":"2", "No3":"3"}
	a = dic1.get("No1")        # 1
	```
1. 根据key查询插入`setdefault`：查询到就返回value，没查到就插入None值键值对，也可设置Value插入
	```
	dic1 = {"No1":"1", "No2":"2", "No3":"3"}
	a = dic1.setdefault("No3")        # 3；查询到
	b = dic1.setdefault("No4")        # None；查询到没有，返回插入的'No4': None的value
	c = dic1.setdefault("No5", "5")   # 5；查询到没有，返回插入的'No5': 5的value
	dic1             # {'No1': '1', 'No2': '2', 'No3': '3', 'No4': None, 'No5': '5'}
	```
1. 更新`update`：重复的会替换
	```
	dic1 = {"No1":"1", "No2":"2", "No3":"3"}
	dic1.update({"No3":"3.1", "No4":"3"})  # {'No1': '1', 'No2': '2', 'No3': '3.1', 'No4': '3'}
	```
1. 删除`pop`：没有对应的key会报错
	```
	dic1 = {"No1":"1", "No2":"2", "No3":"3"}
	dic1.pop("No3")
	dic1             # {'No1': '1', 'No2': '2'}
	```

1. json文件转化成字典：不管有多少层，都会转化成字典的键值对，有重复的key，会取后者
	```
	#下面这个是json1.json文件内容
	"""
	{ "user": {
	    "No1": {
	      "name": "zhangsan"
	      },
	    "No2": {
	      "name": "lisi"
	    },
	    "No2": {
	      "name": "lisi2"
	    }
	  }
	}
	"""

	import json
	with open("json1.json",mode="r+",encoding="utf-8") as f:
		rows = f.read()        # 读取整个json文档
	dct1 = json.loads(rows)    # {'user': {'No1': {'name': 'zhangsan'}, 'No2': {'name': 'lisi2'}}}

	# 字典转化成json：虽然内容还是和刚才的字典一样，但是已经不能使用字典的方法了
	json1 = json.dumps(dct1)   # {"user": {"No1": {"name": "zhangsan"}, "No2": {"name": "lisi2"}}}
	```
## 数据类型转化
1. 转整数
	```
	# 字符串转整数
	a = "123"
	b = int(a)

	# 小数转整数
	a = 3.7
	b = int(a)  # 3
	```
1. 转字符串
	```
	a = 123
	b = str(a)
	```
1. 字符串转列表
	```
	string = "abc"
	my_list = list(string)  # ['a', 'b', 'c']
	```

1. 列表元组互转
	```
	a = ("一", "二", "三")
	b = list(a)
	c = tuple(b)
	```
1. 字典转列表
	```
	# 转化成键值对表、key表、value表
	dic1 = {"No1":"1", "No2":"2", "No3":"3"}
	a = list(dic1.items())     # [('No1', '1'), ('No2', '2'), ('No3', '3')]
	b = list(dic1.keys())      # ['No1', 'No2', 'No3']
	c = list(dic1.values())    # ['1', '2', '3']
	```
## 数据类型判断
1. 示例
	```
	isinstance("二", str)       # 返回True
	```
## 计算
1. 示例
	```
	a = 5/2    # 正常除：2.5
	b = 5 % 2  # 取余：1
	c = 5//2   # 取整：2
	d = 3**2   # 平方：9
	x += y     # x = x + y
	```

## 循环控制
### if
1. 代码：可以使用`and`、`or`和多个逻辑符`0<a<10`
	```
	if a == 2:
		a = 0
	elif a == 3:
		a = 1
	else:
		a = "其他"
	```
### for
1. 示例：`in`后面可以跟list、tuple和string
	```
	for i in range(10):       # range函数和切片一样，分隔符是`,`
		a = i + 1
	else：                    # else只有for循环“正常”结束才会执行，有break就不会执行。但如果只是接在for循环后面的普通语句，不管for循环是否正常结束都会执行。
		print("循环正常结束")
	```
1. break和continue
	```
	for i in range(10):
        print(i)
        if i > 5:
            break             # 跳出当前循环，执行循环下面的内容，不影响外层循环

	for i in range(10):
        print(i)
        if i > 5:
            continue          # 跳过continue下面循环的内容，进行下次循环
		print("完整的一次")
	```
1. 列表推导式
	```
	squares = [x**2 for x in range(4)]  # [0, 1, 4, 9]
	```
	等同于：
	```
	squares = []
	for x in range(4):
		squares.append(x**2)
	```

1. 注意：循环的列表不能变动，不然后按照第一次的列表进行，容易发生out of index。
### while
1. 示例
	```
	a = 1
	while a <= 10:
		a = a + 1
	else：
		a = 0
	```
## 变量交换赋值：python内存结构和java差不多
1. 示例：语法糖
	```
	a = 1
	b = 2
	a, b = b, a   # a=2, b=1
	```
## 输入input：字符串数据类型
1. 示例
	```
	a = input("请输入：")
	```
## 打印print
1. 打印结尾：任意字符串；默认是\n，即换行；\t表示不换行
	```
	for i in range(10):
		print(i, end="\t")
	```
1. 打印间隔：任意字符串
	```
	print("你好","朋友们","拜拜",sep="|")  # 你好|朋友们|拜拜
	```
## 方法
### 基础结构
1. 示例
    ```
    def method1(a, b):
        """
        :param a: 加数1
        :param b: 加数2
        :return: 和
        """
        c = a + b
        return c
    ```
2. 返回多个值：需要解构获取值
    ```
    def method1(a, b):
        c = a + b
        d = a * b
        return c, d

    e = method1(1,2)        # (3, 2)
    f, g = method1(1,2)     # 解构：f：3  g：2
    ```
### 参数
1. 方法参数默认值：默认值参照要放后面，不然传参不知道是重新赋值还是给的后面参数的值
    ```
    def method1(a, b=2):
        c = a + b
        return c
    ```
1. 可变参数：也可以叫元组参数
    ```
    def method1(*b):        # b=(1, 2, 3)，是数组
        s = 0
        for i in b:
            s = s + i
        return s

    f = method1(1, 2, 3)     # 6
    ```
1. 关键字参数：字典参数
    ```
    def method1(**b):
        c = b.get("name")
        d = b.get("age")
        return c, d

    dict1 = {"name": "zhangsan", "age": "18"}
    f = method1(**dict1)    # ('zhangsan', '18')，传参必须加`**`
    ```
1. 参数注解：
    ```
	# 方法参数类型限定，返回str类型（不返回是None）
    def method1(a: int, b: str) -> str:
        return f"b {a}"

	# 变量类型注解，a变量是int类型
	a: int = 10
	print(a)
    ```
### 匿名函数
1. 不可被引用的方法
    ```
	# 1. def定义方法
	def add(a, b):
		return a + b
	# 调用
	print(add(1,2))

	# 2. lambda定义方法：分别是入参变量，逻辑，入参
	print((lambda a, b: a + b)(1, 2))
    ```
### 闭包
1. 说明
	非闭包的方法存在全局变量，变量容易被修改，函数结构独立性不高的问题。这里是一个简化的赚钱函数，最后结果是15。
	```
	money = 0
	def sum(x):
		print(money + x) 

	sum(5)
	sum(10)
	```
    
	下面是闭包结构：闭包结构的核心是返回函数，outer函数把参数x值传入到inner函数中，然后返回inner函数，相当于在调用这个函数，只是这个函数目前还没有参数y，first = outer(10)相当于first = inner（已经有x值了），second = first(5)相当于second = inner(5)（已经有x值了）
	```
	def outer(x):
		def inner(y):
			return x + y
		return inner

	first = outer(10)
	second = first(5)
	print(second)  # 输出：15
	```
1. 修改外部函数
	上面的例子，inner函数只能读取outer函数内的变量，不能修改，修改会提示没有定义这个 `x` 变量(UnboundLocalError)，要修改需要使用关键字 `nonlocal `。
	```
	# 累加x
	def outer(x):
		def inner(y):
			nonlocal x
			x = x + y
			print(x)
		return inner

	a = outer(1)
	a(1)
	a(1)
	```
	nonlocal只能针对闭包结构，如果不是闭包结构，需要 `global` 关键字：
	```
	x = 10

	def add():
		global x 
		x += 5
		print(x)

	add()  # 输出 15
	```

### 装饰器
1. 说明：
	装饰器就是使用闭包函数来增加原函数功能的
	```
	def outer(func):
		def inner():
			func()  # 调用原函数
			print("新添加的功能")  # 新增功能

		return inner

	@outer		# 装饰原函数
	def old():
		print("原来的功能") 

	old()    # 输出 "原来的功能  新添加的功能"
	```
### 递归
1. 示例：斐波那契数列是指前两项之和是第三项的值，如0, 1, 1, 2, 3, 5, 8, 13...，求第n项的值
	```
	def fibonacci(n):
		if n <= 1:
			return n
		else:
			return fibonacci(n-1) + fibonacci(n-2)

	# 测试
	print(fibonacci(10)) # 输出 55
	```

## 类（封装）
### 类的属性
1. 说明
    类中的属性实际上就是类中的变量，实例化后通过`实例.变量名`获取值。类属性始终只有一个，不同实例化获取的也是该值
1. 示例
   ```
   class Human:
        name = "张三"
   
   # 调用属性
   person1 = Human()  # 切记！实例化必须带括号，不然相当于给类重命名了
   person1.name       # 张三
   
   # 修改(增加)属性：不影响其他实例化对象的属性
   person2 = Human()
   person2.name = "李四"
   person2.weight = "100kg"
   
   person3 = Human
   person3.name       # 张三
   ```
### 构造函数（__init__）
1. 说明
    类的属性主要为类中的方法提供参数，这样就尽量减少了类内部对外的依赖。但是如果这些参数通过一个个修改类属性的方式传进去其实并不便捷和安全，因此通过创建一个统一的参数传入口就显得比较好。下面做个比较。
1. 构造器：
    - 说明：构造函数（构造器）是在类实例化自动运行的一个函数，其参数可通过实例化类传入，`__init__`中的下划线表示该方法私有，不可被外部调用。最后就是该函数不能使用`return`。
    - 示例：
      ```
      """ 修改属性传参入类 """
      class Human:
        name = "张三"

      def run(self, fast):
        print(self.name + "跑得" + fast)
      
      someone = Human()
      someone.name = "李四"
      someone.run("非常快")
      ```
      init方法刨除上面说的特性，就是一个普通函数，这里就相当于在函数里面进行属性设定了
      ```
      """ 通过构造函数传参 """
      class Man:
        def __init__(self, name):
           self.Name = name

        def run(self, fast):
           print(self.Name + "跑得" + fast)

      someone = Man("李四")
      someone.run("非常快")
      ```

### self关键字
1. 说明
    当参数还没实例化的时候，类内部要代替实例调用类属性或者方法就需要self。
2. 示例
   ```
   class Man:
     name = "张三"

     def run(self, fast):
        print(self.name + "跑得" + fast)
   ```
1. self作为类方法参数的意义
   - 所有的类内部方法第一个参数都是self，主要是因为内部实现方式导致的。当我们调用一个类方法，形如`zhangsan.run("很快")`，我们知道，这个run方法在类中定义大致是`run(self, fast)`,当我们调用run之后，python实际运行的是`Human.run(zhangsan, "很快")`，这个Human是类��，也就是说，self起占位的作用。

### 私有变量和方法
1. 示例：变量和方法前有 `__` 就是私有，只能类内部使用
	````
	class MyClass:
		def __init__(self):
			# 私有变量
			self.__private_var = 0

		# 私有方法
		def __private_method(self):
			print("This is a private method.")

		def public_method(self):
			print("This is a public method.")
			self.__private_method()  # 内部方法使用私有方法
			self.__private_var = 10  # 内部方法修改私有变量的值
			print("Private variable:", self.__private_var)


	obj = MyClass()
	obj.public_method()
	```

## 子类（继承）
### 基础结构
1. 示例
	```
    # 可继承init方法、改写父类方法
    class Chinese(Human):
        def run(self, fast):
            return f"中国人{self.name1}跑得{fast}"
    
    
    someone = Chinese("张三")
    someoneRun = someone.run("快")    # 中国人张三跑得快
    print(someoneRun)
	```
### 多继承
1. 示例
	```
	class ParentClass1:
		def method1(self):
			print("ParentClass1 method1")

	class ParentClass2:
		def method2(self):
			print("ParentClass2 method2")

	# 继承上面两个类
	class Subclass(ParentClass1, ParentClass2):
		pass

	obj = Subclass()
	obj.method1()  # Output: ParentClass1 method1
	obj.method2()  # Output: ParentClass2 method2
	```

### 调用父类方法super关键字
1. 示例
	```
	class ParentClass:
		def __init__(self):
			self.parent_attribute = "Parent Attribute"

		def parent_method(self):
			print("Parent Method")

	class ChildClass(ParentClass):
		def __init__(self):
			super().__init__()  # 调用父类的构造函数
			self.child_attribute = "Child Attribute"

		def child_method(self):
			super().parent_method()  # 调用父类的方法
			print("Child Method")


	obj = ChildClass()

	# 通过子类实例访问父类的属性
	print("Parent Attribute:", obj.parent_attribute)

	# 通过子类实例调用父类的方法
	obj.parent_method()

	# 调用子类的方法
	obj.child_method()
	```

### 多态
1. 示例：父类提供一个壳子，具体实现看子类
	```
	class Animal:
		def sound(self):
			pass

	class Dog(Animal):
		def sound(self):
			return "汪汪!"

	class Cat(Animal):
		def sound(self):
			return "喵喵!"

	def make_sound(animal):
		print(animal.sound())

	# 创建不同的对象
	dog = Dog()
	cat = Cat()

	# 调用方法，实际输出的声音根据对象的类型而定
	make_sound(dog)  # 输出：汪汪!
	make_sound(cat)  # 输出：喵喵!
	```

## 设计模式
### 单例模式
1. 说明：
	不同的实例会占用内存，因此单例模式就是把一个实例化对象在不同模块中引用赋值，这样就能减少内存使用，比如我们在 `test.py` 模块中创建一个实例
	```
	class Human:
		pass

	p1 = Human()    # 创建p1实例
	```
	然后在 `test2.py` 模块导入 `p1` 并赋值给其他变量
	```
	from test1 import p1

	P2 = p1    # 赋值给p2
	```
### 工厂模式
1. 说明：
	所谓工厂模式就是通过一个中间类的函数来统一管理类的实例化，这样可以统一管理类的实例化，比如需要在实例化修改或者添加一个参数，就不用去实例化的地方一个个改，而只需要改中间类中的函数。
	```
	class Dog:
		def speak(self):
			return "汪!"

	class Cat:
		def speak(self):
			return "喵!"

	# 使用工厂模式
	class AnimalFactory:
		def create_animal(animal_type):
			if animal_type == "dog":
				return Dog()  # 返回对应的类
			elif animal_type == "cat":
				return Cat()

	animal_factory = AnimalFactory()
	animal3 = animal_factory.create_animal("dog")  # 调用中间类的函数进行实例化
	print(animal3.speak())  # 输出 "汪!"

	animal4 = animal_factory.create_animal("cat")
	print(animal4.speak())  # 输出 "喵!"  
	```
## 多进程和多线程
1. 说明
	多进程是可以调用多个核心的，是正真的同时执行，而多线程由于存在GIL锁，实际上只能调用一个核心，交替执行线程。但是，如果是读写比较频繁的活动，由于读写本身比较耗时间，调用多个核心和单个核心没什么区别，反而反复多开核心耗时要久一点，而如果是计算比较多的活动，多进程的多核心就比较快了。
### 多进程
1. 示例
    ```
    import multiprocessing
    import time

    def worker(num):
        """进程执行的任务"""
        time.sleep(1)
        print('Worker %d is running' % num)

    # 不使用多进程，耗时久
    # if __name__ == '__main__':
    #     for i in range(10):
    #         worker(i)

    # 使用多进程，耗时短
    if __name__ == '__main__':
        # 创建进程池，指定进程数为4，即每次执行4个线程
        pool = multiprocessing.Pool(processes=4)
        # 创建10个任务，交给进程池处理
        for i in range(10):
            pool.apply_async(worker, args=(i,))
        # 关闭进程池
        pool.close()
        # 等待所有任务完成
        pool.join()
    ```
1. 显示进程id
    ```
    # 显示进程id
    print(os.getpid())
    
    # 显示父进程id
    print(os.getppid())
    ```  
### 多线程
1. 示例
	```
	from time import sleep
	import threading

	def dog(sound):
		while True:
			print("狗叫：" + sound)
			sleep(1)
			

	def cat(sound):
		while True:
			print("猫叫：" + sound)
			sleep(1)

	dog_thread = threading.Thread(target=dog, args=("汪",))  # target是方法名，args是元组传参
	cat_thread = threading.Thread(target=cat, kwargs={"sound": "喵"})  # kwargs是字典传参
	dog_thread.start()  # 启动多线程任务
	cat_thread.start()
	```
## 异常处理
1. 说明
	异常具有传递性，比如a方法调用了b方法，那b报错可以被a方法中的异常捕获抛出

1. 不限定错误类型
	```
    a = "你好"
    try:
        b = a + 123
    except:                # 报错就执行下面的语句
        print("有错误！")
	```
 1. 限定错误类型
	```   
    a = "你好"
    try:
        print(c)  # NameError       # 有一个错误就不再检查下面的
        b = a + 123   # TypeError
    except(TypeError, NameError):   # 限定错误类型，否则还是报错
        print("有错误！")
	```
 1. 打印错误
	```    
    a = "你好"
    try:
        print(c)
        b = a + 123 
    except TypeError as f:     # 打印错误
        print(f)
    else:
        print("其他异常！")
    finally:
        print("异常排除结束")    # 用于执行固定语句，如关闭连接等
	```
## 读写文件
1. 示例
	```
    # 打开文件读取所有行，一行为一个列表元素
    with open("text.txt", mode="r+", encoding="utf-8") as f:
        rows = f.readlines()[1:]  # ['第二行\n', '第三行']；[1:]表示第二行到末尾行
    
    # 打开文件逐个列表元素写入
    with open("test2.txt", mode="r+", encoding="utf-8") as g:
        for i in rows:
            g.write(i)  # 会覆盖
	```

## Socket通讯
1. 说明：
   Socket 是计算机网络中实现数据传输的一种通用方法。
### Socket服务端
1. 示例：这里创建了一个Socket服务器，进行简单的消息监听和回复。
	```
	import socket

	# 创建socket对象
	socket_server = socket.socket()
	# 绑定ip地址和端口
	socket_server.bind(("localhost", 8888))
	# 监听端口
	socket_server.listen(1)  # 数字表示连接数量
	# 等待客户端连接：如果没有客户端连接，将阻塞在这里
	conn, address = socket_server.accept()  # 返回一个元组，第一个元素是客户端的socket对象

	print("客户端连接到了！")

	# 接收客户端信息
	data: str = conn.recv(1024).decode("utf-8")  # resv接受的参数是缓冲区大小，一般是1024；其返回值是字节数组，需要转换成UTF-8编码

	print(f"客户端回复的消息是：{data}")
	# 回消息给客户端
	msg = "自动回复的消息！"
	conn.send(msg.encode("utf-8"))

	# 关闭连接
	conn.close()  # 关闭客户端连接
	socket_server.close()  # 关闭socket对象，不关闭还能接受下一个客户端连接
	```
1. 客户端
   我们上面只创建了服务器，这里需要用一个三方的客户端和我们创建的服务器连接沟通。
   下载这个三方客户端：https://github.com/nicedayzhu/netAssist/releases
   配置如下：
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/python基础_1.png)

### Socket客户端
1. 示例：
	```
	import socket

	# 创建socket对象
	client_socket = socket.socket()

	# 连接服务器
	client_socket.connect(("localhost", 8888))

	# 发送消息给服务器
	message = "你好，我是客户端!"
	client_socket.sendall(message.encode("UTF-8"))

	# 从服务器接收消息
	response = client_socket.recv(1024)
	print("服务端回复的消息是:", response.decode("UTF-8"))

	# 关闭socket连接
	client_socket.close()
	```