yum -y install git

git --version

```
git clone https://@code.mlamp.cn/0002852/dashboard.git
 
cd dashboard/
 
git checkout dev
 
mvn -U clean package -Prelease -Dmaven.test.skip=true
 
mv  dashboard-server-dist/dashboard-backend/target/dashboard.tar.gz ..
```