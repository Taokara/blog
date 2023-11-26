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
### java常识
#### java编译
- java程序，先要保存成 .java的源文件，然后通过`javac`命令编译成 .class字节码文件，然后通过`java`命令运行得到结果。直接在命令行窗口使用这些命令就行。
- 每个class类会生成一个`.class`字节码文件
- java是编译和解释型语言，首先是因为要编译成字节码，所以叫编译型，其次字节码也不是机器能识别的语言，而是需要到虚拟机JVM中解释给机器，所以也带有解释型语言的特点。

#### java命名规则
- 包名myname
- 变量/方法myName
- 类名MyName

### java依赖
&emsp;&emsp;首先我们创建java项目的时候，要选择创建maven项目，而不是java项目，maven项目是在java项目的基础上添加了maven依赖管理，创建的java项目会多一个pom文件，pom文件是我们依赖配置信息和下载地址
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_1.png)
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_2.png)
	&emsp;&emsp;当我们存在依赖爆红时，我们需要添加依赖，一般情况下idea通过maven可以自动下载，但有时候还是存在下载不了的情况，这个时候我们需要手动添加依赖。这个时候需要先查到需要添加的jar包或依赖库名，然后在[mvnrepository](https://mvnrepository.com/search?q=+httpmime-4.5.1.jar "mvnrepository")搜索：
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_3.png)
	&emsp;&emsp;进入选择版本并复制依赖配置信息，将配置信息贴到pom文件的依赖中即可：
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_4.png)
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_5.png)
	&emsp;&emsp;需要重新加载依赖，不然贴入的配置信息会爆红：
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_6.png)

#### 创建maven项目并创建层级目录
1. 创建maven项目
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_7.png)

1. 把src文件设成根目录
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_8.png)

1. 允许创建层级目录：去掉勾选
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_9.png)

1. 在src下创建层级包：注意命名和url是反着的
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_10.png)

	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_11.png)


### 创建java类和程序入口
1. 首先在文件下自己建的文件工程下建一个包，然后在包下面建java类
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_12.png)
1. 在类中创建程序入口（快捷键是`psvm`）：;这个程序入口有点像python里面的`if name == main`。红色部分是写的程序
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_13.png)


### 注释
- 单行`//`
- 多行`/*XXX*/`
- 文档注释`/**XXX */`，对方法等进行说明，会生成一个开发者文档，开发中最常用

### 打印
1. 快捷键是`sout`
	```
	System.out.println("123");
	```

### 数据类型
#### char类型
1. 说明&示例：
	单个字符类型，只能用单引号，用于处理单字符的，字符串用String
	```
	char a = '你';
	```
#### char操作
1. 说明&示例：
	char转int：因为int比char容量大，可以无损转换（自动转换），可以转回去，但是低转高会导致精度损失和内存溢出（强制转换）。
	```
	// 转换
	char a = '你';
	int c = (int)a;
	int d = a + 1;  // 计算转换

	// 内存溢出
	int a = 128;
	byte d = (byte)a;  //-128：byte(-128到127)，所以int128转成byte超过最大值，只能从头开始，就是-128。这就叫内存溢出。
	```
#### 小数float
1. 说明：
	这个一般不用，会四舍五入，一般用Bigdecimal类。
#### 字符串String
1. 与python中一样，但变量须声明类型！
	```
	String name = "123";
	```
	注意：不是说变量一定要赋值，和python不一样，这里只要先申明变量类型也是可以的，赋值后面再赋
	```
	String name;
	name = "123";
	```
	注意：下面这种也能创建变量，但区别在于下面这个变量是在内存中重新创建的。java其实有很多省内存和耗时的设计，当我们创建一个变量的值在内存池中已经存在，java不会新建一个值，而是直接指向这个内存空间，所以在一个程序中同一个值的变量用的是同一个内存空间。但是如果我们用下面new方法创建的，就不会使用别人的值，而是直接生成新的值。
	```
	String name = new String("123");
	```
#### 字符串String与StringBuilder类的区别
1. String类说明：
	当我们对String类进行操作的时候，其实并不会修改原来的String对象，而是重新赋值到了一个新的String对象上。结果就是内存中多了很多匿名对象。如果只是对String进行少量操作，则没有关系。
1. StringBuilder类说明：
	StringBuilder类针对的是同一个对象进行的操作，所以性能更好，但使用不如String类方便。
#### 字符串操作
1. 获取字符串长度：
	```
	String a = "12345";
	int b = a.length();
	```
