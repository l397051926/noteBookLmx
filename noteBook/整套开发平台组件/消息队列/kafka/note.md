kafaka
1. 基于大数据 实施的 分布式 消息队列
2. 传统javaee 消息队列一般应用
    1. 异步发送消息处理
    2. 消峰 ， 秒杀功能
    3. 解耦服务和服务之间的耦合
3. 消息队列两种模式
    1. 点对点模式
        1. 一个生产者 对应1个消费者
        点对点不会持久化数据
    2. 发布订阅模式
        1. 消费者订阅一个top ，当top 出消息时 所有订阅top 的消费者都会消费这条信息
        发布订阅会持久化数据
4. kafaka 基础架构
    1. 为了扩展方便 提高吞吐量， 一个top 会分多个 分区 partition
    2. 为了分区的设计，提出了消费者组的概念
    3. 一个kafaka 会有多个 broker
    4. 每个broker 里面是有分区 partition
    5. 每个partition 都有副本
5. kafaka 组件内容
    1. produce
    2. consumer
    3. consumer group
    4. broker
    5. topic
    6. partition
    7. re'plica 副本
    8. leader
    9. follower
6. 安装kafaka
    。。略
7. 创建 topic  
    bin/kafka-topics.sh --zookeeper 1.1.1.1:2181 --create first --partitions 3 --replication-factor 2
8. 引入 offect 偏移量
    每发送一条数据 都会有一个 offect  每个 consumer 消费一个也会保存offect 数据
9. 文件存储机智
    每个log 设置分片，以时间和大小进行分片，里面还保存了两种文件 一个是.log .index 一个对应数据 一个对应索引，方便查找数据
10.如果给一个 offect -3 如何查找在哪个文件
     根据文件名 判断在哪个index里，  然后用3 - 文件名 然后就查到了在哪个log里，然后在对应的log 文件里查找
11. 一般是在挂掉重启的时候才会查找这个偏移量 offect
12. 分区策略
    1. 方便在集群扩展，2 提高并发量
    2. 如何去分区
        1. produce 每次发送一个 produceRecord 对象
        2. 可以指定 partition 分区
        3. 如果没有指定 ，指定key  会根据key hash 取分区值
        4.如果没有指定key  也没有指定分区 就会使用轮询规则
13. 生产者如何发送消息
    1. 生产者 发送消息给消费者 ，如果收到消息 则会给反馈 生产者
    2. leader 选举机智 和zk类似 使用了 半数以上的机智
    3. isr 是一个集合里面是所有的 flower ，如果isr 全部通过，则可以返回接受数据成功
14. 三种可靠性等级 acks 来设计
    acks 0 ， produce 不管broker 回复 继续发送数据
    acks 1 ， leader 收到信息 给返回 不用等flower 就可以成功
    acks -1 all , 需要所有flower 和leader 都收到数据 才算成功
15. 数据故障处理
    LEO log end offset 日志最后的 偏移量
    HW high watermark 水位， 最小的LEO
    当 broker 挂掉的话 会从hw 处开始同步数据
16. 幂等性机智 增加这种机智 可以实现有 且只有一次 ， acks -1
    其实就是每个消息都有一个唯一id  保证每条消息的id 如果重复了 就不消费
17. 消费方式
    push 模式 很难适应消费者 速率不同的消费者，因为消费是由broker决定的
    pull 模式不足之处是 如果kafka 没有数据，消费者可能会陷入循环中
18. 分区分配方式
    1. roundrobin  轮询 分配分区策略 ，默认是轮询
    2. range  缺陷，以topic 为单位去分，可能会出现数据倾斜， 数据都堆在一个consumer 中
19 offect
    偏移量， consumer 挂掉 或者重启时，会从offect处开始数据， 0.9之前是存在zk 中 0.9之后值存在topic 中的一个字段中
20 高校读写数据 利用顺序写日志
    使用 零拷贝 机智
21. kafaka 的 controller 依赖zookeeper 的机智
    负责管理集群broker 的上下线， 每个broker 都会成为 controller ，启动时会向zk注册
    谁注册上了 谁就是controller ，biroker 上面的节点是 临时节点， 当某一个borker 挂掉后， controller 会监听到这个机智挂掉， 后续在处理 isr 喝leader 的关系
22. 创建topics 时会在zookeeper 注册  
23. 消费者的 offect  怎么保存处理
    需要开启 自动提交 offect  然后服务器重启后会从上次offect 绑定
    先把offect 提交给kafka 然后本地 保存一下kafaka 因为 本地保存会有单节点问题 所以将这个offect 保存在redis 或者其他文件目录里
    需要根据 offect 定位是哪个分区 consumer.seek 这个方式
24. 拦截器 实现一个接口 Interceptor
    1. configure
    2. onsend
    3. onAcknowledgenment
    4. close
25. kafka 中的 isr ar 代表什么 ， isr + or = ar
    hw， leo 代表什么
    kafka 中 只能保证分区内有序， 只用一个分区
    先拦截 在序列化 在分区
    一个分区只能被一个消费者消费
    什么时候会重复消费
    什么时候会漏消费
    











