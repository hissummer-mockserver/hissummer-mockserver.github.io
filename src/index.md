## 介绍

mockserver是模拟http返回报文的一个mock 服务。 可以用于微服务架构下和前端（h5，native app）模拟后端服务报文的开发联调和测试。
hissummer mockserver 不仅仅是一个restful api的mock server且支持mockserver注册到eureka发现中心，可以方便的进行eureka服务实例的mock测试。

##  支持的功能

* http协议（若想支持https 建议前面通过反向代理支持，因为mockserver可以自定义domainname，但是通过tomcat支持多个domainname的ssl证书应该无法解决）
* mock 规则的管理
* 支持eureka 服务的注册，心跳，取消注册功能

## 部署

推荐使用docker-compose进行部署。如果使用docker和源码或者war包部署，请先部署mongodb服务，[如何部署mongodb？](deploy/deploymongodb/)。

1. war包方式部署

    > 注意：此方式部署，需要先部署mongodb服务！

    [war包部署文档](deploy/compile/)

1. docker部署

    > 注意：此方式部署，需要先部署mongodb服务！

    `$sudo docker run -d -e mongodbHost=${mongodbHost} -e mongodbPort=${mongodbPort} -p 8080:8080   nighteblis/hissummer-mockserver`

    mongodbHost 是mongodb服务的地址, mongodbPort 是mongodb服务的端口号

1. docker-compose 部署

    ```
    $git clone git@github.com:hissummer-mockserver/buildStandaloneWar.git
    $cd compose
    $sudo docker-compose up -d
    ```

## 快速开始


## 使用文档

1. 匹配流程

    >http mock匹配规则说明
    >1. 同样的hostName和uri 只能添加一条    
    >1. hostName 为* 时, 即表示可以匹配所有的hostName.    
    >1. hostName(不为*) 和 uri如果 没有匹配到,会尝试匹配hostName为*的规则    

    >**示例如下:**
    >若添加有2条规则
    >* 第一条规则: hostName:*  uri:/hello  mockResponse: mock1
    >* 第二条规则: hostName:testHostName  uri:/hello  mockResponse: mock2
    >>* 当访问 http://127.0.0.1/hello 时(通过ip地址访问mock server), 则会匹配第一条规则， 返回报文： *mock1*.
    >>* 如果我访问者 http://testHostName/hello 时,会匹配到第二条规则，返回报文：*mock2*. (testHostName 需要添加hosts或者dns添加record)
    >>* 再如果我访问 http://testanotherHostName/hello 时, 则会尝试先匹配 hostName=testanotherHostName, uri=/hello  找不到则会寻找
    >>* hostName=testanotherHostName , uri=/ , 如果再找不到则开始寻找 hostName=* , uri=/hello，返回报文: *mock1*。

1. 如何Mock的报文

    1. 静态response报文呢
        > 即创建mock规则的响应报文内容不做任何处理直接返回。

    1. 动态response报文
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

## 赞助
