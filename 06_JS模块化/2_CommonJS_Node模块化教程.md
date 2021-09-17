## CommonJS服务端模块化教程(Node.js模块化教程)

### 0. 基本语法

```
CommonJS是唯一的双端模块化规范
在服务器端：模块的加载是运行时同步加载的
在浏览器端：模块需要提前编译打包处理（异步加载）

暴露模块：
	- module.exports = value
	- exports.xxx = value
	
引入模块：
	- require(xxx)
		- 若引入的是第三方模块，则xxx为文件名
		- 若引入的是自定义模块，则xxx为模块文件路径，必须写'./'
```



### 1. 安装Node.js

### 2. 创建项目结构
  ```
  |-modules
    |-module1.js
    |-module2.js
    |-module3.js
  |-app.js
  |-package.json
    {
      "name": "test-0719",
      "version": "1.0.0"
    }
  ```
### 3. 模块化编码：
  * module1.js
    ```js
    module.exports = {
      data:'module1',
      foo(){
        console.log('foo()------',this.data);
      },
      bar(){
        console.log('bar()------',this.data);
      }
    }
    ```
  * module2.js
    ```js
    module.exports = function () {
      console.log('module2');
    }
    ```
  * module3.js
    ```js
    exports.foo = function () {
      console.log('foo()  module3');
    }
    
    exports.bar = function () {
      console.log('bar()  module3');
    }
    ```
  * 下载第三方模块uniq：打开左下角的Terminal，cd到02_CommonJS-Node路径，输入命令：```npm install uniq```

  * app.js 
    ```js
    let module1 = require('./modules/module1')
    let module2 = require('./modules/module2')
    let module3 = require('./modules/module3')
    let a = require('uniq')
    
    module1.foo()
    module1.bar()
    module2()
    module3.foo()
    module3.bar() 
    
    let arr = [1,11,2,2,2,5,5,5,3,4,6,6,9,7,8]
    console.log(a(arr));
      
    ```
### 4. 在node环境下运行app.js的两种方法(任选其一)：
  * 第一种方法：用命令启动: ```node app.js```

  * 第二种方法：用工具启动: 右键 --> Run 'xxxxx.js'

    

### 5. CommonJs模块化内置关系

​		暴露的本质是exports对象，更准确的说是module.exports所指向的那个对象。

​		注意：在CommonJs模块规范中，module.exports和exports.xxx不能混用，如果混用，**以module.exports为主**。

<img src="C:\Users\abc\AppData\Roaming\Typora\typora-user-images\image-20210315093856718.png" alt="image-20210315093856718" style="zoom:80%;" />