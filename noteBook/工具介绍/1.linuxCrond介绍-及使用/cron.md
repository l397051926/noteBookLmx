# linux crontab 使用
## 说明
    linux cron 是linxu 本身自带的定时任务工具，可以定时的执行linux 的某些命令，比如我会用他定时执行 shell 脚本
## 实战使用

### 1. 使用 本身的cron 来操作
    1. 在linux /etc/crontab  该文件夹下 直接填写 要定时的时间 和 执行的命令
### 2. 使用用户下来执行定时操作
    1. 常用命令 归纳
        启动
        service crond start
        停止
        service crond stop
        重新加载
        service crond reload
        编辑 执行脚本
        crontab -e 
        查询脚本内容 
        crontab -l
        删除定时任务 
        crontab -r
    2. 具体操作
        2.1 启动crond
        2.2 编写脚本
        2.3 重新加载 crond
        
## 定时内容编写 
    29 11 * * * sh /home/liumingxin/test.sh
    分钟 时间 周 月 年 执行命令
    
        
