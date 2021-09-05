1. http://maven.apache.org/download.cgi   maven 下载地址
2. wget https://mirror.bit.edu.cn/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz 下载tar包
3. tar -zxvf apache-maven-3.6.3-bin.tar.gz  解压tar包
4. 修改环境变量 vim /etc/profile
增加内容 
```
export MAVEN_HOME=/usr/local/src/apache-maven-3.6.0
export PATH=$MAVEN_HOME/bin:$PATH
```
5. source /etc/profile
6. 测试 mvn -v


