1.什么是impala
    1.基于hive 使用内存计算 兼顾数据仓库，具有实施 批处理 多并发等优点
    2. 优点
        基于内存运算
        无需转换为mapreduce
        尽可能将数据和计算分配在同一机器， 减少了网络开销
        支持各种文件格式 textfile sequencefile parten rpcfile
        可以方位hive的 metastore 对hive 进行数据分析
    3.缺点
        堆内存依赖大， 完全依赖于hive
        分区超过1万 性能下降
        只能读取文本文件 不能读取自定义二进制文件
        每当新记录 添加到hdfs中的数据目录时， 该表需要呗刷新
2. impala 安装
    -
3. impala 基础使用
    操作方法和hive 方法一样，就是比hive 有要快
    impala-shell -p 直接执行sql语句
    impala-shell -f 指定文件 执行sql语句

4. ddl 数据定义
    impala 不支持with dbproperties("test"="123)
    其他和操作hive 是类似的

5. 数据导出功能弱
    不支持 export 和import 这种命令

6. 查询
    基本语法和hive 大体一样， 不支持关于mapreduce 相关的函数 不支持分桶表

7. 创建函数
    可以传自己的udf 包

8.优化
    尽量将statestore 和catalog 放在一个节点
    使用partin 文件格式进行存储
    避免小文件
    