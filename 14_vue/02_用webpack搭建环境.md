## 1. 初始化项目

```js
1). 生成package.json
    yarn init -y

2). 创建入口js: src/index.js
    console.log('Hello Webpack!')
    document.getElementById('root').innerHTML = '<h1>Hello222</h1>'

3). 创建页面文件: index.html
    <div id="root"></div>
```

## 2. webpack基本使用

```js
1). 下载依赖包
    yarn add -D webpack webpack-cli // webpack用来编译打包 webpack-cli用来提供webpack命令
    yarn add -D html-webpack-plugin // 打包html，自动引入打包后的js/css

2). 创建webpack配置: webpack.config.js
    const path = require('path')
    const HtmlWebpackPlugin = require('html-webpack-plugin')

    module.exports = {
      // 模式: 生产环境
      mode: 'production',
      // 入口
      entry: {
        app: path.resolve(__dirname, 'src/index.js')
      },
      // 出口(打包生成js)
      output: {
        filename: 'static/js/[name].bundle.js',
        path: path.resolve(__dirname, 'dist')
      },
      // 模块加载器
      module: {
        rules: [

        ]
      },
      // 插件
      plugins: [
        new HtmlWebpackPlugin({
          template: 'index.html',
          filename: 'index.html'
        })
      ]
    }

3). 生成环境打包并运行
    在package.json中配置打包命令:  "build": "webpack --mode production"
    打包项目: yarn build
    运行打包项目: serve dist  // 前提是要先下载server包
```

## 3. 开发环境运行

```js
1). 现在的问题:
    每次修改项目代码后, 必须重新打包, 重新运行

2). 下载依赖包
    yarn add -D webpack-dev-server  // 自动打包运行，在浏览器显示运行结果

3). 配置开发服务器
    devServer: {
      port: 8080,
      open: true, // 自动打开浏览器
      //quiet: true, // 不做太多日志输出
    },

4). 配置开启source-map调试
    devtool: 'cheap-module-eval-source-map',

5). 开发环境运行
    在package.json中配置命令: "dev": "webpack-dev-server --mode development"
    执行命令: yarn dev
```

## 4. 打包处理 ES6/CSS/图片

```js
1). 处理ES6 -> ES5
    a. 下载依赖包
        yarn add -D babel-loader @babel/core @babel/preset-env
    b. 配置
        {
          test: /\.js$/,  // 用于匹配文件
          //exclude: /(node_modules|bower_components)/,  // 排除文件
          include: path.resolve(__dirname, 'src'), // 只针对哪些处理
          use: {
            loader: 'babel-loader',
            options: {
              presets: ['@babel/preset-env']
            }
          }
        }

2). 处理CSS
    a. 下载依赖包
        yarn add -D css-loader style-loader
    b. 配置
        {
          test: /\.css$/,
          use: ['style-loader', 'css-loader'], // 多个loader从右到左处理
        }

3). 处理图片
    a. 下载依赖包
        yarn add -D url-loader@2.3.0 file-loader@4.3.0
    b. 配置
        {
          test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
          loader: 'url-loader',
          options: {
            limit: 8192,
            name: 'static/img/[name].[hash:7].[ext]' // 相对于output.path
          }
        }
4). 测试
    a. 添加图片: src/assets/imgs/logo.png
    b. 添加css: src/assets/css/my.css
        img {
          width: 200px;
          height: 200px;
        }
    c. index.js
        import logo from './assets/imgs/logo.png'
        import  './assets/css/my.css'

        const image = new Image()
        image.src = logo
        document.body.appendChild(image)
        document.getElementById('root').innerHTML = '<h1>Hello222</h1>'
```

## 5. 搭建vue的环境

```js
0). 文档:
    https://vue-loader.vuejs.org/zh/

1). 下载依赖包:
    yarn add vue
    yarn add -D vue-loader vue-template-compiler

2). 配置
    const VueLoaderPlugin = require('vue-loader/lib/plugin')

    {
      test: /\.vue$/,  
      include: path.resolve(__dirname, 'src'),
      loader: 'vue-loader'
    }

    {
      test: /\.css$/,
      use: ['vue-style-loader', 'css-loader'], // vue-style-loader替换style-loader
    }

    // plugins下添加
    new VueLoaderPlugin()

    // 配置引入模块的解析
    resolve: {
      extensions: ['.js', '.vue', '.json'], // 可以省略的后缀名
      alias: { // 路径别名(简写方式)
         // 表示精准匹配 import Vue from 'vue'相当于vue/dist/vue.esm.js'，带vue编译器
        'vue$': 'vue/dist/vue.esm.js',  
      }
    }

3). 编码: 
    src/App.vue
    src/index.js
```

## 区分使用生产环境与开发环境

```js
使用生产环境:
    npm run build   ==> webpack
    1). 在内存中进行编译打包, 生成内存中的打包文件
    2). 保存到本地(在本地生成打包文件)   ===> 此时还不能通过浏览器来访问, 需要手动启动服务器运行
使用开发环境
    npm run dev   ==> webpack-dev-server
    1). 在内存中进行编译打包, 生成内存中的打包文件
    2). 启动服务器, 运行内存中的打包文件(不生成本地打包文件)   ===> 可以通过浏览器虚拟路径访问
```

## 6. 解决开发环境ajax请求跨域问题

```js
1). 利用webpack-dev-server进行请求代理转发
    webpack-dev-server内部利用http-proxy-middle包对特定请求进行转发操作
2). 配置:
    devServer: {
      proxy: {
        // 处理以/api开头路径的请求
        // '/api': 'http://localhost:4000'
        '/api': {
          target: 'http://localhost:4000', // 转发的目标地址
          pathRewrite: {
            '^/api' : ''  // 转发请求时去除路径前面的/api
          },
          changeOrigin: true, // 支持跨域
        }
      }
    }
```

## 7. 配置async/await的编译环境

```js
1). 下载包
    yarn add @babel/runtime-corejs2
2). 配置
    presets: [
      ['@babel/preset-env', {
        useBuiltIns: 'usage',
        'corejs': 2 // 处理一些新语法的实现
      }]
    ]
```

## 8. 解决mint-ui按需引入配置异常的问题

```js
1). 文档上的配置
        "plugins": [
          ["component", [
            {
              "libraryName": "mint-ui",
              "style": true
            }
          ]]
        ]
2). 异常信息:  
    Error: .plugins[0][1] must be an object, false, or undefined
3). 原因:
    文档编写时, 是根据老的babel版本编写的, 新版本的babel配置有变化
    以前是数组, 现在只能是对象
4). 修正:
    "plugins": [
      ["component", {
          "libraryName": "mint-ui",
          "style": true
      }]
    ]
```

## 9.解决history模式路由请求404的问题

```js
 devServer: historyApiFallback: true, // 任意的 404 响应都被替代为 index.html
 output: publicPath: '/', // 引入打包的文件时路径以/开头
```

