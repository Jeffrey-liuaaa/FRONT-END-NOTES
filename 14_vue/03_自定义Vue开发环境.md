# 自定义Vue开发环境
## 1. 搭建基本开发环境
```js
1). 下载依赖包
    yarn add -D webpack webpack-cli
    yarn add -D html-webpack-plugin
    yarn add -D webpack-dev-server
    yarn add -D babel-loader @babel/core @babel/preset-env
    yarn add -D css-loader style-loader
    yarn add -D url-loader@2.3.0 file-loader@4.3.0

2). webpack的基本配置: webpack.config.js
    module.exports = {
      mode: 'production|development'
      entry: {

      },
      output: {

      },
      module: {
        rules: [
            {
              test: /\.vue$/,  
              include: path.resolve(__dirname, 'src'),
              loader: 'vue-loader'
            }

            {
              test: /\.css$/,
              use: ['vue-style-loader', 'css-loader'], // vue-style-loader替换style-loader
            }

        ]
      },
      plugins: [
			new VueLoaderPlugin()
      ],
      devServer: {

      },
      devtool: ''，
      // 配置引入模块的解析
      resolve: {
          extensions: ['.js', '.vue', '.json'], // 可以省略的后缀名
          alias: { // 路径别名(简写方式)
             // 表示精准匹配 import Vue from 'vue'相当于vue/dist/vue.esm.js'，带vue编译器
            'vue$': 'vue/dist/vue.esm.js',  
          }
      }
    }

3). 区分使用生产环境与开发环境
    使用生产环境:
        npm run build   ==> webpack
        1). 在内存中进行编译打包, 生成内存中的打包文件
        2). 保存到本地(在本地生成打包文件)   ===> 此时还不能通过浏览器来访问, 需要手动启动服务器运行
    使用开发环境
        npm run dev   ==> webpack-dev-server
        1). 在内存中进行编译打包, 生成内存中的打包文件
        2). 启动服务器, 运行内存中的打包文件(不生成本地打包文件)   ===> 可以通过浏览器虚拟路径访问
```

## 2. 搭建Vue的开发环境
```js
1). 配置处理.Vue组件文件的loader和plugin
2). 配置使用vue-style-loader替换style-loader
3). 解决无法编译vue模板的错误
    原因: 默认引入的vue是不带编译器的版本, 无法对template配置指定模板进行编译
    解决: 配置模块别名来指定引入vue带编译器的版本
4). 配置省略模块后缀名(.js/.vue/.json)
```

