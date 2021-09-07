sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

sudo yum install -y nginx

sudo systemctl start nginx.service
sudo systemctl restart nginx 
sudo systemctl stop nginx

CentOS 7 开机启动Nginx
sudo systemctl enable nginx.service

开放80端口
##Add
firewall-cmd --permanent --zone=public --add-port=80/tcp
##Reload
firewall-cmd --reload

Nginx配置信息
网站文件存放默认目录
    /usr/share/nginx/html
网站默认站点配置
    /etc/nginx/conf.d/default.conf
自定义Nginx站点配置文件存放目录
    /etc/nginx/conf.d/
Nginx全局配置
    /etc/nginx/nginx.conf
Nginx启动
    nginx -c nginx.conf