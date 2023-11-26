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
### java文档
1. 说明
	当我们在做大项目，写的类和方法加了很多注释（`/**`），要生成类似swagger的文档
1. 通过javadoc命令生成文档
	首选跳转到需要类文件目录
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java中级_1.png)
	
	进入命令行
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java中级_2.png)

	对需要生成文档的类文件使用javadoc命令：前面两个UTF-8是因为注释有中文，test2.java是类文件
	```
	javadoc -encoding UTF-8 -charset UTF-8 test2.java
	```
	在目录下生成了一个index.html文件，进入就是javadoc文档
	![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/java中级_3.png)

### java多线程
#### 基础概念
1. 多进程与cpu：
	cpu有几核就能开多少真实的进程，超过的就变成了模拟进程，即一个核可能开几个进程，但其实是通过在多个进程之间切换实现的。
1. 多线程与cpu
	进程中的多个线程谁先去cpu执行是系统控制的，人干预不了。
#### 继承Thread类（不推荐使用）：继承类实现子线程
1. 说明：
	继承了Thread类并改写run方法就相当于创建了一个子线程方法
1. 示例：
	```
	public class test1 extends Thread {
		@Override
		public void run(){
			//run方法体
			for (int i = 0; i < 5; i++){
				System.out.println("run执行"+i);
			}
		}
	}
	```
1. 通过start方法调用子线程方法，通过子线程运行：运行结果就是主线程的和子线程的结果交替出现，即两个线程都在执行，至于那个具体执行那个是系统调度
	```
	public class test1 extends Thread {
		@Override
		public void run(){
			//run方法体
			for (int i = 0; i < 5; i++){
				System.out.println("run执行"+i);
			}
		}
		public static void main(String[] args){
			test1 testThead = new test1();  // 实例化
			testThead.start();              // 调用子线程方法run

			//主线程的方法体
			for (int i = 0; i < 200; i++){
				System.out.println("main执行"+i);
			}
		}
	}
	```

	如果不用start方法，而是直接换成run，即`testThead.run();`，就相当于没有启动子线程，而是直接调用run方法，那就按顺序先执行run再执行主线程的方法体。start就相当于告诉系统，start的方法要在子线程中执行。如果有几个start启动的子线程，这些子线程的运行顺序是同样是不固定的。
#### 调用Runable接口：调用接口实现子线程
1. 说明
	上面的类实现子线程，存在java单继承的问题，所以通过接口实现子线程就可以拥有接口可以多调用的好处。本质上Thread类也是在Runable接口上实现的。所以Runable接口实现多线程更灵活。
1. 示例
	调用Runnable接口同样需要改写run方法
	```
	public class test2 implements Runnable{
		@Override
		public void run(){
			//run方法体
			for (int i = 0; i < 5; i++){
				System.out.println("run执行"+i);
			}
		}
	```
1. 通过接口start子线程：但还是需要Thread类的start方法
	```
	public class test2 implements Runnable{
		@Override
		public void run(){
			for (int i = 0; i < 5; i++){
				System.out.println("run执行"+i);
			}
		}

		public static void main(String[] args){
			test2 testThead = new test2();       // 先实例化接口类
			Thread t1 = new Thread(testThead);   // 再实例化Thread类并将接口类作为参数
			t1.start();                          // 通过Thread类start
			// 上面两行可以简写成new Thread(testThead).start()

			//主线程
			for (int i = 0; i < 200; i++){
				System.out.println("main执行"+i);
			}
		}
	}
	```
#### 线程常用方法
1. 起名字
1. 获得当前线程名称