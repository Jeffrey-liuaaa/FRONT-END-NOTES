## 1. vue-router
    是用来实现SPA的vue插件

## 2. vue-router的基本使用
```js
1). 创建路由器: router/index.js
    new VueRouter({
      mode: 'hash/history'
      routes: [
        { // 一般路由
          path: '/about',
          component: About
        },
        { // 自动跳转路由
          path: '/',
          redirect: '/about'
        }
      ]
    })
2). 注册路由器: main.js
    import router from './router'
    new Vue({
      router
    })
3). 使用路由组件标签:
	// 路由链接
    <router-link to="/xxx">Go to XXX</router-link>  // 可以不使用
	// 显示当前路由组件界面
    <router-view></router-view>  // 必须使用
4). 2个对象
    $router: 代表路由器对象, 包含一些实现路由跳转/导航的方法: push()/replace()/back()
    $route: 代表当前路由对象, 包含一些路由相关的属性: path/params/query/meta
```

## 3. 编写路由的3步
```js
1). 定义路由组件
2). 映射路由
3). 使用<router-view/>显示当前路由组件
```

## 4. 嵌套路由
```js
children: [
    {
      path: '/home/news/:id/:title',
      component: news
    },
    {
      path: 'message',
      component: message
    }
]
```

## 4. 向路由组件传递数据
```js
方式一：路由路径携带参数(params/query)
<router-link :to="`/home/news/${m.id}`">{{m.title}}</router-link>
路由组件中读取请求参数：this.$route.params.id
方式二：<router-view>属性携带数据
变相props: <router-view :msg='msg'></router-view>
```

## 5. 动态路由与路由别名
```js
注册路由: 
    {
        name: 'news'
        path: '/home/news/:id/:title',
        component: News
    }
跳转: 
    <router-link :to="{name: 'news', params: {id: 1, title: 'abc'}}">
    router.push({name: 'news', params: {id: 1, title: 'abc'}})


:id 动态路径参数
情景：使用了动态路径参数的路由组件下点击路由链接，数据不会改变
原因：路由组件对象是在第一次请求对应路径时才创建
     从一个路由组件离开, 路由组件死亡, 再进入需要重新创建
     当在同一个路由路径上做切换(只是改了参数), 当前路由组件对象被直接复用
     同一个组件对象mounted()只执行一次
解决：监视$route对象的变化
	动态路由的监视：
	watch: {
      '$route' (to, from) { // 当请求参数发生改变时, 内部指定了新的$route属性
        // 对路由变化作出响应...
        setTimeout(() => {
          // 得到当前新的id
          const id = to.params.id * 1
          const detail = allMessageDetils.find(detail => detail.id===id)
          this.detail = detail
        }, 1000);
      }
    }
```

## 6. 缓存路由组件
```js
路由组件对象默认的生命周期: 被切换时就会死亡, 切换回来时重新创建
<keep-alive exlude="A,B">
  <router-view></router-view>
</keep-alive>
```

## 7. 路由的编程式导航
```js
this.$router.push(path): 相当于点击路由链接(可以返回到当前路由界面)
this.$router.replace(path): 用新路由替换当前路由(不可以返回到当前路由界面)
this.$router.back(): 请求(返回)上一个记录路由
```

## 8. 路由的2种模式比较, 解决history模式404问题
```js
hash模式:
    路径中带#: http://localhost:8080/#/home/news
    发请求的路径: http://localhost:8080  项目根路径
    响应: 返回的总是index页面  ==> path部分(/home/news)被解析为前台路由路径

history模式:
    路径中不带#: http://localhost:8080/home/news
    发请求的路径: http://localhost:8080/home/news
    响应: 404错误
    希望: 如果没有对应的资源, 返回index页面, path部分(/home/news)被解析为前台路由路径
    解决: 添加配置
        devServer: historyApiFallback: true, // 任意的 404 响应都被替代为 index.html
        output: publicPath: '/', // 引入打包的文件时路径以/开头
        // 原本的引入路径为'./static/css/base.css'，这时会从'http://localhost:8080/home'
	    // 路径下开始找，所以会报错，去掉'.'就会从项目的根路径'http://localhost:8080'下找
```