1. 字符串切片：b打印出来是"abc"。"c"的索引是2，但用3就能把右边界值"c"取到
	```
	String a = "abc";
    String b = a.substring(0,3);
	```
1. 字符串包含：返回布尔
	```
	String a = "abc";
	String b = "123abc123";
	boolean c = b.contains("abc");   //返回true
	```
1. 字符串包含：返回索引
	```
	String a = "abc";
	String b = "123abc123";
	int c = b.indexof("abc");   //返回3，如果没找到返回-1
	```
1. 替换：replaceAll，从新生成一个变量
1. 分割：split，注意特殊字符分割要转义

#### 整数int
1. 说明&示例：
	```
	int name = 123;
	```
#### 随机数
1. Math.random()：生成 [0-1) 之间的数
	```
	//如果要获取范围[10-99]之间的数
	//首先扩大99倍右区间
	Math.random()*99
	//因为函数娶不到右极值，要加1
	Math.random()*(99+1)
	//然乎扩大10倍左区间
	Math.random()*(99+1)+10
	//但这样右区间也加了10，要减去
	Math.random()*(99+1-10)+10
	```
#### 数据类型转换
1.  **int转化成String**：三种方式
	```
	String str1 = Integer.toString(123);
	String str2 = String.valueOf(123);
	String str3 = "" + 123;
	```
1. **String转化成int**：两种方式
	```
	int number1 = Integer.parseInt("123");
	int number2 = Integer.valueOf("123").intValue();
	```
1. **其他数值转化成int**：
	```
	int a = (int) 12.34;
	```

#### 列表list
1. 说明
   List作为collection的子接口，ArrayList和LinkedList都是继承该接口的类
   - ArrayList用object[]存数据，所以可以放入任何类型
   - LinkedList叫链表，即每个数据还保存下一个数据的地址，而ArrayList存的是index，当我们要经常删除插入数据的时候，前者只需要变动前后的数据即可，但是后者需要修改其后的所有数据的index，所以性能前者更好，但后者适合查询，不用遍历。
1. 创建列表对象：要限制类型参看泛型
	```
	ArrayList list1 = new ArrayList<>();    //ArrayList类的实例化
	List list2 = new ArrayList<>();         //接口多态性的实例化
	```

#### 列表操作
1. 数组或一组值转化为列表
	```
	List list1 = Arrays.asList(99,"张飞",3);  //创建一个初始列表
	```
1. 指定位置插入元素
	```
	List ls = new ArrayList();
	ls.add(0,"小天才");
	```
1. 包含与否
	```
	int idx= list1.indexOf("哈哈");        //判断是否在，返回index，否则-1
	```
1. 列表长度
	```
    System.out.println(list1.size());     //获取列表长度
	```

1. 插入子表与合并表
	```
	List ls = new ArrayList();
	ls.add("小天才");

	List ls2 = new ArrayList();
	ls2.add("大聪明");

	//ls.add(ls2); //[小天才, [大聪明]]
	ls.addAll(0,ls2); //[大聪明, 小天才]
	```
1. 根据索引获取列表元素
	```
	Object obj = ls.get(2); //用Object可获取任意类型元素
	```

1. 根据索引删除元素
	```
	ls.remove(4);
	```
1. 根据索引替换元素
	```
	ls.set(1,"天神");
	```
1. 截取列表
	形成一个新表
	```
	List ls3 = ls.subList(2,3); //取不到右
	```
1. 遍历 
	- 迭代器方式
		```
		ListIterator<String> iter = ls.listIterator();
		String one = iter.next();
		String two = iter.next();
		```
	- 两种for循环方式
		```
	    for(Object i:list1){                   //遍历2
            System.out.println(i);
        }

        for (int i = 0; i < list1.size(); i++) {  //遍历3
            System.out.println(list1.get(i));
        }
		```


#### 集合set
1. 和list唯一不同是值不能重复

#### 数组arrays
1. 数组初始化：这个和列表很像，只是长度固定，且只能存单一数据类型
    - 第一种初始化的方式：直接赋值 
		```
		String[] array = {"小天才1","小天才2","小天才3"};
		```
	- 第二种初始化：默认初始化值，整数是0，
		```
		int[] arr1 = new int[4];   //{0，0，0，0}
		arr1[0]=1;                 //挨个赋值
		```
	- 第三种初始化：
		```
		int[] arr1;
		arr1 = new int[]{1,3,5};
		```
