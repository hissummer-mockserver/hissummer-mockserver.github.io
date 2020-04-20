## 介绍

mockserver是模拟http返回报文的一个mock 服务。 可以用于微服务架构下和前端（h5，native app）模拟后端服务报文的开发联调和测试。
hissummer mockserver 不仅仅是一个restful api的mock server且支持mockserver注册到eureka发现中心，可以方便的进行eureka服务实例的mock测试。

##  支持的功能

* http协议（若想支持https 建议前面通过反向代理支持，因为mockserver可以自定义domainname，但是通过tomcat支持多个domainname的ssl证书应该无法解决）
* mock 规则的管理
* 支持eureka 服务的注册，心跳，取消注册功能

## 部署

推荐使用docker-compose进行部署。如果使用docker和源码或者war包部署，请先部署mongodb服务，[如何部署mongodb？](deploy/deploymongodb/)。

*  [war包部署](deploy/compile/)

    ！注意：此方式部署，需要先[部署mongodb](deploy/deploymongodb/)。

* docker部署

    ！注意：此方式部署，需要先[部署mongodb](deploy/deploymongodb/)。

    `$sudo docker run -d -e mongodbHost=${mongodbHost} -e mongodbPort=${mongodbPort} -p 8080:8080   nighteblis/hissummer-mockserver`

    mongodbHost 是mongodb服务的地址, mongodbPort 是mongodb服务的端口号

* docker-compose 部署

    ```
    $git clone git@github.com:hissummer-mockserver/buildStandaloneWar.git
    $cd compose
    $sudo docker-compose up -d
    ```

## 快速开始

[快速开始](quickstart/)

## 文档

[文档](documents/catalog/)

## 赞助
* paypal account: [https://www.paypal.me/nighteblis](https://www.paypal.me/nighteblis)
