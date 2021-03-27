# GET请求报文（给服务器看的）-- 通过form表单发送的GET请求

    GET http://localhost:3000/?name=kobe&password=123 HTTP/1.1
    Host: localhost:3000
    Connection: keep-alive
    Pragma: no-cache
    Cache-Control: no-cache
    Upgrade-Insecure-Requests: 1
    DNT: 1
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
    Referer: http://localhost:63347/0719_node/demo.html?_ijt=tphpp47dag8jevtqrnq44blv6p
    Accept-Encoding: gzip, deflate, br
    Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
    Cookie: Webstorm-9af2238=09820128-3adb-43e4-8242-a6f65c9e523a
    空行
    空行
## 请求报文首行
    GET http://localhost:3000/?name=kobe&password=123 HTTP/1.1
    -请求方式 协议名://主机地址:端口号/？urlencoded编码形式的参数 协议名/版本
## 请求报文头
    Host: localhost:3000
       --发送请求的目标主机：主机名:端口号
    Connection: keep-alive
       --处理完这次请求后继续保持连接，默认为3000ms
    Pragma: no-cache
       -- 不缓存该资源，http 1.0的规定
    Cache-Control: no-cache
       -- 不缓存该资源 http 1.1的规定，优先级更高
    Upgrade-Insecure-Requests: 1
       -- 告诉服务器，支持发请求的时候不用http而用https
    DNT: 1
       -- 浏览器告诉服务器：禁止跟踪。最终是否跟踪，还得看服务器是否配合。
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36
       -- 与浏览器和OS相关的信息。有些网站会显示用户的系统版本和浏览器版本信息，这都是通过获取User-Agent头信息而来的
    Accept:	text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,
    application/signed-exchange;v=b3
       -- 浏览器能够接收资源的类型及优先级，优先级不写默认是1,1的优先级是最高的。
    Referer: http://localhost:63347/0719_node/demo.html?_ijt=tphpp47dag8jevtqrnq44blv6p
       -- 本次请求是“站”在哪里发出去的。 1.防盗链。 2.广告计费
    Accept-Encoding: gzip, deflate, br
       -- 浏览器告诉服务器，浏览器所能接受的压缩文件类型。
    Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
       -- 浏览器告诉服务器，浏览器所能支持的语言种类，及权重。
    Cookie: Webstorm-9af2238=09820128-3adb-43e4-8242-a6f65c9e523a
       -- Webstorm给你种下的cookie
## 空行

## 请求报文体
    GET请求没有报文体

