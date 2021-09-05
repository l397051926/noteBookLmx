1. 概述
    是一个开源分布式 协调框架，通过 保存数据 和通知机智，来达到协调机智，包含 master follow
    zookeeper 必须半数以上 存活就可以工作
    zookeeper 必须全局一致
    更新数据顺序执行，client 的更新请求按照发送顺序依次执行
    数据更新原子性，一次数据更新要么成功 要么失败
2. zookeper 文件存储数据结构是 和树行 相同
    每个节点ZNode 存储，每个ZNode 只能存储1M数据
    create -s 有序节点
    create -e 临时节点， 当这个连接丢失后就会消失
3. zk 选举机智
    1.zab 协议 ，zookeeper 原子广播
        1. 没有leader 选leader
        2. 有leader 就干活
    2. Paxos 算法
    3. zk 会先比较 zxc id 在比较myid
        zxcid 是zk 的更新记录
    4. leader 干活机智
        1. server 获取一条写通知
        2. server 通知 leader
        3. leader 通知所有集群是否可以写 超过半数
        4. leader 通知所有人都写
        5.有一个代写队列
