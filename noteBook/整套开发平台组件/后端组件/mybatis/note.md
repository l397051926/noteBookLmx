1.mybatis 是什么？ 是一个orm框架 ，用于直接和数据库进行连接，方便直接使用
2.mybatis 底层整理
	1. 数据库源
	2. 数据库地址
	3. 数据库用户名
	4. 数据库密码
	5. 
sql语句


3.执行过程
	1. connect 连接
	2. 执行它
	3. 获取结果


4.源码过程
	1. 首先通过xml解析 xml 解析所有的配置信息


5.mapping解析方式有几种
	1. 4种
	2. package
	3. resource
	4. url
	5. class


总归 最后对会 形成 configuration 这个文件
