## 介绍

mockserver是模拟http返回报文的一个mock 服务。 可以用于微服务架构下和前端（h5，native app）模拟后端服务报文的开发联调和测试。
hissummer mockserver 不仅仅是一个restful api的mock server且支持mockserver注册到eureka发现中心，可以方便的进行eureka服务实例的mock测试。

##  支持的功能

* http协议（若想支持https 建议前面通过反向代理支持，因为mockserver可以自定义domainname，但是通过tomcat支持多个domainname的ssl证书应该无法解决）
* mock 规则的管理
* 支持eureka 服务的注册，心跳，取消注册功能

## 部署

1. 源代码构建

    如果需要自己构建代码或者构建镜像，请访问 https://github.com/hissummer-mockserver/buildStandaloneWar

    1. 使用已构建的war文件

       1. 部署之前

           1. 您需要先安装mongodb 服务器并启动。 <a href="https://docs.mongodb.com/manual/introduction/"  target="_blank" > 什么是mongodb </a>

           1. 如何安装mongodb ？
              1. <a href="https://docs.mongodb.com/manual/installation/" target="_blank">官方文档</a>
              1. <a href="https://cloud.tencent.com/developer/article/1360756" target="_blank">linux安装中文文档</a>
              1. <a href="https://www.runoob.com/mongodb/mongodb-window-install.html" target="_blank">windows安装中文文档</a>
              1. docker 部署mongodb  "sudo docker  run -d mongo:4.2.5-bionic "

           1. 如何验证mongodb启动成功
      使用客户端访问并可以连接，或者使用telnet ip port 来验证mongodb服务器监听的端口是否可以链接。

       1. 部署hissummer mockserver

           1. 单独启动
              将war下载后,直接执行命令启动.  <a href="https://github.com/hissummer-mockserver/mockServer/packages" target="_blank">版本下载</a>

            ```
            $java -jar hissummer-mockserver.war  --server.port=8081 --spring.data.mongodb.host=localhost --spring.data.mongodb.port=27017   
            ```

            (备注： spring.data.mongodb.host 和 spring.data.mongodb.port 分别为mongodb 服务的ip和端口号， server.port 为mockserver 的服务端口号)

          1. tomcat容器部署

            下载tomcat，并将war包放置于tomcat home目录下的webapps下，启动tomcat
            启动后，用浏览器访问 http://localhost:8081 （端口号是你在tomcat的config/server.xml中设定的端口）  

1. docker部署

```
$sudo docker run -d -e mongodbHost=${mongodbHost} -e mongodbPort=${mongodbPort} -p 8080:8080   nighteblis/hissummer-mockserver  
```
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
