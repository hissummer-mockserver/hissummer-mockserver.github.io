# war包部署

[war包下载](https://github.com/hissummer-mockserver/buildStandaloneWar/releases)

如果想自行构建war包，需要使用(hissummer-mockserver/buildStandaloneWar)中的build.sh脚本进行构建并打包，打包后的war会包含前端代码。具体构建方法及步骤请访问"[war构建文档]( https://github.com/hissummer-mockserver/buildStandaloneWar)"。此后的文档假设您已经成功构建了war包或者已经下载了构建好的war包。

1. 部署mongodb

    安装mockserver之前需要先部署mongodb，mongodb部署请阅读请访问“[mongodb部署](../deploymongodb)”

1. 部署hissummer mockserver

    1. 单独启动
        将war下载后,直接执行命令启动.  <a href="https://github.com/hissummer-mockserver/mockServer/packages" target="_blank">版本下载</a>

        ```
        $java -jar hissummer-mockserver.war  --server.port=8081 --spring.data.mongodb.host=localhost --spring.data.mongodb.port=27017   
        ```

        (备注： spring.data.mongodb.host 和 spring.data.mongodb.port 分别为mongodb 服务的ip和端口号， server.port 为mockserver 的服务端口号)
        ```
        -DLOGBASE 指定输出的日志目录
        $java -DLOGBASE="/log/path"  -jar hissummer-mockserver.war --server.port=8082 --spring.data.mongodb.host=localhost --spring.data.mongodb.port=27017   
        ```        


    1. tomcat容器部署

        下载tomcat，并将war包放置于tomcat home目录下的webapps下，启动tomcat
        启动后，用浏览器访问 http://localhost:8081 （端口号是你在tomcat的config/server.xml中设定的端口）  
