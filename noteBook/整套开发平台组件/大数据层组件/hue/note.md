HUE
    大数据平台 可视化 操作界面
1. hadoop 商业发行版 CDH -> WEB DESK -> HUE
2. 安装hue
    1.集群人选一台进行安装（这台机器不能安装mysql）
    2.上传解压
    3. 修改配置文件
    4. 重新加载文件
    5. 安装依赖
    6 解压 编译 进入解压后文件 执行 make apps
    7修改hue配置文件
    8. 启动测试
3. 整合
    1. 整合 mysql
    2. 整合 hdfs  可以直接操作hdfs 文件
    3. 整合 mapreduce 可以查看正在跑的程序
4. 配置mysql
    修改desktop/conf/hue.ini 这个配置文件里面修改
5. 整合hdfs
    修改 hadoop 平台文件
        hdfs-site, core-site
    修改 hue.ini 的配置文件
6. 整合yarn 操作