2. 二维数组：`arr1[0]` 代表二维数组的第一行，打印
	```
	int[][] arr1 = new int[][]{{1,2,3,4},{4,5,6},{9}};
	int a = arr1[0];          //a=[I@15b69c2，地址指向数组{1,2,3,4}
	int b = arr1[0][2];       //b=3     
	```
	默认初始化值：整数是0
	- 第一种初始化的方式
		```
		int[][] erwei = new int[3][4];   //3行4列
		```
	- 第二种初始化
		```
		int[][] arr2 = new int[2][];     //先不定每行多少个元素
        arr2[0] = new int[2];            //分别给每行初始化
        arr2[1] = new int[3];
		```
#### 数组操作
1. 转化成列表：这样就可以预置列表数据了
	```
	String[] array = {"小天才1","小天才2","小天才3"};
	List<String> list = new ArrayList<>(Arrays.asList(array));
	list.add("小天才4");
	list.remove(0);      //[小天才2, 小天才3, 小天才4]
	```
1. 获取列表长度
	```
	int[] arr1 = {1, 2, 3, 4, 5};
	len1 = arr1.length   //5
	```
1. 遍历 二维数组
	```
	int[][] erwei = new int[3][4];
	for(int i=0;i<erwei.length;i++){    //二维数组的长度的行数3
		for(int j=0;j<erwei[i].length;j++){
			System.out.print(erwei[i][j]+" ");
		}
		System.out.println();           //每行换行
	}
	```
1. 数组转化成字符串
	```
	int[] arr1 = { 9,6,3,0,1,10,4,5,2,8,7}; 
	Arrays.toString(arr1)           //"[9,6,3,0,1,10,4,5,2,8,7]"
	```

1. 排序（用的快排）
	```
	int[] arr1 = { 9,6,3,0,1,10,4,5,2,8,7};
	Arrays.sort(arr1);             //arr1={0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	```

1. 查找：返回index
	```
	int[] arr1 = { 9,6,3,0,1,10,4,5,2,8,7};
	Arrys.binarySearch(arr1,6)      //1
	```

#### 字典HashMap
1. 录入键值对
	```
	HashMap<Object, Object> users = new HashMap<>(); //两个Object表示Key和Value都是Object类型
	users.put("11", "小天才"); //录入键值对
	```
#### 字典操作
1. 根据key取value
	```
	Object val = map1.get("11");
	```
1. 遍历字典
	```
	for (Object key : users.keySet()) {
		Object val = users.get(key);
		System.out.println( key + ":" + val);
	}
	```
1. 合并字典
	```
	map1.putAll(map2); //map2有重复key会覆盖map1
	```
1. 根据value删除键值对
	```
	map1.remove(String.valueOf("小天才"));
	```
1. 根据key删除键值对
	```
	map1.remove("11");
	```
1. 查询value是否存在
	```
	boolean a = map1.containsValue("小天才");
	```
1. 转化成set列表
	```
	Set set1 = map1.entrySet(); //返回[11=小天才, 22=大聪明]
	```
1. 字典大小
	```
	int a = map1.size();
	```

#### 泛型
1. 说明
	泛型其实就是限定列表和字典的输入类型。有点相当于变成了数组，限定输入类型的好处就是避免错误类型数据录入，自己加筛选条件其实容易出现漏洞且增加工作。
1. 列表和字典泛型示例
	```
	ArrayList<Integer> list1 = new ArrayList<Integer>(); //类型不能是基本数据类型，只能是其包装类
	ArrayList<Integer> list2 = new ArrayList<>();        //jdk7及以上后面的可省

	List<Integer> lis3 = Arrays.asList(99,3);            //List指定类型

	Map<String,Integer> dir1 = new HashMap<>();          //字典指定类型
	```
1. 自定义泛型类：当我们不确定要传入的参数类型时，可以设置一个类型参数
	```
	class Human<E>{                   //2. 传入E类型（这个E可以是其他字母）
		String name;
		E age;                        //1. 不清楚这个age是什么类型，先设定成E类型

		public E work(E input1){      //该方法调用了E类型参数
			return input1;
		}
	}
	```
	在测试类中使用泛型类
	```
	Human zhangsan = new Human<>();         //不输入E类型默认Object类型
	zhangsan.work("不限制类型");             //Object类型，所以什么类型都可输入

	Human<Integer> lisi = new Human<>();    //只能输入Integer类型参数
	lisi.work(123);
	```
1. 接口、基础类都可以搞成泛型，这里不细说。


### 运算符
#### 算术运算符
1.  **不同类型字符运算规则**
	- 当（内存）容量小的数据类型和容量大的做运算或者赋值，结果会转化成容量大的。所以下面这个计算结果是String类型
	-  容量大小排名：byte→short = char→int→long→float→double→String
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_14.png)
	&emsp;&emsp;注意：不是说只能转化成参与计算的某种数据类型，只要是更大的数据类型都可以，比如char和int计算，就可以变成String，其实就是底层内存编码的加减或者赋值。特别地，char、short、byte参与的计算只能是int类型。
