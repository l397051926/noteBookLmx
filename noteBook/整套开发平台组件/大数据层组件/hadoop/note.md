1.jvm -juc
    1. 进程/线程
        1.后台开启的程序就是进程
        2.当前进程开启多个线路执行不同功能 就是线程
    2. 并发/并行
        1. 同时执行某个功能，由多个线程执行 就是并发
        2. 并行，能够同时执行不通或相同的功能 就是并行 执行
2. 三个包
    1. java.util.concurrent
    2. java.util.concurrent.atomic 原子类
    3. java.util.concurrent.locks 锁
    高内聚 低耦合 -> 线程 操作 资源类  资源是封装了一堆业务的功能对外暴露函数，方便线程来调用
    锁最好放在 资源里， 用来锁资源
3. 代码实例
    psvm{
        Ticket ticket = new Ticket();
        new Threade(new Runnable{ run{....}},"thread_name").start();
    }
    psvm{

    }
4.函数式编程
    1.拷贝小括号 写死右箭头 带上大括号
    2.@FunctionalInterface
    3.default
    4.static
5.解决 arraylist 线程安全问题
    1. new vector()
    2. Collections.synchonizedList()
    3. CopyOnWriteArrayList()
6. 写实复制技术- 读写分离的前身 分成读锁 写锁
7. set 的 concurrent
    copyOnWriteArraySet
7. map
    concurrentHashMap
8. 8 锁演示
    1. synchoniszed
    2. 静态 synchoinzded 也保证了锁
    3. 静态 锁 不会在锁定对象了
    4. 静态 和 普通同步 锁就锁不住了
    5. static 修饰的锁 是全局锁  
9. TimeUnit.SECONDS.sleep(4) --- 高级休眠时间
10. 多线程 编程资料
    1. 判断/干活/通知
    2. 轮番使用 使用 wait  notifyAll
    3. 多线程 notifyAll 要使用wile 不允许使用if
    4. 使用wile 防止 虚假唤醒
    5. wait 只能和 synchoinzded 组合使用 使用lock 不需要使用这个，而改用 condition这个
        使用方法是 locl.condition   condition.await() 与 condition.signalAll() 这两个方法
    6.新需求 A 5次 B 10次 C 15次 新方法 ，增加标志位 ，可以搞多个 condition 一个lock ，可以指定condition 进行执行
    7.Callable 说明 不能用 new Thread();
    8. fUTERtASK<Integer> futerTask = new FunerTask(new Callable)
    9. new Thread (futerTask,"A")
    10.Integer result = futerTask().get();
11.jvm
    1.jvm 体系
        1.jvm 运行在操作系统之上，它与硬件没有直接的交互
        2.类装载器 classloader
            1.bootstrap classloader
            2.Exector classloader
            3.systemctl classloader
