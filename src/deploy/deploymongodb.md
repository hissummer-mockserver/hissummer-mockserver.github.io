# mongodb服务部署

部署hissummer-mockserver之前，您需要先安装mongodb 服务器并成功启动。 <a href="https://docs.mongodb.com/manual/introduction/"  target="_blank" > 什么是mongodb </a>

1. 如何安装mongodb ？
    1. <a href="https://docs.mongodb.com/manual/installation/" target="_blank">官方文档</a>
    1. <a href="https://cloud.tencent.com/developer/article/1360756" target="_blank">linux安装中文文档</a>
    1. <a href="https://www.runoob.com/mongodb/mongodb-window-install.html" target="_blank">windows安装中文文档</a>
    1. docker 部署mongodb  
        `sudo docker  run -d mongo:4.2.5-bionic`

        docker 镜像的tags linux中可以使用 mongo:4.2.5-bionic，其他的tags请参考[mongodb 官方镜像文档](https://hub.docker.com/_/mongo)。

1. 如何验证mongodb启动成功
    使用客户端访问并可以连接，或者使用telnet ip port 来验证mongodb服务器监听的端口是否可以链接。
