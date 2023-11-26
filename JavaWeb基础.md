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
### JaveWeb常识
1. JaveWeb主要就是web应用的后端
### 数据库
#### 数据库设计
1. 数据库一对一表的情况有用户表和用户详情这种，分表的意义在于性能高些。
1. 一对多表设计，比如部门和员工表，员工表需要一个外键关联部门表的主键。
1. 多对多表，比如商品和订单表，需要一个中间表，中间表的两个外键分别是商品表和订单表的主键。
#### 数据库的实现
1. 具体看mysql相关博文，略。
### java连接数据库（JDBC）
1.说明
    和python的连接数据库基本一样，首先用个需要一个mysql的驱动jar包作为操作的基本点，然后就是连接数据库，执行sql那些。
#### 驱动jar包
1. 下载对应系统平台的mysql驱动jar包，略。
1. 把mysql驱动jar包放到项目的lib文件夹下
![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_1.png)
#### 连接使用数据库
1. 示例：
    ```
    import java.sql.DriverManager;
    import java.sql.Connection;   //这几个开头是com.mysql.jdbc要报错：Type mismatch
    import java.sql.Statement;

    public class JDBCDemo{
        public static void main(String[] args)throws Exception {
            //获取连接
            String url="jdbc:mysql://localhost:3306/test1?useSSL=false";   //test1是数据库的名称
            String user="root";
            String password="123456";
            Connection connet1 =  DriverManager.getConnection(url, user, password);

            //要执行的sql语句
            String sql1 = "update goods set price = 100 where id = 1";

            //创建要执行sql的对象
            Statement state1 = connet1.createStatement();

            //sql对象执行sql语句：执行修改语句用executeUpdate，返回受影响的行数
            int count1 = state1.executeUpdate(sql1);
            System.out.println(count1);

            //关闭连接
            state1.close();
            connet1.close();
        }
    }
    ```
1. 执行查询语句
	```
    //执行查询语句
    ResultSet rs1 = state1.executeQuery(sql1);

    while(rs1.next()){                   //next()方法返回布尔，也即是没有下一行了返回false
        int name1 = rs1.getInt("id");    //获取当前行字段名叫id的int类型值;获取字符串字段是getString，其余类似
        double price1 = rs1.getDouble("price");
        }

    //这次还要关闭查询的连接
    state1.close();
    connet1.close();
    rs1.close();
	```

    将查询到的数据存入列表：需要提前创建一个Goods类，这里没写
    ```
    //查询sql
    String sql1 = "select * from tb_goods";
    Statement state1 = connet1.createStatement();
    ResultSet rs1 = state1.executeQuery(sql1);

    //创建列表
    List<Goods> goodsList= new ArrayList<>();

    while(rs1.next()){                   
        int id1 = rs1.getInt("id"); 
        double price1 = rs1.getDouble("price");
        String titile1 = rs1.getString("titile");

        //实例化goods对象并赋值并加入列表
        Goods shangping = new Goods(id1, price1, titile1);  //如果Goods类有set和get方法，这里可以用set方法写入属性
        goodsList.add(shangping);                           //这样，每行数据都作为Goods对象存入列表
    }
    ```
1. 防止sql注入的执行sql方式
    ```
    //我们常用的sql拼接，如果name中含有单引号和sql语句，会导致sql注入
    String name = "手表";
    String sql1 = "select * from tb_goods where titile = '"+name+"'";

    //新的方式
    String sql1 = "select * from tb_goods where titile = ?";     // ?号代表参数
    PreparedStatement state1 = connet1.prepareStatement(sql1);   //获取PreparedStatement对象
    state1.setString(1,"手表");                                  //设置?号参数，注意数据类型和参数序号
    ResultSet rs1 = state1.executeQuery();                       //执行sql，不需要传入sql了
    ```
    此外，PreparedStatement还有预编译的功能，加快sql执行速度，需要开启
    ```
    String url="jdbc:mysql://localhost:3306/test1?useSSL=false&useServerPrepStmts=true"    //把useServerPrepStmts=true添加到url参数里面即可
    ```


2. 事务：当try中间有代码错误，事务回滚，不会造成数据库部分值被修改（事务是数据库本身有的能力）
    ```
    try {
        //开启事务
        connet1.setAutoCommit(false);

        //要执行的sql
        int count1 = state1.executeUpdate(sql1);
        System.out.println(count1);

        //提交事务
        connet1.commit();
    } catch (Exception e) {
        //回滚事务
        connet1.rollback();
    }

    //关闭连接
    state1.close();
    connet1.close();
    ```

### 数据库连接池
1.说明
    每个资源都来连接关闭一次数据库连接效率低，用连接池和ip池一样，能提升效率，这里用阿里的德鲁伊druid连接池接口。