1.  **加减乘除**
	`+`、`-`、`*`、`/`(取整)、`%`(取余)

	- **语法糖**：a = a + 2 可以写成`a+=2`，此外还有`-=`、`*=`、`/=`
	- **自增、自减**
		a自增一次变成了3（相当于把上面语法糖的=和增量都省了）。自减是`--`
		```
		int a = 2;
		a++;  //与++a效果一样
		```
		注意：a++与++a在赋值给别人的时候效果不同，所以尽量不要在在自增自减的时候赋值
1. 内存溢出
	- 当我们计算的数据类型都是小的数据类型，而结果超过所能承载的数据类型，就会导致溢出
		```
		int a = 1000000000;
		int b = 20;
		long c = a*b;        // -1474836480：超过int的最大值了，就算c是long也不行，看参与计算的数据类型的最大容量
		long d = a*(long)b;  // 20000000000
		```
#### 逻辑运算符
1. `&&`(短路与)、`&` 、 `||`(或)、`!`：即布尔数据类型的运算符
&emsp;&emsp;注意：`&&`在前面的条件不满足就不会判断后面的了，比如`a>0 && b<10`，如果 a<=0，直接跳过后面的判断
#### 比较运算符
1. `==`、`.equals()`、`<=`、`>=`、`!=`
&emsp;&emsp;注意：`==` 和 `.equals()` 的区别在于前者比较是不是一个内存地址，后者比较值是不是一样，后者范围大些。具体请看字符串那里讲的。
#### 三元运算符
1. 基本结构：`(表达式)?结果1:结果2` 。如果符合表达式，输出结果1，否则结果2
	```
	int a = 12;
	int b = 20;
	int max = (a>b)?a:b;  //max=20
	```
1. 嵌套结构：少用嵌套，可读性差，拆成多个更好
	```
	int a = 20;
	int b = 20;
	int max = (a>b)?a:((a==b)?0:b);  //max=0
	//int max2 = a>b?a:a==b?0:b;     //括号不是必须的
	```
1. 多个比较
	```
	int a = 12;
	int b = 20;
	int c = 6;
	int max = (a>b)?a:b;
	int max2 = (max>c)?max:c;
	```  

#### Math函数
1. Math函数包含常见的数学函数：比如求和、求绝对值、求平均等
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_15.png)


### 流程控制
#### if
1. 代码：
	```
	String a = "123";
	String b = "123";
	if (a==b){
	   System.out.println("ok");
	}
	```
1. 递归：这里是求n的阶乘
	```
    public int all(int n){
       if (n==1){
           return 1;
       }else {
           return n*all(n-1);  // n不为1继续用n-1调用该函数
       }
    }
	```

#### switch
1. 示例
```
switch (selecter) {                      //selecter是条件
    case 1:				                 //selecter等于1时
		System.out.println("selecter=1");
		break;                           //跳出switch
    case 2:
		System.out.println("selecter=2");
		break;
	case 3:
		System.out.println("selecter=3");
		return;                          //结束整个程序
```

#### for循环
1. 两种方式
	```
	//for(初始值;条件;步长)
	for (int a = 1;a<10;a++){
		System.out.println(a);
	}

	//for(元素:元素列表)：这个和python中的一致
	for (String i:stringList){
		System.out.println(i);
	}	
	```

1. 跳出多重循环：也适用while循环 
	```
	loop1:for(int i=1;i<100;i++){  //给对应的循环加一个标签 `标签名:`
		for(int f=1;f<100;f++){
			if(i*f==20){
				break loop1;       //跳出带标签的循环
			}
		}
	}
	```
#### while循环
1. 代码：
	```
	int i = 1;
	while (i<10){
		System.out.println(i);
		i++;
	}
	```

### Scanner类(输入)
1. 类似python中的input
	```
	Scanner shuru = new Scanner(System.in); //先实例化一下Scanner类
	String a = shuru.next();                //a就是输入值，文本类型
	//int a = shuru.nextInt();              // 数值类型
	```

