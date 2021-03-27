## CommonJS浏览器端模块化教程

### 0. 语法与CommonJS服务器端语法完全一致

### 1. 创建项目结构

  ```
  |-js
    |-dist //生成编译完js的目录
    |-src //源码所在的目录（我们编写的、没经过工具处理的代码，叫做源码）
      |-module1.js
      |-module2.js
      |-module3.js
      |-app.js
  |-index.html
  |-package.json
    {
      "name": "test-0719",
      "version": "1.0.0"
    }
  ```

### 2. 模块化编码

  * module1.js
    ```js
    module.exports = {
      foo() {
        console.log('moudle1 foo()')
      }
    }
    ```
  * module2.js
    ```js
    module.exports = function () {
      console.log('module2()')
    }
    ```
  * module3.js
    ```js
    exports.foo = function () {
      console.log('module3 foo()')
    }
    
    exports.bar = function () {
      console.log('module3 bar()')
    }
    ```
  * 下载第三方模块uniq：打开左下角的Terminal，cd到02_CommonJS-Node路径，输入命令：```npm install uniq --save```
  
  * app.js
    ```js
    //引用模块
    let module1 = require('./module1')
    let module2 = require('./module2')
    let module3 = require('./module3')
    
    let uniq = require('uniq')
    
    //使用模块
    module1.foo()
    module2()
    module3.foo()
    module3.bar()
    
    console.log(uniq([1, 3, 1, 4, 3]))
    ```

### 3. 下载browserify(用于把CommonJS的模块化语法，翻译成浏览器认识的语法，是一个“翻译官”)
  * 全局安装browserify，命令: ```npm install browserify -g```
    备注：若此步骤报错，请使用管理员身份打开webstorm，再次执行即可；或使用管理员身份打开cmd执行。

### 4. 执行处理命令
  * 第一步，cd到指定文件夹（03_CommonJS-Browserify）即：app.js所在的文件夹
  * 第二步，输入命令```browserify js/src/app.js -o js/dist/bundle.js```

### 5. 页面使用引入:
  ```js
  <script type="text/javascript" src="js/dist/bundle.js"></script> 
  ```

