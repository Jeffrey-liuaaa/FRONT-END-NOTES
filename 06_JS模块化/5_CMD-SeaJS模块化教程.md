## sea.js简单使用教程
### 1. 下载sea.js, 并引入

  * 官网: http://seajs.org/
  * github : https://github.com/seajs/seajs
  * 将sea.js导入项目: js/libs/sea.js 
### 2. 创建项目结构

  ```
  |-js
    |-libs
      |-sea.js
    |-modules
      |-module1.js
      |-module2.js
      |-module3.js
      |-module4.js
      |-main.js
  |-index.html
  ```
### 3. 定义sea.js的模块代码

  * module1.js （没有依赖）
    ```js
    define(function (require,exports,module) {
      var name = 'module1';
    
      function fun1() {
        console.log(name);
      }
    
      //暴露模块
      exports.showName = fun1
    });
    ```
  * module2.js  （没有依赖）
    ```js
    define(function (require,exports,module) {
      var name = 'module2';
    
      function fun2() {
        console.log(name);
      }
    
      //暴露模块
      module.exports = fun2
    });
    ```
  * module3.js  （没有依赖）
    ```js
    define(function (require,exports,module) {
      var name = 'module3';
    
      function fun3() {
        console.log(name);
      }
    
      //暴露模块
      module.exports = fun3
    });
    ```
  * module4.js  （有依赖）
    ```js
    //module4依赖于module2，module3
    define(function (require,exports,module) {
      var name = 'module4';
    
      function fun4() {
        console.log(name);
      }
      //同步引入module2
      let module2 = require('./module2')
      module2()
      //异步引入module3
      require.async('./module3',function (m3) {
        m3.foo()
      })
      //暴露模块
      module.exports = fun4
    });
    ```
  * main.js : 主(入口)模块
    ```js
    define(function (require) {
      var m1 = require('./module1')
      var m4 = require('./module4')
      m1()
      m4()
    })
    ```
### 4. index.html

  ```js
  <!--
  使用seajs:
    1. 引入sea.js库
    2. 如何定义导出模块 :
      define()
      exports
      module.exports
    3. 如何依赖模块:
      require()
    4. 如何使用模块:
      seajs.use()
  -->
  <script type="text/javascript" src="js/libs/sea.js"></script>
  <script type="text/javascript">
    seajs.use('./js/modules/main')
  </script>
  ```
### 5.思考：为什么运行后输出结果如下？   

```js
module2       // module2同步引入，不执行完不会继续执行后续代码
module1
module4  
module3       // module3异步引入，要等回调执行完再执行
```