### java内存结构
&emsp;&emsp;下图绿色是栈，蓝色是堆。当我们创建变量，名称会像子弹一样压入栈中，然后根据栈中变量绑定的内存起始地址找到堆中的变量值。
&emsp;&emsp;如果变量值和堆中存在的相同，则栈中新压入的变量内存地址指向已经存在的堆值。如果某个栈变量改变了值，也会首先去找是否存在改变值的堆值，而不是去改变当前指向的堆值。
&emsp;&emsp;当一个`{}`内的程序执行完，栈中的变量会像子弹一样弹出，堆中的空间则不会马上回收，这也是为什么java占内存的一个原因。
![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_16.png)

### 类属性和方法
#### 创建类中的属性和方法
1. 代码：
	```
	class Human{
		//属性
		String name;	//属性就是变量
		int age;
		boolean sex = true;

		//方法1
		public String run(String shuDu){	//第一个String是输出类型，第二个String是输入类型
			return "我跑得" + shuDu;
		}

		//方法2
		public void eat(int wan){	//void表示不返回数据
			System.out.println("我能吃"+wan+"碗饭");
		}
	}
	```
#### 调用属性方法
1. java里面调用类的话不用管顺序，类在调用程序的下面都行
	```
	Human zhangSan = new Human();	//实例化，其实String、int这些也是类
	zhangSan.sex = false;		//改属性
	String zhangSanRun = zhangSan.run("快"); //调用有返回的方法
	System.out.println(zhangSanRun);
	zhangSan.eat(3);	//调用没有返回的方法
	```
1. 批量实例化
	```
	//要实例化的类
	class Student {
		int number;
		int state;
		int score;
	}

	//测试类
	public class AppTest {
		public static void main(String[] args) {
			Student[] students = new Student[10];      //创建学生类列表（10个学生元素）
			for (int i = 0; i < students.length; i++) {
				students[i] = new Student();           //实例化元素
				students[i].number = i + 1;            //实例属性赋值
				students[i].score = (int) (Math.random() * (100 + 1 - 50) + 50);
				students[i].state = (int) (Math.random() * (3 + 1 - 1) + 1);
			}

			for (int i = 0; i < students.length; i++) {
				System.out.println(students[i].number + "," + students[i].state + "," + students[i].score);
			}
		}
	}
	```

#### 方法的可变参数
1. 其实就是传入一个列表：该参数只能放最后，且要注意列表长度，所以一般都是用循环判断
	```
	public void eat(name, String...fool){
	System.out.println(name+"吃"+fool[0]+fool[1]);
	}
	```

#### 递归调用方法
1. 说明：递归就是不停的调用本函数，直到有确切的值后再依次计算值。
1. 计算斐波那契数列值：当我们输入3，函数会去调用`fibo(2)`和`fibo(1)`，这两次个都会返回1，所以`fibo(3)`就等于2
	```
	public static int fibo(int n) {
			if (n < 3) {
				return 1;   //确切值
			} else {
				return fibo(n-1) + fibo(n-2);
			}
		}
	```

#### 继承
1.  与python一样，继承后可直接使用父类方法属性
	```
	class Chinese extends Human{
	}
	```
1.  继承父类的好处之子类共用父类方法
	```
	//创建一个支付类和支付方法
	class Pay {
		public String pay() {
			return "原始pay";
		}
	}
	//两个子类改写支付方法
	class AliPay extends Pay {
		@Override
		public String pay() {
			return "支付宝pay";
		}
	}

	class WeixinPay extends Pay {
		@Override
		public String pay() {
			return "微信Pay";
		}
	}

	//1. 正常情况：创建一个测试类
	public class test{

		public static void main(String[] args) {
			//正常情况下，每次使用子类的方法都要实例化再调用方法
			Pay pay = new AliPay();
			pay.pay();

			pay = new WeixinPay();
			pay.pay();

		}
	}

	//2. 继承使用：创建一个测试类
	public class test{
		//这里搞一个商店，使用各种支付，我们只需在参数中设置父类，后面传入父类及其子类则都能运行
		public static void shop(Pay money){
			System.out.println(money.pay()+"支付成功！");
		}
		//只需要调用同一个方法
		public static void main(String[] args) {
			AliPay ali = new AliPay();
			shop(ali); //结果是“支付宝pay支付成功！”
			WeixinPay weiXin = new WeixinPay();
			shop(weiXin); //结果是“微信Pay支付成功！”

			//也可以整成匿名函数
			shop(new AliPay()); //结果是“支付宝pay支付成功！”
		}
	}
	```
#### 匿名对象
1. 即把前面那坨 `Human zhangSan = ` 省了，只要后面的：这里以 `Caidan` 这个类为例
	```
	//创建对象
	Caidan cai1 = new Caidan("鱼香肉丝", 1, 25.5);
	//添加对象
	caidanList.add(cai1);

	//用匿名对象方式创建并添加
	caidanList.add(new Caidan("麻婆豆腐", 2, 15));
	```
