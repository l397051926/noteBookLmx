elasticeach
最好的搜索库

1. es 能做什么呢
    1.全文检索 模糊查询 数据分析

2. 同类对比 soler  herma（腾讯）

3. 安装
    1.jdk
    2. es 单机安装
    3. tar 安装包就可以
    4. 启动 ./elearsearch
    5. chmod -R ELk:elk .
    6. curl localhost:9200  验证是否成功
    7. cd config
    8. vim eleasticsearch.yml
        networkhost 本机ip

4. 安装 kibana
    1. tar 解压即可
    2. cd config
    3. vim config
        port
        server.port
        elasticsearch.url
        kibana.index
    4.bin/kibana
    ip:5601

5. 操作
    dev toos 操作es

6. 存储方式
    1. 面向文档
    2.面向json存储

7. index 形式
    index:
        type:
            document:

8. 查询费昂是
    /index/doc/in
    /index/doc/_search 查询所有

9. 全文检索
    index/doc/_search?q-haha 模糊查询

10. group by
    6.2 新特性 需要指定

11. 正派所以 倒排索引
    正排索引： 根据id 取查找内容
    倒排索引： 根据内容取查找 id 依赖B +TREE 这个数据结构
    每个最底层数据都会维护一个posting list ：
                                            docid
                                            tf
                                            polition
                                            ooset

12. 每个文档都会构建一个倒排索引

13. 分词
    1. 字符过滤  去出一些 html 字符 和特殊字符
    2. 对文本分词 真正的分词过程
    3. 去掉一些奇怪词汇 ，指定不要词汇

14. 分词测试
    1._analyzer
    {
        "analyzer",
        "text": "xxx"
    }


15.  自定义分四期
    是一种 固定的json ，可以查文档 制作
    "analysis":{
        "analyzer":{
            "y":{

            }
        }
    }

16. 如果不指定id 会自己生成id
17. pretty 会自动格式化
18. 会对id 相同的数据直接更新操作
19. 批量操作 _bulk
    先指定文档id，然后指定实际数据

20. mapping
    查看  /mapping
    字段参数类型

21 api 搜索
    /_search?q=keyword&
    df=user //指定字段
    sort=age
    from=0&size=19
    timeout

22. term / phrase
    term 单词查询
    phrase 词语查询

23. body 查询方式
    {
        "query":{
            "match"{
                "username":"zhangsan"
            }
        }
    }

    {
        "query":{
            "match"{
                "username":{
                    "query"："zhangsan",
                    "operator":"and"
                }
            }
        }
    }

24. 相关性算法

25. es的监控一个小工具
    cerebro 本地小工具

26 logstash
    收集 过滤 输出 （清晰工具）
    使用场景
        1. 多个数据库 同步
        2. 持续收集 log/文件
        3.
