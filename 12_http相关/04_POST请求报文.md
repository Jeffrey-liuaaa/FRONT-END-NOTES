# POST请求报文（给服务器看的）-- 通过form表单发送的POST请求

    POST http://localhost:3000/ HTTP/1.1
    Host: localhost:3000
    Connection: keep-alive
    Content-Length: 22
    Pragma: no-cache
    Cache-Control: no-cache
    Origin: http://localhost:63347
    Upgrade-Insecure-Requests: 1
    DNT: 1
    Content-Type: application/x-www-form-urlencoded
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
    Referer: http://localhost:63347/0719_node/day04/5.http%E6%8A%A5%E6%96%87&%E7%8A%B6%E6%80%81%E7%A0%81/%E6%BC%94%E7%A4%BA%E9%98%B2%E7%9B%97%E9%93%BE.html?_ijt=v73gogoe0uaatcie38ma6l7gso
    Accept-Encoding: gzip, deflate, br
    Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
    Cookie: Webstorm-9af2238=09820128-3adb-43e4-8242-a6f65c9e523a
    空行
    name=kobe&password=123
## 请求报文首行
     POST http://localhost:3000/ HTTP/1.1
## 请求报文头
    Host: localhost:3000
    Connection: keep-alive
    【Content-Length: 22】
        -- 发送数据的长度
    Pragma: no-cache
    Cache-Control: no-cache
    【Origin: http://localhost:63347】
        -- 精简版的Referer  1.防盗链。 2.广告计费
    Upgrade-Insecure-Requests: 1
    DNT: 1
    【Content-Type: application/x-www-form-urlencoded】
        --浏览器告诉服务器，发送数据的类型
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36
    Accept:	text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,
    application/signed-exchange;v=b3
    Referer: http://localhost:63347/0719_node/demo.html?_ijt=r08g7l67qsmghv05cf7mphidka
        -- “站”在哪里发出去的请求(源站)  1.防盗链。 2.广告计费
    Accept-Encoding: gzip, deflate, br
    Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
    Cookie: Webstorm-9af2238=09820128-3adb-43e4-8242-a6f65c9e523a
## 空行
    空行
## 请求报文体
    name=kobe&password=123


​    
### 备注：
    1.form表单的 post请求和get请求 参数均以urlencoded形式进行编码
    2.get请求将urlencoded编码的参数放入请求地址携带给服务器，所以称之为：查询字符串参数。
    3.post请求将urlencoded编码的参数放入请求体，所以称之为：请求体参数。