#### 继承的多态性：指实例化时实例化一个父类却new了一个子类
1.  说明：只能执行子类中继承或者改写父类中的方法。
	下图1是改写父类(Human)的方法，可以用；2是子类(Chinese)自己的，不能用。
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_17.png)
1.  多态性的优点：没看出来，感觉这种实例化只会限制子类，没有任何好处。

#### 类关键字this和super
1. **this**：表示当前类本身
	```
	class Person {
		private int age = 10;

		public int GetAge(int yourAge){
			this.age = yourAge; //this表示Person类
			return this.age;
		}
	}

	public class test {
		public static void main(String[] args) {
			Person Harry = new Person();
			Harry.GetAge(12); //返回12
		}
	}
	```
1. **super**：表示父类。有时候需要调用父类方法属性但不改写的时候就可以用
	```
	class Person {
		public String run(){
			return "人可以跑";
		}
	}

	class Chinese extends Person{
		public String CNrun(){
			String a = super.run(); //直接用super调用父类
			return "中国" + a;
		}
	}
	```

#### 权限修饰：public和private（缺省和protected不讲）
- Private只能在类内部使用、缺省可以在一个包中使用、protected只要继承了，就可以、public是一个工程就行。
- 类只能用缺省和public修饰、属性和方法四种都行，需要注意的是，一个源文件可以有多个类，但是声明为`public`的只能有一个，且只能是那个类名和源文件名相同的类。为什么要这样？主要是为了提高查询class的效率。
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_18.png)
#### 抽象类abstract
1. 说明：
	- abstract可以修饰类和方法，且修饰了方法必须修饰类。
	- 被修饰的父类和方法，不能被实例化和调用，只能被子类继承之后重写抽象类中的方法来使用。
	- 如果方法被abstract修饰，则子类必须重写该方法。
	```
	abstract class Human{
	    public void work(String whichWork){
            };
	}

	class Chinese extends Human{
	    public void work(String whichWork){
	        System.out.println("中国人工作");
	    }
	}
	```
1. 作用：
	能够规范多人开发的时候具有统一的类使用格式。
#### 接口
1. 说明：
	- 接口和抽象类很像，接口下的方法不能有body
	- 继承接口的类需要全部重写接口中的方法
	- 抽象类是规范他的子类的，那么接口就是规范不同子类的
	```
	//创建接口
   interface Human{
        public void work();
        public void eat();
    }

	//类调用接口
    class Chinese implements Human{
        public void work(){
            System.out.println("中国人干活");
        }
        public void eat(){
            System.out.println("中国人吃大米");
        }
    }

	//实例化类
    public class test2 {
        public static void main(String[] args) {
            Chinese zhangSan = new Chinese();
            zhangSan.eat();
            zhangSan.work();
        }
    }
	```
1. 接口可以继承另一个接口
	```
    interface Human{
        public void work();
    }

	//接口继承接口：下面这个接口继承了1个方法，自己还有一个方法
    interface Asian extends Human{
        public void math();
    }
	```
1. 接口具有多态性：接口和类都可以继承多个接口
	```
	//接口1
    interface Human{
        public void work();
    }

	//接口2
    interface Life{
        public void breath();
    }

	//接口继承两个接口
    interface Asian extends Human,Life{

    }
	```

	```
	//接口1
    interface Human{
        public void work();
    }

	//接口2
    interface Life{
        public void breath();
    }

	//类继承两个接口
    class Chinese implements Human,Life{
        public void work(){
            System.out.println("中国人干活");
        }
        public void breath(){
            System.out.println("中国人呼吸");
        }
    }
	```
1. 疑惑：
	为什么要单独搞一个接口，而不是让抽象类具有多态呢？因为java中类的继承有点复杂，多态继承会导致系统更加复杂，但是接口没有很多变量属性这些，就比较容易实现多继承。
1. 接口的意义：
	接口更像给类扩展共有的方法的，比如A类的子类B类和C类的子类D类都要实现一个类似的方法，但C类和D类又不能继承其他类了，这个时候我们只需要新建一个接口包含这个方法，C类和D类就可以继承了。
