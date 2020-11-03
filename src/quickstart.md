# 快速开始
1. 打开首页

    [部署](../#_3)成功后访问http://localhost:8080
    ![homepage](../img/homepage.png)
    如果打开如上图页面，则证明部署成功。v0.0.4版本增加了登陆功能，默认用户名/密码为admin/hissummer.com。

1. 添加http规则

    添加一个hostame为*（可以匹配任何Host)， 一个接口/test 的mock规则。
    ![homepage](../img/addrule.png)

    添加成功后，如下图会提示添加成功，并查询到已添加的mock规则。
    ![homepage](../img/addok.png)


1. 访问接口返回mock报文

    访问mock规则的接口：http://localhost:8080/test

    ![homepage](../img/httpmock.png)
