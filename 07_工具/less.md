### less

​	less是一种动态样式语言，属于css预处理器的范畴，它扩展了 CSS 语言，
​	增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展
​	LESS 既可以在 客户端 上运行 ，也可以借助Node.js在服务端运行。

	less的中文官网：http://lesscss.cn/

### less初次使用：
   1.定义变量（@zero:0）并运用，凡是页面中使用0，都用@zero代替;
   2.子元素需要放在父元素中，此时子元素可以放心使用class，因为他已经有前提条件是父元素
   			不用再继续担心对同名class值样式的影响

```HTML
 <style type="text/less">
```

     		3.  style标签的类型需要改成less
     		4.  根据官网我们需要一个less编译的	less.js 文件，并在最下方引入，
            因为需要读取页面中所有less相关的文件，才可以进行编译

   	less --- 支持原生js,node
   	sass --- ruby环境
   	stylus --- node -- 开发项目中我们使用stylus

### Less编译工具

​	koala 官网:www.koala-app.com 
​	

### less中的注释

​    单行注释：以//开头的注释，不会被编译到css文件中
​    多行注释：以/**/包裹的注释会被编译到css文件中 
​	

### less中的变量

使用@来声明一个变量：@pink：pink;
​   1. 作为普通属性值来使用：直接使用@pink

2. 作为选择器和属性名：#@{selector的值}的选择器形式, @{selector的值}属性名
3.  作为URL：@url

4. 在其他位置使用变量

​		语法：@{变量名}

 5. 变量引用变量

    语法：@@变量名

	6. 将其他属性作为变量使用

    语法：$属性名

7. 变量的延迟加载：

```HTML
	*  先找子元素，如果子元素中有两个或者多个相同变量，我们默认拿最后一个
	*  在找父元素，把子元素东西排除掉,如果没有，向上一层去找
	*  如果自身没有，就会往外找 无论在那一层找 都是使用这一层的最后一个
```

```less
@var: 0;
.class {
	@var: 1;
    .brass {
      @var: 2;
      three: @var;   // 3
      @var: 3;
    }
  	one: @var;        // 1
}
```



### less中的嵌套规则
​	1.基本嵌套规则

​		 在使用嵌套的时候 ，要注意合理的嵌套；一旦发现有定义比较<font color="red">特殊的class 或者id值</font>等情况，就可以单独拿出来写

​	2.&的使用

​		&代表当前元素，也可以说成是，<font color="red">前边所有祖先选择器的集合</font>；

​		所有与伪元素、伪类选择器相关的 一般情况下都搭配&，如 &:hover

### less加减乘除运算

​	less可以进行加减乘除运算，使用时要注意运算符左右必须带空格。

```less
/*是在less文件里写*/
@width:10px + 5;
div {
/*其实就变成了15px的边框*/
	border:@width solid skyblue;
}
/*生成的css文件是这样的*/
div {
	border:15px solid skyblue;
}
/*甚至还可以带小括号，比如说下面这种 和数学中的一样，先算小括号再去相乘*/
width:(@width + 5) * 2;

```

### less扩展 :extend()

通过extend() 可以使用其他样式来扩展当前样式

```less
// 源码
.box1{
    width: 100px;
    height: 100px;
}
.box2{
    &:extend(.box1);
}

// 编译后
.box1,
.box2{
    width: 100px;
    height: 100px;
}
```



### less中的混合 Mixin

​	混合就是将一系列属性从一个规则集引入到另一个规则集的方式。

​	mixin的作用：将一些代码集成到一个混合器中，提高代码重用的能力。

​	1.普通混合 
​	2.带参数的混合
​	3.带参数并且有默认值的混合
​	4.带多个参数的混合

​	

```less
// 商品列表布局
//设置Mixin
.hideBox(@box,@num,@w,@h,@mr){
//  @box  父容器选择器
//  @num  每行的列数   商品个数
//  @w    商品容器宽度
//  @h    商品容器高度
//  @mr   商品容器右边距
//<div class="box">
//  <div class="hideBox">
//    <div class="item"></div>
//    <div class="item"></div>
//    <div class="item"></div>
//    <div class="item"></div>
//  </div>
//</div>
  .@{box}{
    width: (@w * @num) + ( @num - 1) * @mr;
    border: 1px solid #000;
    margin: 0 auto;
    overflow: hidden;
    .hideBox{
      width: (@w + @mr) * @num;
      .item{
        width: @w;
        height: @h;
        margin-right: @mr;
        margin-bottom: 30px;
        background: pink;
        float: left;
      }
    }
  }
}

.hideBox(@box:inner,@num:4,@w:200px,@h:300px,@mr:50px);
```


​		     

### less中引入外部文件 @import

```less
//引入外部less文件
@import "mixins/mixin.less";
```