#### 将德鲁伊的jar包放入项目
1. jar包自己下载
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_2.png)
#### 配置数据库连接池
1. 新建一个properties配置文件
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_3.png)
1. properties配置代码：
    ```
    # 这个固定
    driverClassName=com.mysql.jdbc.Driver
    # 数据库地址密码
    url=jdbc:mysql://localhost:3306/test1?useSSL=false&useServerPrepStmts=true
    username=root
    password=123456
    # 初始化连接数量
    initialSize=5
    # 最大连接数（初始不够后允许的最大连接数）
    maxActive=10
    # 最大等待时间(ms)
    maxWait=3000
    ```
1. 通过德鲁伊连接数据库代码：
    ```
    //加载配置文件
    Properties prop1 = new Properties();
    prop1.load(new FileInputStream("src/druid.properties")); // 需要注意的是，这个路径可能需要通过System.out.println(System.getProperty("user.dir"))判断，其打印出来的路径，到properties文件为止，缺的部分才需要填入。

    //获取连接池对象
    DataSource data1 = DruidDataSourceFactory.createDataSource(prop1);

    //获取数据库连接
    Connection connet1 = data1.getConnection();

    System.out.println(connet1);
    ```

### mybatis
1. 说明
   mybatis是用来替代jdbc的，是数据持久化的框架，因为jdbc操作容易硬编码且不好维护。
#### 配置mybatis
1. 添加mybatis依赖
   在pom文件中添加mybatis依赖，此外由于需要mysql驱动，所以还要添加mysql依赖（有了这个就不需要自己去下载mysql的驱动jar包了）
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_4.png)

1. mybatis配置文件
   - 我们一般把配置文件放在resources文件夹下，格式为xml
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_5.png)
   - 这个配置文件用来配置一些数据库信息，此外还有一个mappers sql映射文件地址，这个下面说
        ```
        <?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
        <configuration>
        <environments default="development"> 
            <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">

                <!--数据库的信息-->
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
            </environment>
        </environments>
        <mappers>
            
            <!--mappers_sql映射文件位置-->
            <mapper resource="tb_userMappper.xml"/>
        </mappers>
        </configuration>
        ```

1. 数据库说明
   我们这里新建了一个叫tb_user的表，表里面有id、username等字段。一般我们一个表建一个java类来处理数据，类里面有基本的get、set方法。需要注意的是这些属性名称一定要和数据库中的字段名称一样，不然查不到。
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_6.png)

1. sql映射文件（mappers）
   - 这个文件就是用来存sql语句的，我们要执行的sql语句都放进去
   - 文件位置一般和配置文件放一起，名称一般根据要操作的数据库名称定，也是xml文件
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_7.png)
    - 里面的内容如下：namespace是命名空间，不重名就行。如果数据库表名报错，是因为没vscode不认识该数据库，通过数据库插件连接数据库即可
        ```
        <?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
        <mapper namespace="test1">

            <!--前面的这个select叫标签，select是查询语言的标签，还有编辑的update等；这个id是标签下的sql语句的唯一标识；resultType是sql执行语句的出参类型，这里就是我们建的java类-->
        <select id="selectAll1" resultType="com.example.User">
            select * from tb_user;
        </select>

        </mapper>
        ```
1. 在测试类中使用mybatis进行数据库操作
    ```
    //mybatis配置文件地址
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

    SqlSession session1 = sqlSessionFactory.openSession();
    //调用sql映射文件中的sql语句
    List<User> users =  session1.selectList("test1.selectAll");
    //因为该sql语句在映射文件配置的出参是一个User类，所以这里查询出的就是一个User类列表，这里我们用类的get方法循环取出查询出的User对象的name字段（属性）
    for(Object i:users){ 
        String a = ((User) i).getUsername();               
        System.out.println(a);
    }
    //关闭mybatis
    session1.close();
    ```
1. 路径问题
   上面几个配置文件都涉及到行对路径问题，我有点糊，自己先试试看吧。

#### mybatis优化
1. 说明
   - 在上面的mybatis使用中 `session1.selectList("test1.selectAll");` ，还是用了硬编码，这种硬编码不好维护，所以我们要把它做出方法，方便维护。
   - 上面的mybatis运行流程是，mybatis-config配置了数据库连接信息和sql语句（语句指定java类出参）的配置文件，测试类根据sql语句配置文件中的sql语句id运行sql语句。
   - 优化的mybatis运行流程是就是加了个接口来获取映射文件的中sql语句。
1. 新建接口方法来使用sql映射文件的中的sel语句
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_8.png)

1.修改sql映射文件：命名空间名称要是接口的包装名
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_9.png)

1. 使用接口中的方法调用sql语句
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_10.png)

