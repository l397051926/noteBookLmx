#mysql 基础

##为什么学习数据库
将重要的数据进行保存形式有多种，其中常用的是以内存或者硬盘的形式，而数据存储后的管理则使用数据库技术来实现

##数据库的相关概念
###DB
    数据库（database）： 存储数据的仓库，它保存了一系列有组织的数据
###DBMS
    数据库管理系统（database management system）。数据库是通过DBMS创建和操作的容器
### SQL
    结构化查询语言（structure query language），专门用来与数据库通信的语言

##SQL的优点
1. 不是某个特定数据库的语言，而是面向所有DBMS的语言
2. 简单易学
3. 虽然使用简单，但实际上是一种强有力的语言，灵活使用，可以实现很多高级和复杂的数据库操作

##SQL 语言的分类
1. DML 数据操作语句，用于添加、删除、修改、查询数据库记录，并检查数据的完整性
2. DDL 数据定义语句，用于数据库和表的创建，修改，删除
3. DCL 数据控制语句，用于定义用户的访问权限和安全级别

###DML
    DML 用于查询与修改数据记录，包括如下SQL语句：  
    INSERT 添加数据到数据库中
    UPDATE 修改数据库中的数据
    DELETE 删除数据库中的数据
    SELECT 选择（查询）数据

###DDL
    DDL 用于定义数据库的结构，比如创建，修改，删除数据库的对象，包括的sql 如下：
    CREATE TABLE 创建数据库表
    ALTER TABLE  修改数据库
    DROP TABLE   删除数据库
    CREATE INDEX 在表上建立索引
    DROP  INDEX  删除索引
    
###DCL
    DCL 用于控制数据库的访问，包括sql如下
    GRANT 授权访问权限
    REVOKE 撤销访问权限
    COMMIT 提交事务处理
    ROLLBACK 事务处理回退
    SAVEPOINT 设置保存点
    LOCK 对数据库的特定部分进行锁定

#Mysql 的数据库安装
    详细内容 -后期补充

## 安装后命令
    1. net start mysql 启动
    2. net stop mysql 停止
    3. mysql -u -p -h -P 登录 u 用户名， p 密码， h ip ， P 端口
    4. exit 退出

## 安装后重要配置文件
    my.ini 文件 其中可以修改 
    1. 服务的端口
    2. 数据存储磁盘位置
    3. 允许最大连接数
    4. 服务端使用的字符集默认为8比特编码的latin1字符集
    5. 创建新表时将使用的默认存储引擎

## mysql 的语法规范
    1. 不区分大小写
    2. 每句话都需要; 或者\g 结尾
    3. 各个子句 一般分行编写
    4. 关键字不能缩写 也不能分行
    5. 用缩进提高语言的可读性

## mysql 常用语句
    1. show databases 展示所有数据库
    2. show tables 展示所有表
    3. use database  数据库名  进入这个数据库
    4. create table student(id int, name varchar(200)); 创建一个表
    5. drop 表名 删除数据表
    6. desc 表名 查看表结构
    7. select * from 表名 查询所有记录
    8. insert into 表名 (列名) values (列值) 插入一条数据 
    9. update 表名 set 列1=新值   更新表中数据
    10. delete from 表名  删除表 数据
    11. 可以使用 where 进行过滤
    12. 在select 时可以指定要查询的列
    13. 运算符 可以使用 = > < between and 
    14. % 可以匹配多个字符
    15. _ 只匹配一个字符
    16 使用like 进行模糊查询
    17 is not null  不为空的数据
    18 order by 按顺序排列  ，如果使用desc 则是倒叙