12. hadoop
    url
        hadoop:50070/dfshealth.html
    1. hdfs
    2. map reduce
    3.版本问题
        1. hadoop
        2. clooders
        3. hortonWords
    4. 4高
        1.高可靠性， 多副本机制
        2.高扩展性 ，加个机器就可以用
        3.高效性 并行工作
        4.高容错性 会解决节点失败的任务
    5.hadoop的组成
        1.0 时代
            1. map reduce
            2. hdfs
            3. common
        2.0 时代
            1.map reduce
            2. yarn
            3. hdfs
            4. common 辅助工具
    6. hdfs 架构
        1. namenode 管理资源的节点
        2. datanode 实际数据存储节点
        3. secondar namenode 辅助name node 去保存数据
    7. yarn
        1. 调度资源 内存 cpu
        2.组成
            1. Resource Manager 项目组长， 总览整个集群资源的人，处理客户请求 监控nodeManager 启动或监控ApplicationMaster 资源分配调度
            2. NodeMananger 管理每个节点上的资源， 处理 resourceManager的命令 处理来自 ApplicationMaster的命令
            3.ApplicationMaster 负责数据切分 为应用申请资源 并分配任务  任务监控和容错
        3.安装hadoo
            1. 安装jdk
            2. 安装hadoop
        4. 本地运行 hadoop
            hadoop02:50070
        5. 远程拷贝  
            scp
            rsync  // 只能在本地开发
        6. hdfs 优缺点
            1. 不适合低延迟数据访问
            2. 无法高校的对小文件进行存储
            3. 不支持并发写入， 不支持文件随机修改
        7. namenode
            1.管理hdfs 命名空间
            2. 配置副本测策略
            3. 管理数据块映射信息
            4. 处理客户端读写请求
        8. datanode
            1. 存储实际的数据块
            2. 执行数据块的读写操作
        9.block 128m 默认
        10. FileSystem fileSystem = FileSystem.get(URI.create(),new Configuration,"username")
        11. HDFS 写数据流程
            1.首先有个本地文件 200M
            2. 需要一个客户端 client
            3. client 读取这个文件
            4. DistributedFislSystem 读取这个文件
            5. 先发起一个请求， namenode 会判断这个文件是否正常 /path /权限
            6. 然后把这个文件切块， 逻辑切分 -128M
            7. 上传hdfs 开了一个输出流 FSDataOutPutStream
            8. 请求上传 第一个block
            9. namenode 返回一个datanode 的lisit -》 取决于你配置集群的副本次数
            10.返回的list 比如3ge datanode ，有规则  第一个离这个机器最近的节点，第二个和第三个 不在第一个这台节点上
            11. 上传是有顺序的 比如 dn 1 -》 dn2 -》 dn3 ，dn3 返回 dn2 返回 dn1 ，代表文件通了
            12. 通道通了后开始写 packet dn1， 落盘 发送给 dn2 以此类推
            13. packet 不是一个一个发送的，而是以队列的形式发送的
            14. 文件传完后， 告诉 namenode 文件已经传完 关掉对应的流
        12. hdfs 写的时候的问题
            1. 每次发送package 都会重新获取 dn list  所以最小存储单位是 block
            2. 建立通道时 失败了 则失败了
            3. 如果 dn1 传输文件失败了 则还是失败的
            4. 如果 dn1 -> dn2 或者 dn2 ->dn3 失败了， 则返回还是会成功， hdfs会自动复制dn1 节点 兴盛三个副本
        13. hdfs 读过程
            1. client 向 namenode 申请下载文件
            2. namenode 会判断这个文件是否正常  权限 /path 等
            3.一切正常后 开始一个输入流 FSDataInputSteram ，namenode 返回包含第一个block 的三个datanode 节点
            4. client 会向 dn1 如果成功 则直接返回数据， 如果 dn1 失败则一次向 dn2 请求
            5. 第一块完成 然后在namenode 获取第二个blck
            6， 一直到最后一个结束 namenode 会告诉文件大小已经结束了
        14. 相邻机架问题 -机架感知
            1.第一个节点在 本地， 第二个节点同机架不同节点， 第三个不同机架不同节点
        15. 额外 redis 持久化的方式
            1. RDB ->写如数据 ->加载高校 生成慢 -》 安全略低
            2. AOF -> 记录命令方式 -> 加载慢 生成快 -》安全性高
        16. hadoop namenode 持久化方式
            1. deits.log 记录数据变化的方式
            2. Fsimage 记录数据镜像
        17. secondeNameNode 将 edits.log 行程 Fsimage 镜像
        18. datanode
            1.包含数据信息
            2. 包含对应数据 block_meta 信息
        19. 如果保证传输数据完整性
            1.crc 算法
            2.md5 算法
        20. 如何扩展集群
            1.扩展hadoop 安装程序
            2.修改hadoop 配置
        21. x的特性
            1. 集群间数据拷贝
            2. 小文件存档 可以对一堆小文件进行镜像打包
        22. mapReduce
            1. 优点 是 分布式  简单 好扩展
            2.缺点 慢 不适用 流失计算 实施计算
        23. mapReduce
            1. map
                把数据映射成别的形式
            2. reduce
                把映射后的信息 合并 规约 成最后的文件
        24.woder count
            1. map 阶段 的并发 MApTask 完全并发执行 互补相关
            2. reduce 并发 reduce task 完全不相干扰，但是他们的数据依赖上一阶段map 的输出
            3. map reduce 可以实现多个 map reduce 来组合 实现功能
        25. 如何配置执行参数
            params arguements
        26. 如何在打包在服务器上执行
            1. 打包 上传到服务器上
            2. hadoop jar 1.jar [main] [input] [output]
        27. hadoop 序列化
            不用java 序列化 ，使用了Writable 参数
            优点   
                1. 紧凑
                2. 快速
                3. 可扩展
                4. 互操作
            java 操作如果对象需要 用hadoop 序列化 ，需要实现 Writable，并实现 write 方法和 read 方法
        28. mapreduce 分布式机智
            1. inputformat 用于划分数据 切了多少块 就会有多少个maptask
            2. 多种 inputformt ，也可以自定义inputformat
        29. MapReduce 全流程
            1. 准备带处理文本      
            2. 客户端 完成堆文件切片流程
            3. yarn 根据切片信息 分配资源 分配mapTask 数量
            4. MApTask 拿到第一段数据， 调用 inputFormat 获取 RecorderReader 生成kv 值 交给mapper
            5. mapper 逻辑处理后 使用 Context.writer 写个 环形缓冲区中
            6. 环形缓冲区， 存储了 map给 的kv 数据， 默认 100m ，从map 出来的数据 按照key 做了一个全排序， 进行分组
            7. 大数据如何进行全排序， 将部分数据 进行局部排序， 然后将多块 合到一块， 用归并排序
            8. 首先在环形缓冲区 进行排序，使用快速排序， 然后缓冲区满了后 落入到一个文件中，每满一次就进行落入文件中，最后将多个文件进行归并排序
            9. 通过 环形缓冲区后，会产生一个文件，这个文件是一个有序的文件
            10. reduce 之前阶段 ，多个mapTask  都将发给 reduce ，每个mapTask 完成数据是有序的，reduce 在归并排序一次
            11. 然后reduce 获取到一个 排序的数据 ，然后reduce 处理逻辑 将数据交给 outputStream
            12. reduce 的数量是由我们自己设定的 job.setNumReduceTasks(10)
            13.  partition 分区操作 ,标明这个数据 应该去哪个reduceTask
                1. 分区怎么分
                    默认使用 hashcode 莫 key 的hash 去分配到哪个reduceTask
                2. 实现 自定义 partition
                    继承  Partition
                    重写 getPartition() 方法
            14. shuffle
                1.在环形缓冲区内 到达 80% 就会进行反转，在这期间会进行 分区 排序 使用快排方法，然后落入此片，载次读取 到达80% 重复操作
                2. 在落入磁盘时 会判断是否执行 combiner 然后进行归并排序 合成一个大文件
            15. 排序
                实现 WritableComparable
            16. combiner 合并操作    
                combiner 本身就是 reduce 的一个过程 ， Combiner 是在mapTask 起作用 和reduce 中间阶段， 他存在的目的主要是减少磁盘的io
                分组 时要注意排序的问题， 因为map reduce 阶段会先排序 后分组，因此，如果排序出现问题会导致分组出现问题
            17. shuffer 过程
                1.map逻辑处理
                2. 写入环形缓冲区，
                3.当环形缓冲区满时 会溢写到磁盘上，在写磁盘之前会进行分区 然后进行排序 分区排序是同时处理，使用的是二次排序
                4. 当进入缓冲区时 会有 k，v ，p（分区）
                5.如果有Combinar 会先进行 combinar 在写入磁盘
                6.多个落地的数据会进行归并排序，在combiner在从mapTask 出来 ，准备进入reduce阶段
                7.每个rudece阶段 会获取所有mapTask数据，会根据分区 去处理数据
                8.在进入reduce 之前会进入一个内存缓存中，然后会将多个mapTasik的 分区数据进行归并排序，然后再次进行分组，最后进入reduce中 处理逻辑
                9.reduce 逻辑处理完就进入 outputFormat
            18.环形缓冲区的好处
                1.没头没尾，可以在任何一个点开始处理数据
                2.逻辑是环形的，物理上还是条型缓冲区
                3. 当容量快到80%开始以溢写
                4. 然后剩余20% 找一个点继续写数据，这样可以持续的写数据，不需要等待
                5. 进入环形缓冲区的数据 会从两侧开始写 一测存储索引，另一侧存储kv 两边一一对应，排序的时候，只移动索引，不需要移动kv，提高效率
            19. outputFormat
                1.Text outputFormat
                2.SequencOutputFormat 两个mapreduce 的衔接
            20. reduceJoin
                join 哪个字段 就将哪个字段 都进入相同分组里
            21. mapJoin
                join 在map 阶段执行适用于 一张小表 join 一张大表
            22. hadoop ha jernnnode 保存元数据信息
            23. yarn-ha 集群
                1.可以根据资料 配置yarn 的高可用配置
                2. hadoop102:8088 yarn 的地址
            24. hadoop Federation   架构设计
                1.为了解决 namenode 的内存不够问题
            25. 倒排索引 - Toi 项目
                倒排索引 就是 从文章到数字
                正排索引 就是 从标题到内容
            26. 压缩， 可以在output input 会自动识别压缩，map到reduce 也可以压缩
            27. yarn  集群的任务管理器，只负责任务资源分配和 调度
                1.架构
                    1. resourceMananger
                    2. NodeMananger
                    3. ApplicationMaster
                    3. Container
                2. nodemananger 通过 Container 来管理集群资源
                3. Container 就是执行的任务， 执行之后在进行销毁
                4. 资源调度其
                    1.FIFO 先进先出
                    2.Capactty Scheduler 容量调度其 ，多个先进先出
                    3.Fail Scheduler 公平调度其 ，可以分等级，每增加任务就会增加入口，分开资源一起执行
                       可以支持多级多列的关系，调整优先级
                5. 任务推测执行
                    1. 多节点执行任务， hadoop 会在一定时间检查一下每个节点执行的任务，如果发现一个任务远远低于总任务的平均时间，会在另一个节点启动一个最慢的任务，比较新节点的任务和最慢节点任务谁先执行完，则使用谁。

                6.优化 --在查





