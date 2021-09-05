hive
    数据库
        创建
        1.create database test
        2.create database if not exists tses;
        3.create database test location '/ttt' //location 指定建数据库的位置
        查询
        show databases;
        show databases 'defau*'
        详情
        desc database test;
        desc database exended test;
        修改数据库
        alter database test set dbproperties('create_time'='2019')
        删除
        drop database test2
    表
        创建表
            1.create table if not exists student2(
                    id int ,name string
                )
                rot format delimited fields terminated by '\t'
                stored as texfile
                location '/user/hive/warehouse/student2'
            2.create table if not exists student3  as select id name from student
            3. create table if not exists student4 like student
        查询表信息
            desc formatted student
    2. 外部表
        不是由hive 生成的文件 ，属于外部传进来的表 后交给了hive 管理 ，就是外部表，就算在hive 删除了也无法对外部源文件
    3. 内部表 转外部表
        alert table student5 set tblproperties('EXTERNAL'='TRUE');
    4 分区
        在hive 多了一个字段，在hdfs上增加了一个目录，意义是在 hive 是没有索引的，分区变相的增加了索引
    5.二级分区
        在插入的时候 必须要 包含两个分区
    6. 查询时 如果指定分区可以提高很高的速度
    7. 分区表注意事项
        1. 有分区的时候 需要分区恢复一下，才可以使用
        msck repair table  xxx
        可以直接添加分区 alert  add partition (xxx)
    查询
        select * from test;
        select id as ha from test;
    join
        inner join  内连接 不满足on 条件都会删掉
        left join 左连接 以左未基准
        right join 右连接 以右边未肌醇
        full join 满外连接 全部出先
    order by
        排序不能随便使用，因为把所有数据拉进去
    sort by
        内部排序 不会全部有序 是每个reduce 保持有序
    distribute by 分区排序
        有几个reduce 分几个区
        distribute by 要卸载 sort by 之前
    分桶
        对某一个表或者 分区 表 进行进一步分区
        create table stu_buck(id int, name string)
        clustered by(id)
        into 4 buckets
        row format delimited fields terminated by '\t'
        需要先 设置强制分桶
        set hive.enforce.bucketing=true;
        set mapreduce.job.reduce=-1;
        使用分桶来抽样数据
        select * from stu_buck tablesample(bucket 1 out of 4 on id);
    常用函数
        nvl()有就显示 没有就不显示空子段赋值
        case when then else
        concat 拼接
        collect_set 行转列
        concat_ws(",",list)
    行转列
        collect_set 多列转成集合
    列转行
        explode(**) 如果要拼1 v 多的话 可以使用lateral view 用于拼接 1个属性对应多行
        select
         a,b
         from table
         lateral view
            explode(b) tb1
    窗口函数
        select
            distinct(name),
            count(*) over() 开窗 rows between 1 preceding and 1 following
        lag() 网上找一行数据
        lead() 往后多少行
        ntle() 把所有数据分块  窗口函数只能最后执行，因此只能使用 子查询
        rank() 分数都一样排序
        dsnse_rank
        row_rank
    函数 udf udtf 函数编写
        expend udf
        udf  一进一出
        udaf 多近一出
        udtf 一进多出
        打包
        上传到服务器
         hive/lib 下面
         进入hive 里
        add jar ...
        create temporary function mylower as "com.atguigu.hive.Lower"
    压缩
        开启hive 中间   传输数据压缩
        开启map 输出压缩
        开启 reduce 输出压缩
        指定压缩编码
    文件存储
        分为行市存储
        和列式存储
        textFile / sequencefile 行
        orc /parquet 列
    hive 调优
        fetch 抓取，某些查询不走map reduce ，可以直接读文件 走的fetich
        本地模式 如果小文件可以在本地跑
        大表join 小表
        大表join 大表
    其他优化
        列存储 尽量不要用select *
        动态分区

    