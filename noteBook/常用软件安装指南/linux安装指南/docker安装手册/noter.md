使用官方安装脚本自动安装
安装命令如下：

curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
也可以使用国内 daocloud 一键安装命令：

curl -sSL https://get.daocloud.io/docker | sh

启动docker
sudo systemctl start docker

参考文档：https://www.runoob.com/docker/centos-docker-install.html


配置docker hub

需要修改 sudo vim /etc/docker/daemon.json

增加
{
  "registry-mirrors": ["https://82ba41hq.mirror.aliyuncs.com"],
  "insecure-registries": ["harbor.eip.com:8843", "0.0.0.0"]
}
然后登录 docker hub 

sudo docker login -u eip -p OTMxOWUwZjViY2Ji harbor.eip.com:8843