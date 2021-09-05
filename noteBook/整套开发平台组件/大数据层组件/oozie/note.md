1.oozie 训象人 -操作hadoop 功能 apache oozie workflow for hadoop
    1. workflow(工作流程)
        1. 有多个工作单元组成
        2. 有先后执行顺序
    2. scheduler （定时调度其）

2.作用
    1. 监控当前工作单元，完成后自动开启下一个
    2. 定时调度 工作
3.模块
    1. workflow  定义工作流程
    2. coordinator 协调器 ，定时触发workflow
    3. bundle 绑定多个 coordinator
4. workflow 常用节点
    1.workflow 常用节点
        1. 控制流节点
            工作单元执行顺序
        2. 动作节点
            对应工作 单元
5. 特殊说明 - 依赖hadoop 生态圈很严重 ， 因此原生的oozie 需要修改其对应的源码， 需要匹配hadoop 的所有版本，指定好编码，然后进行编译
    适用 cdh 或者 tbds 环境 可以直接指定 对应版本，oozie 就会匹配对应的hadoop 环境
6. 需要配置代理用户，
    1. 可以指定 代理用户工作在哪个 hosts 和指定工作 哪个用户组 ，可以适用 *通配符代替
7. 安装oozie
    1. 解压jar包
    2. libbext 创建这个文件 ，放入hadoop 相关jar包，相关驱动 ，ext-2.2.tar 前端包
    3. 修改 oozie 配置文件， 配置一个下mysql 的配置文件， 修改hadoop的configuration
    4. 初始化mysql 数据库
    5. 然后打成一个war包
8. 执行脚本
    bin/ooziedb.sh create -sqlfile oozie.sql
9. 打包
    bin/oozie-setup.sh prepare war
10.启动
    ozie start
11.登录页面
    hadoop102:11000
12.oozie 的使用
    1. 编写 workflow.xml
    2. 将配置文件上传至hdfs指定路径
    3. oozie job
    实战： 编写两个文件
        1. workflow.xml
        2. job.properties -配置 workflow 动态参数
        需要把 文件传到hadoop 文件内
        提交任务
        bin/oozie job -oozie http... -config
