## AJAX

### 1. 原生AJAX

#### 1.1 AJAX简介

​		AJAX 全称为Asynchronous Javascript And XML，就是==异步的 JS 和 XML==。通过AJAX可以在浏览器中向服务器发送异步请求，最大的优势：==无刷新获取数据== 。AJAX 不是新的编程语言，不是新的一门独立的技术，而是一种使用现有标准的新方法。

#### 1.2 XML简介

​		XML ——可扩展标记语言。

​		XML 被设计用来传输和存储数据。

​		XML和HTML类似，不同的是HTML中都是预定义标签，而XML中没有预定义标签，全都是自定义标签，用来表示一些数据。

​		现在已经被JSON取代了。

#### 1.3 AJAX的工作原理

​		Ajax的工作原理相当于在用户和服务器之间加了一个==中间层(Ajax引擎)==，使用户操作与服务器响应异步化。

#### 1.4 AJAX的特点

优点：

​		1)    可以==无需刷新==页面而与服务器端进行通信。

​		2)    允许你根据用户事件来更新部分页面内容。

缺点：

​		1)    没有浏览历史，不能回退

​		2)    存在跨域问题

​		3)    SEO不友好     （爬虫是抓网页，而使用ajax从头到尾只有一个网页）

#### 1.5 AJAX的使用

**使用原生js发送get请求  (会手写基本代码)**

```js
/*
* 1.实例化一个XMLHttpRequest对象,名为：xhr---------找来一个帮你发请求的人。
* 2.绑定一个名为onreadystatechange事件监听------和发请求的人约定好--成功了做什么，失败了做什么。
* 3.调用open方法---------用什么方法发？给谁发？带着什么过去？
* 4.调用send方法---------发送请求
* */

//1.实例化一个XMLHttpRequest对象
let xhr = new XMLHttpRequest()

//2.绑定一个名为onreadystatechange事件监听
xhr.onreadystatechange = function () {
  //xhr对象本身有5种状态：xhr“诞生”的那一刻就是0状态
  /*
  * 0:xhr对象在实例化出来的那一刻，就已经是0状态，代表着xhr是初始化状态。
  * 1:send方法还没有被调用，即：请求没有发出去，此时依然可以修改请求头。
  * 2:send方法被调用了，即：请求已经发出去了，此时已经不可以再修改请求头。
  * 3:已经回来一部分数据了，如果是比较小的数据，会在此阶段一次性接收完毕,较大数据，有待于进一步接收。
  * 4:数据完美的回来了。
  * */

  //我们几乎不会在0状态里做任何事。即：如下判断0状态，永远进不去。
  /*if(xhr.readyState === 0){
    console.log('我是一个刚出生的娃娃')
  }*/
  //1:send方法还没有被调用，即：请求没有发出去，此时依然可以修改请求头。
  /*if(xhr.readyState === 1){
    console.log('我是1状态')
    xhr.setRequestHeader('demo','123')
  }*/
  //2:send方法被调用了，即：请求已经发出去了，此时已经不可以再修改请求头。
  /*if(xhr.readyState === 2){
    console.log('我是2状态')
    xhr.setRequestHeader('demo','123')
  }*/
  //3.已经回来一部分数据了，如果是比较小的数据，会在此阶段一次性接收完毕,较大数据，有待于进一步接收。
  /*if(xhr.readyState === 3){
    console.log(xhr.response)
  }*/
  //4:数据完美的回来了。
  if(xhr.readyState === 4 && xhr.status === 200){
    //如果进入此判断，意味着：请求成功了，且数据已经回来了
    console.log(xhr.response)
    let demo = document.getElementById('demo')
    demo.innerHTML = xhr.response
  }
}

//3.调用open方法---------用什么方法发？给谁发？带着什么过去？
xhr.open('get','http://localhost:3000/ajax_get?name=kobe&age=18&t='+Date.now())

//4.调用send方法---------发送请求
xhr.send()
```

**使用原生js发送post请求  (会手写基本代码)**

```js
//1.实例化一个XMLHttpRequest对象
let xhr = new XMLHttpRequest()

//2.绑定一个名为onreadystatechange事件监听
xhr.onreadystatechange = function () {
  if(xhr.readyState === 4 && xhr.status === 200){
    console.log(xhr.response)
    let demo = document.getElementById('demo')
    demo.innerHTML = xhr.response
  }
}

//3.调用open方法---------用什么方法发？给谁发？带着什么过去？
xhr.open('post','http://localhost:3000/ajax_post')

//特别注意：此处是设置post请求所特有的请求头，若不设置，服务器无法获取参数
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')

//4.调用send方法---------发送请求
xhr.send('name=kobe&age=18')
```

#### 1.6 解决IE缓存问题

问题：在一些浏览器中(IE),由于缓存机制的存在，ajax只会发送的第一次请求，剩余多次请求不会在发送给浏览器而是直接加载缓存中的数据。

解决方式：浏览器的缓存是根据url地址来记录的，所以我们只需要修改url地址即可避免缓存问题

==xhr.open("get","/testAJAX?t="+Date.now());==



### 2. jQuery中的AJAX

#### 2.1 get请求

==$.get(url, [data], [callback], [type])==

url:请求的URL地址。

data:请求携带的参数。(写成对象格式)

callback:载入成功时回调函数。 (data) => {}

type:设置返回内容格式，xml, html, script, json, text, _default。

#### 2.2 post请求

==$.post(url, [data], [callback], [type])==

url:请求的URL地址。

data:请求携带的参数。

callback:载入成功时回调函数。

type:设置返回内容格式，xml, html, script, json, text, _default。