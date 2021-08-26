1. 下载地址[.tar.gz] https://github.com/alibaba/nacos/releases
2. 解压
```
sudo tar -zxvf nacos-server-2.0.3.tar.gz
```
3. 单机模式启动
```
cd /opt/nacos/nacos/bin
sh startup.sh -m standalone
```

遇到 jdk启动不了的问题
修改 startup.sh 
修改前
```
[ ! -e "$JAVA_HOME/bin/java" ] && JAVA_HOME=$HOME/jdk/java
[ ! -e "$JAVA_HOME/bin/java" ] && JAVA_HOME=/usr/java
[ ! -e "$JAVA_HOME/bin/java" ] && JAVA_HOME=/opt/taobao/java
[ ! -e "$JAVA_HOME/bin/java" ] && unset JAVA_HOME

```
修改后
```
[ ! -e "$JAVA_HOME/bin/java" ] && JAVA_HOME=/usr/java/jdk1.8.0_181
#[ ! -e "$JAVA_HOME/bin/java" ] && JAVA_HOME=/usr/java
#[ ! -e "$JAVA_HOME/bin/java" ] && JAVA_HOME=/opt/taobao/java
#[ ! -e "$JAVA_HOME/bin/java" ] && unset JAVA_HOME
```

http://127.0.0.1:8848/nacos/index.html

```
用户名:nacos
密码: nacos
```

集群形式
配置 cluster.conf
在文件里添加相关服务器IP，三台机器都做相同的配置
```
cd /usr/local/nacos/conf
cp cluster.conf.example cluster.conf
vim cluster.conf

```

cluster.conf配置内容
```
#it is ip
#example
#10.10.109.214
#11.16.128.34
#11.16.128.36
192.168.47.128:8848
192.168.47.129:8848
192.168.47.130:8848
```

创建数据库
```
脚本位置 /usr/local/nacos/conf/nacos-mysql.sql
将脚本里的SQL语句直接导入既可
```

配置application.properties
```
cd /usr/local/nacos/conf
vim application.properties

```

增加内容为
```
spring.datasource.platform=mysql
db.num=1
db.url.0=jdbc:mysql://192.168.47.128:5186/nacos_config?serverTimezone=GMT%2B8&characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
db.user=cici
db.password=123123

```

分步启动机器
```
cd /usr/local/nacos/bin
sh startup.sh

```

