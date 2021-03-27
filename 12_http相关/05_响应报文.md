# 响应报文(给浏览器看的)
    HTTP/1.1 200 OK
    X-Powered-By: Express
    Content-Type: text/html; charset=utf-8
    Content-Length: 2
    ETag: W/"2-eoX0dku9ba8cNUXvu/DyeabcC+s"
    Date: Fri, 01 Nov 2019 08:24:19 GMT
    Connection: keep-alive
    空行
    ok

## 报文首行
     HTTP/1.1 200 OK
       --协议名/协议版本 状态码 
## 报文头
    X-Powered-By: Express 
        --服务器所采用的框架，一般不返回容易造成安全漏洞。（尽量不要让用户知道服务器具体采用的技术）
    Content-Type: text/html; charset=utf-8
        --告诉浏览器返回资源的类型及编码格式
    Content-Length: 2
        --返回数据的长度
    ETag: W/"2-eoX0dku9ba8cNUXvu/DyeabcC+s"
        --协商缓存必要字段
    Date: Fri, 01 Nov 2019 08:24:19 GMT
        --响应的日期+时间
    Connection: keep-alive
        --服务器告诉浏览器，下次请求时，或许会采用长连接。
## 空行

## 报文体
    ok