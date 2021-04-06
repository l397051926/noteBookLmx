前端打包方式，使用npm ，所以需要在服务器上 安装最新版本的npm-也就是先安装node
1. 安装node
    1.1 下载node包，然后解压，然后配置环境变量即可安装，具体版本可以查看观望，配置环境变量方法
    1.2 配置环境变量
```shell script
export NODE_HOME=/opt/node
export PATH=$NODE_HOME/bin:$PATH
```
    1.3 配置完环境变量则需要 source /etc/profile
    1.4 使用淘宝镜像
    npm install -g cnpm --registry=https://registry.npm.taobao.org
    
    
2. 打包方式
    1.第一种 npm run deploy / npm run build 
