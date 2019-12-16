# Hissummer Mock server
* ## 介绍
    > mockserver是模拟http返回报文的一个mock 服务。 可以用于微服务架构下和前端（h5，native app）模拟后端服务报文的开发联调和测试。
    为什么使用hissummer mock server？ 
    
* ## 部署
1. 部署文件
    1. 源代码构建
        > 请使用最新的master分支进行构建
    1. 使用已构建war文件

1. 部署方式
    1. 单独启动
        > 将war下载后,直接执行命令启动
    1. tomcat容器部署
        > 下载tomcat，并将war包放置于tomcat home目录下的webapps下，启动tomcat    

* ## 使用
1. 静态response
    > 即填写的内容不做任何处理直接返回。
    
1. 内建函数
    > 内建函数的命名规则同Jmeter，不支持嵌套使用。 但一个responseBody总可以使用多个内建函数。 ${__NowDate(arg1,arg2)} NowDate为函数名称。

    1. NowDate("yyyy-MM-dd HH:mm:ss")  日期为可选参数，若不填写即时当前时间秒。 若填写返回指定的时间的java时间秒。
        > 示例：
        NowDate("2018-10-12 11:00:00") ->  1539313200000
        NowDate()  ->  1539313200000 (当前时间的java秒) 
        
    1. RandomString(stringLength,stringCharactor) 
        > stringLength 返回的随机字符串长度
        > stringCharactor 返回的字符串的字符内容
        
        > 示例：
        RandomString("5","abcdefg")  ->  adefg
        RandomString("5") -> XZ6MKZOOF77MFABQ3V

1. 通过请求header或者请求body中获取数据
    > 通过
    
1. groovy脚本

* ## 赞助