1. 接口多态意义示例：多个类继承一个接口
	```
	//创建接口
	interface Human{
		public void work();
	}

	//Chinese类调用接口
	class Chinese implements Human{
		public void work(){
			System.out.println("中国人干活");
		}
		public void work2(){
			System.out.println("中国人干好活");
		}
	}

	//English类调用接口
	class English implements Human{
		public void work(){
			System.out.println("英国人干活");
		}
	}
	```
	然后我们在测试类中分别通过接口和类实例化
	```
	Chinese wangwu = new Chinese();  //这是正常类实例化，可用类的所有方法
	wangwu.work();
	wangwu.work2();

	Human zhangsan = new Chinese();  //这里是接口指定类实例化，只能用接口中含有的方法
	zhangsan.work();
	```
	有什么好处呢？当我们有一天要换成English类的时候，如果正常实例化的方式，我要把非English类的方法替换，很麻烦。如果是下面这种方式我只需要把new Chinese()换成new English()，又因为English类引用了接口，所以方法都是一样的，不用修改。

#### 静态static属性和方法
1. **静态属性**：又叫类变量
&emsp;&emsp;静态属性只会保留一份，新属性值会覆盖旧值，相当于是一个全局变量的声明。
&emsp;&emsp;非静态的类属性又叫实例变量，和python属性一样。
	```
	class Human{
		static String name; //声明static静态属性
	}

	public class test{
		public static void main(String[] args) {
			Human.name = "zhangSan"; //没有实例化一个Human去赋值
			Human.name = "liSi";
			System.out.println(Human.name); //打印出来是"liSi"，"zhangSan"被覆盖了
		}
	}
	```
1. **静态方法**：
&emsp;&emsp;同样可以直接通过类进行使用。
	```
	class Human{
		public static void run(String shuDu){   //声明static静态方法
			System.out.println(shuDu+"跑！");
		}
	}

	public class test{
		public static void main(String[] args) {
			Human.run("静态的");
		}
	}
	```

1. 使用说明：
&emsp;&emsp;静态方法和属性都是随着类加载而加载的，而一个程序运行最开始就是加载类，所以声明了静态的属性和方法可以直接通过类调用。非静态方法和类需要在实例化之后才能加载，所以不能通过类直接调用。因此，静态方法和非静态方法是时空隔离的，所以静态方法不能使用`this`、`super`等实例化对象的方法才能用的关键字。

### 枚举类Enum
#### 最早的枚举类
1. 说明：
   对于常量，我们优先使用枚举。下面是新建一个枚举类。
2. 示例
	```
	class Human{
		//枚举的属性
		String name;
		int index;

		//构造方法：1.必须和类的名字相同 2.必须没有返回类型，也不能写void。其作用和python中的一致
		public Human(String input1,int input2){
			this.name = input1;
			this.index = input2;
		}

		//实例化作为枚举项：public表示公共属性，static随类加载，final定义常量
		public static final Human MAN = new Human("男人",1); 
		public static final Human WOMAN = new Human("女人",2); 

		//其他：搞个获取属性name的方法
		public String getName() {
			return name;
		}
	}
	```

1. 在测试类中
	```
	Human zhangSan = Human.MAN;              //这里是赋值不是实例化,又因为MAN是静态的，可以直接通过类调用
	System.out.println(zhangSan.getName());  //男人
	```
#### 改进后的枚举类
1. 说明：
   java5.0后简化了枚举类
1. 示例
	```
	enum Season{   //直接用enum代替class
		//实例化提前
		SPRING("春天","爱下雨"),
		SUMMER("夏天","热死人"); 

		//属性
		private final String seasonName;
		private final String seasonShow;

		//构造器
		private Season(String input1,String input2){
			this.seasonName = input1;
			this.seasonShow = input2;
		}  
	}
	```
1. enum自带几个方法。下面是在测试类中代码
	```
	Season a = Season.SPRING;
	System.out.println(a.toString()); //获取实例名SPRING

	//遍历实例名
	Season[] b =  Season.values();
	for (int i = 0; i < b.length; i++) {
		System.out.println(b[i]);    //SPRING SUMMER
	}
	```
1. 枚举类实现接口：实例化类的单独方法
	```
	interface Show {
		void show();
	}

	enum Season implements Show{
		SPRING("春天","爱下雨"){
			@Override       //给每个实例单独重写方法
			public void show() {
				System.out.println("春天也还好！");
				
			}
		},
		SUMMER("夏天","热死人"){
			@Override
			public void show() {
				System.out.println("夏天真的要化了！");
				
			}
		}; 

		private final String seasonName;
		private final String seasonShow;

		private Season(String input1,String input2){
			this.seasonName = input1;
			this.seasonShow = input2;
		}  
	}
	```