1. 使用mybatisx进行切换
   开发的时候我们经常需要在映射文件和接口文件之间进行切换，使用mybatisx插件后（安装后需要重启vscode），两个文件可以通过点击小鸟图标进行切换
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_11.png)

#### mybatis传参查询
1. 在映射文件的sql语句中设置参数
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_12.png)

1. 接口方法设置入参
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_13.png)

1. 在测试类调用接口方式时传参
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_14.png)
   顺便说一下，这里直接打印Brand类的本来会直接显示内存地址，但是这个类中我有toString方法，所以打印的是toString的返回值。

### Tomcat
#### 安装使用tomcat
1. 下载tomcat：不同版本对于的java版本不一样，一般8的比较多，下载好解压了就行了
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_15.png)
1. 修改配置中的编码格式：修改conf文件夹下的logging.properties文件编码格式为GBK（如果是在vscode中使用，还是要UTF-8）
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_16.png)
1. 运行tomcat
   点击bin文件夹下的startup.bat文件，然后去浏览器输入`http://localhost:8080/` 访问tomcat自带的web项目
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_17.png)
1. 关闭tomcat
   在运行tomcat的命令行窗口按 `Ctrl` + `C`

#### vscode创建web项目
1. 通过模板创建web项目：略
1. 添加java和resource文件夹：java文件夹用来存放java文件, resources用来存放资源文件(maven编译时会识别文件夹名所以必须要叫resources）
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_18.png)
1. 修改配置文件：只用保留这部分，其他删除即可，其中packaging是打包方式，一般web项目是war，普通java项目是jar（这个是默认方式）
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_19.png)

#### tomcat Maven插件
1. 在pom文件中添加tomcat和maven插件
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_20.png)
1. 下载Community Server Connector插件并配置tomcat
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_21.png)
    这个是在最左下角的位置的，先点Create New Server...
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_22.png)
    选择本地的Tomcat
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_23.png)
    选定后会出现一个页面让你编辑一些东西，你不要管，直接Finish就行
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_24.png)
    然后左下角就可以看到这个了
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_25.png)
    起服务
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_26.png)

    打包项目（记得保存了再打包）
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_27.png)

    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_28.png)

    打包成功会在target文件下下显示war文件
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_29.png)

    重新打包前最好清理下target文件夹：点击小三角，有时候不清理貌似会导致重新打包失败，另外vscode里面的文件记得ctrl+s保存啊！
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_30.png)

    此外，如果vscode终端中文是乱码，可以在终端输入 `chcp 65001` 将终端的编码改成UTF-8，vscode右下角的编码和终端乱码无关。

    如果打包遇到版本问题，可参看这个博文：[默认版本冲突](https://blog.csdn.net/qq_36521848/article/details/125893987)
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_31.png)

    访问
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_32.png)

    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_33.png)

    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_34.png)

    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_35.png)

### Servlet类
1. 说明
   我们知道tomcat里面有个servlet的容器，该容器可以创建Servlet类，当我们启动服务的时候，这个类下的init方法被启动，然后每次访问，其service方法都会调用，最后就是关闭服务器会调用destroy方法
#### 导入Servlet坐标
1. 添加依赖：要UTF-8编码
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_36.png)
#### 实现Servlet接口
1. 创建一个类实现Servlet接口
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_37.png)
#### 注解路径
1. 添加注解：路径名称填写，会有5个方法（包括说明中的init、service、destroy等），主要是service方法
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_38.png)
1. 路径正则匹配
   如果一个路径是
   ```
   @WebServlet("/servletDemo1/abc")
   ```
   一个是
   ```
   @WebServlet("/servletDemo1/*")       //*表示任意字符
   ```
   访问 'http://localhost:8080/demo-1.0/servletDemo1/abc' 会优先访问第一个地址

#### 访问路径
1. 重新打包项目后输入路径访问刚才的路径（这里是在service方法里面打印一段话）
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_39.png)

   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_40.png)

#### get和post请求访问不同资源
1. post和get请求方法
    上面我们知道，直接通过注解的路径可以访问service方法下的函数，但我们如果要控制请求方法不同访问的资源不同，这里先注释掉service方法，改用重写的doGet和doPost方法。
    ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_41.png)

1. service下用post和get
   上面只是简单尝试用get和post访问资源，实际上，我们还是需要service，所以service用来查看访问的方式，然后再来调用doGet和doPost方法
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_42.png)

#### Servlet父类
1. 父类写法
   如果每个java文件都搞上面那一套，势必每个资源文件都需要重写一遍，可以搞一个父类，把基本的都写了，子类复写doGet和doPost方法就行。父类不用注释路径，子类需要。
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_43.png)

1. 子类写法
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/JavaWeb基础_44.png)

### request和response
#### request请求常用方法
1. 常用方法