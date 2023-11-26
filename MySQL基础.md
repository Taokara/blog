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
#### MySQL数据库的创建和连接
1. 说明：
   - 首先我们需要在系统（windows或linux）中安装MySQL，参看[这篇博文](https://blog.csdn.net/An0217313/article/details/119245960)。
   - 然后我们通过navicat（完全可以用vscode插件代替）连接该数据库，这个也可以查，略。
### DDL和DML
#### 数据定义语言（DDL）
1. 创建数据库
   ```
   CREATE DATABASE test_database DEFAULT CHARACTER SET = 'utf8mb4';
   ```
1. 创建/删除表
   ```
   CREATE TABLE table1(name CHAR(10), age INT);

   DROP TABLE table1;
   ```
#### 数据操纵语言（DML）
1. 插入数据
   ```
   -- 插入一行完整数据
   insert into Student values('01' , '赵雷' , '1990-01-01' , '男');

   -- 插入一行部分数据
   INSERT INTO usertable(username, password, email)
   VALUES ('admin', '123456', 'xxxx@163.com');

   -- 插入查询到的数据
   INSERT INTO user(username)
   SELECT name FROM account;
   ```
1. 更新数据
   ```
   UPDATE usertable SET password='123456' WHERE username = 'root';
   ```
1. 删除数据
   ```
   DELETE FROM usertable WHERE username = 'robot';
   ```
### 数据查询语言（DQL）
#### 显示 SELECT
1. 说明
    Select语句作为显示语句，也能使用条件语句，很大一部分where能使用的而语句selec都可以使用，此外select也可以使用聚合函数。
#### 显示结果限制 DISTINCT & LIMIT
1. 结果去重 DISTINCT
    ```
    SELECT DISTINCT user_id FROM usertable;
    ```
1. 查询限制条数（返回第 3 ~ 5 行）
    ```
    SELECT * FROM mytable LIMIT 2, 5;
    ```
#### 子查询 WHERE
1. where：可用逻辑符、between、like、in、exists、and、or、not、is null、any、all，且可在插入、删除等语句中使用。In和exists都是接子函数，区别在于in后面的子函数和主函数没有联系，而exists后的子函数则与主函数字段连接起来，亦或直接判断子函数是否成立

    ```
    SELECT * FROM Customers WHERE vend_id NOT IN ('DLL01', 'BRS01');
    ```
2. 子查询嵌套
    ```
    SELECT username FROM usertable
    WHERE user_id IN (SELECT cust_id FROM orders WHERE cust_id != 12);
    ```
#### 连接组合 JOIN & UNION
1. 自连接：形成笛卡尔积，P1第一列匹配P2所有name，然后是P1第二列匹配P2所有name，以此类推
    ```
    SELECT P1.name AS name_1, P2.name AS name_2 
    FROM Products P1, Products P2;
    ```
2. （内）链接：组成笛卡尔积后保留满足条件的
    ```
    select * from tableA join tableB WHERE TableA.name = TableB.name;
    ```
3. 左(外)连接：同样是组成笛卡尔积后保留满足条件的，但是主表（左边）不满足条件的也要保留
    ```
    select * from tableA left join tableB WHERE TableA.name = TableB.name;
    ```
4. 联合查询：就是把从表的结果接在主表下面，并去重
    ```
    SELECT  name  FROM  student
    UNION
    SELECT  name  FROM  teacher;
    ```
#### 函数 COUNT & AVG & SUM & MAX & MIN
1. 常见函数：COUNT()、AVG()、SUM()、MAX()、MIN()
    ```
    SELECT AVG(score) AS avg_score FROM score;
    ```
#### 排序和分组 Group by & HAVING
1. 分组后排序。Group by函数可以按字段分组，每个组内不同的行形成一张张虚表，处理一般是用having中的聚合函数。
    ```
    SELECT cust_name FROM Customers 
    GROUP BY cust_name
    ORDER BY cust_name DESC;
    ```
2. HAVING子句：HAVING 要求存在一个 GROUP BY 子句
    ```
    SELECT cust_name, COUNT(*) AS num FROM Customers
    WHERE cust_email IS NOT NULL
    GROUP BY cust_name
    HAVING COUNT(*) >= 1;
    ```
### 其他
#### 索引 INDEX
1. 创建索引
    ```
    CREATE UNIQUE INDEX user_index ON user (id);
    ``` 
#### 事务
1. 开启事务后，在commit之前，都可以取消操作，没问题再提交
    ```
    -- 开始事务
    START TRANSACTION;
    -- 插入操作 A
    INSERT INTO `user`
    VALUES (1, 'root1', 'root1', 'xxxx@163.com');
    -- 创建保留点 updateA
    SAVEPOINT updateA;
    -- 插入操作 B
    INSERT INTO `user`
    VALUES (2, 'root2', 'root2', 'xxxx@163.com');
    -- 回滚到保留点 updateA
    ROLLBACK TO updateA;
    -- 提交事务，只有操作 A 生效
    COMMIT;
    ``` 
#### 存储过程
1. 示例
    ```
    create procedure pro1()
    begin
    declare i int;
    set i=1;
    while i<=10 do
    insert into table1(name,age) values(i,i);
    set i=i+1;
    end while;
    end;

    call pro1();
    ```