### 注解
1. **重写注解**
&emsp;&emsp;重写注解的作用是报错提醒。实际上我们重新方法是不需要注解的，但为了避免我们在重新的时候写错，变成新方法，加上`@Override`后，只要我们不是在重写，它就会报红。
&emsp;&emsp;此外，重写方法名和参数必须一样。改变参数的叫重载。
	```
	class Human{
		public void run(String shuDu){
			System.out.println(shuDu+"跑！");
		}
	}

	class Chinese extends Human {
		@Override
		public void run(String shuDu) {
			System.out.println("中国人" + shuDu + "跑！");
		}
	}
	```
1. **过时注释**
&emsp;&emsp;过时注解的作用是提醒使用该方法的地方尽快修改，该方法可能要废弃
		![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java基础_19.png)

### 算法
#### 九九乘法表
1. 三角结构通常都是两重循环加 `j<=i` 
	```
	for(int i=1;i<=9;i++){
		for(int j=1;j<=i;j++){
			System.out.print(j+"×"+i+"="+i*j+" ");
			if(j==i){
				System.out.println();
			}
		}
	}
	```

#### 打印杨辉三角
1. 示例：
	```
	int[][] erwei = new int[10][];  
	for ( int i = 0; i < erwei.length; i++) {
		erwei[i] = new int[i + 1];               //给二维数组每行初始化长度
		for (int j = 0; j <= i; j++) {           //给元素赋值
			if (j!=0 && j!=i) {
				erwei[i][j] = erwei[i-1][j-1] + erwei[i-1][j];
			} else {
				erwei[i][j] = 1;
			}
		}
	}

	for(int i=0;i<erwei.length;i++){             //遍历二维数组
		for(int j=0;j<erwei[i].length;j++){
			System.out.print(erwei[i][j]+" ");
		}
		System.out.println(); 
	}
	```

#### 二分查找
1. 思路
   - 二分查找就是把中值和目标比较，大了就往前找，小了就往后
   - 肯定是一个循环，要一直那中值和目标比较，由于次数不定，所以肯定要用 `while` 循环，循环条件就是当比较值不匹配的时候
   - 循环内部肯定要分两种情况，一种是大了，一种是小了，所以肯定就要 `if` 
   - 当我们的值小了，那我们就要增加循环的i值，反之就减少。
   - 这个i值可以用列表最大长度或者0来计算吗？显然不能，比如我们之前发现这个值最大index只能在5，那就把5标记成最大值，之后的计算就把5拿来计算

2. 示例：
	```
	int[] arr1 = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17 };
	int target = 6;
	int i = arr1.length / 2 - 1;
	int max = arr1.length - 1;
	int min = 0;
	while (arr1[i] != target) {
		if (arr1[i] < target) {
			min = i;               //当前值小于目标，说明当前值是后续计算范围的最小值
			i = (max + i) / 2;
		} else {
			max = i;
			i = (i + min) / 2;
		}
	}
	System.out.println("index是：" + i);
	```

#### 冒泡排序
1. 思路：
   - 冒泡排序就是两两比较，把最大的依次移动到最后
   - 这样的比较次数是固定的，肯定要用 `for` 循环，又因为我们还要遍历多次，肯定就需要两重循环
   - 第一次要遍历全长，之后依次递减，这种两个循环相关的，肯定要用到 `j<=i` 结构
   - 最后的主体就是判断加交换

1. 示例：
	```
	int[] arr1 = { 9,6,3,0,1,10,4,5,2,8,7};
	for (int j = arr1.length; j > 1 ; j--) {
		for (int i = 0; i < j-1; i++) {
			if (arr1[i]>arr1[i+1]) {
				int inter1;
				inter1 = arr1[i];
				arr1[i] = arr1[i+1];
				arr1[i+1]=inter1;
			}
		}
	}
	```

#### 两个字符串长度最大的共同字串
1. 思路
	- 从较小的字符串中挑选字串快一些
	- 外轮循环选字串起始位置，内层循环选结束位置
	- 只要新的字串长度大于旧的就替换
  
2. 示例
	```
	String str1 = "qwertyuhelloiopmnbvcxzvasdfg";
	String str2  = "mnbtyuivchellozxlkjh";
	String maxson = "";
	for (int j = 0; j < str2.length(); j++) {
		boolean ifcontain = str1.contains(str2.substring(j, j+1));
		if (ifcontain) {
			for (int i = j; i < str2.length(); i++) {
				String str2son = str2.substring(j, i+1 );
				boolean ifcontainson = str1.contains(str2son);
				if (ifcontainson&&str2son.length()>maxson.length()) {
					maxson = str2son;
					System.out.println(str2son);
				}
			}
		}
	}
	```