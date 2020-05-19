## 一 工作原理

1.  请求路径的匹配(request path match)

2. 返回mock报文的处理
    1.  第一步首先处理${\_\_内建函数}变量替换。例如${\_\_NowDate()} 替换成 1539313200000
    2.  第二步请求header，请求body中的取值替换 。 例如${requestBody.a} 将本次请求的body中的a值获取到并替换。

            例如： 请求的header content-type: application/json,  body 为  {'a':'value'} , 那么 mock response的报文中 ${requestBody.a}  将会替换成  value值

    3. 第三步，如果是groovy脚本，则执行groovy脚本。 并将groovy脚本中的response变量的值作为要返回的response值。
    4. 第四步，将response所有的换行符删除。

## 二 Http Mock规则
Http Mock Rule，定义一个http接口的mock报文。
### 规则属性
* id
* hostName
* uri
* 工作模式
* 响应Header
* 响应mock报文

    Mock报文如2种方式：

    1. 静态response报文呢

        > 即创建mock规则的响应报文内容不做任何处理直接返回。

    1. 动态response报文
        1. 内建函数

            > 内建函数的命名规则同Jmeter，不支持嵌套使用。 但一个responseBody总可以使用多个内建函数。 ${\_\_NowDate(arg1,arg2)} NowDate为函数名称。

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

            > 通过${responseBody.a}

            > 通过${responseHeader.a}

        1. groovy脚本
```
            //groovy
            a='myresponse'
            response=a
```

        groovy中设置response变量的值就是要返回的值，response的值可以用groovy脚本生成。
### 操作

1. 添加

1. 删除

1. 修改

1. 复制添加

### 匹配规则

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

## 三 Eureka Mock规则
Eureka Mock Rule， 定义如何注册一个eureka服务实例。
### 规则属性
* id
* eurekaServer
* eureka ersion
* hostName
* port
* serviceName
* status (disable/enable)
### 操作
1. 添加

1. 删除

1. 修改

1. 复制添加
