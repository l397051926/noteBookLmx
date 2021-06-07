1. equals和==的区别   
    equals 是判定两个值是否相等， == 不但会判定值，还会判定地址是否相等  
    
2. 8种基本数据类型，long类型占几个字节，char类型占几个字节  
    八种基本类型： long int short byte char double float boolean   
    byte 1 short 2 int 4 long 8 char 2 double 8 float 4 boolean 1

3.  Spring依赖注入说一下
    1. 依赖注入主要解决 程序之间的耦合关系，可以将依赖的关系交给spring 管理，当需要的时候，从spring获取就可以使用了
    2. 能够依赖的数据主要有三种 基本类型+spring ， bean 对象, 负责集合类型
    3. 依赖注入的方式 
        1. 构造方法依赖注入，就是在构造函数时赋予初始值
        2. set 注入方式 常用的方式
        3. 注解方式
            1. 用于创建对象
                1. Component  普通定义
                2. Controller  接口层
                3. Service  业务层
                4. Repository 数据层
            2. 用于初始化
                1. Autowried  自动注入
                2. Qualifier  搭配Autowired 注入
                3. Resources 直接按照bean id 注入
                4. Value 基本数据类型 或者 String 注入 ${表达式}
        4. 用于改变作用范围
            1. scope 
                指定作用的范围， value 为取值 常用为 singleton（单例） prototype（多例）
        5. 和生命周期相关
            作用等于 bean 标签中 init——method 和destroy——method 类似
            PreDestory  指定销毁时
            PostConstruct  指定初始化
            
4. Ipv4的C类地址说一个
    IPV4中A类IP地址，其中在IP地址的四段号码中，第一段号码为网络号码，
    剩下的三段号码为主机号。而且其中的网络地址的最高位必须是“0”。A类地址的范围为：1.0.0.1-126.255.255.254。  
    
    IPV4中B类IP地址，其中在IP地址的四段号码中，四段号码中的前两段号码为网络号码。
    用二进制表示B类IP地址的话，B类IP地址就由2字节的网络地址和2字节主机地址组成，
    而且网络地址的最高位必须是“10”。B类IP地址的范围：128.0.0.1-191.255.255.254  
    
    IPV4中C类IP地址，其中在IP地址的四段号码中，四段号码的前三段号码为网络号码，
    剩下的一段号码为主机号。C类IP地址就由3字节的网络地址和1字节主机地址组成，
    网络地址的最高位必须是“110”。C类IP地址的范围：192.0.0.1-223.255.255.254。  
            
5. left join 为什么需要小表驱动大表，原理是什么
    MySql 的执行顺序会先执行子查询，再执行主查询，然后获得我们要查询的数据。  
    
    在实际操作过程中我们要对两张表的dept_id 都设置索引。在一开始我们就讲了一个优化原则即：
    小表驱动大表，在我们使用IN 进行关联查询时，通过上面IN 操作的执行顺序，
    我们是先查询部门表再根据部门表查出来的id 信息查询员工信息。我们都知道员工表肯定会有很多的员工信息，
    但是部门表一般只会有很少的数据信息，我们事先通过查询部门表信息查询员工信息，以小表(t_dept)的查询结果
    ，去驱动大表(t_emp)，这种查询方式是效率很高的，也是值得提倡的。  
    
    MySQL 表关联的算法是 Nest Loop Join，是通过驱动表的结果集作为循环基础数据，
    然后一条一条地通过该结果集中的数据作为过滤条件到下一个表中查询数据，然后合并结果。

6. Mysql慢查询如何优化
    SHOW VARIABLES LIKE '%query%'      查询慢日志相关信息
　　slow_query_log 默认是off关闭的，使用时，需要改为on 打开　　　　　　
  　slow_query_log_file 记录的是慢日志的记录文件
　　long_query_time 默认是10S，每次执行的sql达到这个时长，就会被记录
    SHOW STATUS LIKE '%slow_queries%'  查看慢查询状态
    在要执行的sql前加上explain  例如：EXPLAIN SELECT menu_name FROM t_sys_menu ORDER BY menu_id DESC;
    system>const>eq_ref>ref>fulltest>ref_or_null>index_merge>unique_subquery>index_subquery>range>index>all
    如果发现type的值是最后两个中的其中一个时，证明语句需要优化了。
    extra 出现以下两个 Using filesort / Using tempoary 时候也是需要优化了
    Using filesort: 表示 mysql 会对结果使用一个外部索引排序，而不是按表里的索引顺序查到数据
    Using tempoary 标识 mysql 在对查询结果使用临时表 常见是 order by  group by 
    修改sql或者尽量让sql走索引
    mysql查询优化器会根据具体情况自己判断走哪个索引，
    不一定是走主键（explain中的key可以看到走的哪个key）具体情况根据具体情况来定，当你要强制执行走某一个key时：
    在查询的最后加上 force index(primary); 强制走主键的
    3.索引是建立得越多越好吗
　　　　1.数据量小的表不需要建立索引，建立会增加额外的索引开销。
　　　　2.数据变更需要维护索引，因此更多的索引意味着更多的维护成本。
　　　　3.更多的索引意味着也需要更多的空间。

7. Redis HyperLogLog
    Redis 在 2.8.9 版本添加了 HyperLogLog 结构。
    Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 的优点是，在输入元素的数量或者体积非常非常大时，
    计算基数所需的空间总是固定 的、并且是很小的。
    在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基 数。
    这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。
    但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。
    
    关于 HyperLogLog 的原理我这里也不进行详细赘述，说实话那一套算法以及调和平均公式我自己也没太整明白；下面大致说一下我个人的朴素理解    
    Redis 中的 HyperLogLog 一共分了2^14=16384个桶，每个桶占 6 个 bit    
    一个数据，塞入 HyperLogLog 之前，先 hash 一下，得到一个 64 位的二进制数据
    取低 14 位，用来定位桶的 index
    高 50 位，从低到高数，找到第一个为 1 出现的位置 n若桶中值 > n，则丢掉反之，则设置桶中的值为 n
    那么怎么进行计数统计呢？
    拿所有桶中的值，代入下面的公式进行计算

    hyperloglog通常是用来非精确的计数统计，前面介绍了日活统计的 case，当时使用的是 bitmap 来作为数据统计，然而当 userId 分散不均匀，小的特别小，大的特别大的时候，并不适用
    在数据量级很大的情况下，hyperloglog的优势非常大，它所占用的存储空间是固定的2^14 下图引用博文《用户日活月活怎么统计》
    使用 HyperLogLog 进行日活统计的设计思路比较简单
    
    每日生成一个 key
    某个用户访问之后，执行 pfadd key userId
    统计总数: pfcount key
    

