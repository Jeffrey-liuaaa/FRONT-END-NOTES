# 1. Vue.js是什么?
```js
1). 一位华裔前Google工程师(尤雨溪)开发的前端js库
2). 作用: 动态构建用户界面
3). 特点:
	* 遵循MVVM模式
	* 编码简洁, 体积小, 运行效率高, 移动/PC端开发
	* 它本身只关注UI, 可以轻松引入vue插件和其它第三库开发项目
4). 与其它框架的关联:
	* 借鉴angular的模板和数据绑定技术
	* 借鉴react的组件化和虚拟DOM技术
5). vue包含一系列的扩展插件(库):
	* vue-cli: vue脚手架
	* vue-resource(axios): ajax请求
	* vue-router: 路由
	* vuex: 状态管理
	* vue-lazyload: 图片懒加载
	* vue-scroller: 页面滑动相关sscv
	* mint-ui: 基于vue的组件库(移动端)
	* element-ui: 基于vue的组件库(PC端)
```

# 2. 基本使用
```js
1). 引入vue.js
2). 创建Vue实例对象(vm), 指定选项(配置)对象
		el: 指定dom标签容器的选择器
		data: 指定初始化状态数据的对象/函数(返回一个对象)
3). 在页面模板中使用{{}}或vue指令
4). MVVM模式
		M: Model(模型), vue中是data(为view提供数据)
		V: View(视图), vue中是模板页面(显示data中的数据)
		VM: ViewModel(视图模型), vue中是Vue实例对象(管理者: 数据绑定/DOM监听) 
```

# 3. Vue对象的选项
## 1). el
```js
指定dom标签容器的选择器
Vue就会管理对应的标签及其子标签
也可以通过$mount()来处理
```

## 2). data
```js
对象或函数类型
指定初始化状态属性数据的对象
vm也会自动拥有data中所有属性
页面中可以直接访问使用
数据代理: 由vm对象来代理对data中所有属性的操作(读/写)
data数据监视的特点:
		1. vue会监视data中所有层次的属性
		2. 对象中的属性数据通过添加set方法来实现监视
		3. 数组中的元素也实现了监视: 重写数组一系列更新元素的方法
				1). 调用原生对应的方法对元素进行处理
				2). 去更新界面
```

## 3). methods
```js
包含多个方法的对象
供页面中的事件指令来绑定回调
回调函数默认有event参数, 但也可以指定自己的参数
所有的方法由vue对象来调用, 访问data中的属性直接使用this.xxx
```

## 4). computed
```js
包含多个计算属性的对象
根据已有属性进行计算返回一个新的数据, 供页面获取显示
如果同时还需要监视计算属性的变化, 需要使用getter/setter
计算属性有缓存, 内部使用对象容器缓存, 可以减少计算的次数
如何给对象定义get/set属性
		对象创建之后指定: Object.defineProperty(obj, age, {get(){}, set(value){}})
		在创建对象时指定: get objName() {return xxx} / set objName(value) {}
弄清楚回调函数的3个问题?
		什么时候回调执行?
		它的作用是什么?
		函数中的this是谁?
```

## 5). watch
```js
包含多个属性监视的对象
分为一般监视和深度监视
		'xxx.yyy': function (value) {},
		'xxx' : {
			deep : true,
			handler : fun(value)
		}
另一种添加监视方式: vm.$watch('xxx', fun)
```

# 4. 过渡动画
```js
利用vue去操控css的transition/animation动画
模板: 使用<transition name='xxx'>包含带动画的标签
css样式
	.fade-enter-active: 进入过程, 指定进入的transition
	.fade-leave-active: 离开过程, 指定离开的transition
	.xxx-enter, .xxx-leave-to: 指定隐藏的样式
编码例子
    .xxx-enter-active, .xxx-leave-active {
      transition: opacity .5s
    }
    .xxx-enter, .xxx-leave-to {
      opacity: 0
    }
    
    <transition name="xxx">
      <p v-if="show">hello</p>
    </transition>
```

# 5. 生命周期
	vm/组件对象
	生命周期图
	主要的生命周期函数(钩子)
		created() / mounted(): 启动异步任务(启动定时器,发送ajax请求, 绑定监听)
		beforeDestroy(): 做一些收尾的工作

![img](https://user-gold-cdn.xitu.io/2019/8/19/16ca74f183827f46?imageslim)

# 6. 自定义过滤器

## 1). 理解
	对需要显示的数据进行格式化后再显示

## 2). 编码
```js
1). 定义过滤器
	Vue.filter(filterName, function(value[,arg1,arg2,...]){
	  // 进行一定的数据处理
	  return newValue
	})
2). 使用过滤器
	<div>{{myData | filterName}}</div>
	<div>{{myData | filterName(arg)}}</div>
```

# 7. vue内置指令
```js
v-text/v-html: 指定标签体
	* v-text : 当作纯文本
	* v-html : 将value作为html标签来解析
v-if v-else v-show: 显示/隐藏元素
	* v-if : 如果vlaue为true, 当前标签会输出在页面中
	* v-else : 与v-if一起使用, 如果value为false, 将当前标签输出到页面中
	* v-show: 就会在标签中添加display样式, 如果vlaue为true, display=block, 否则是none
v-for : 遍历
	* 遍历数组 : v-for="(person, index) in persons"  :key="person.id" 
	* 遍历对象 : v-for="value in person"  $key
v-on : 绑定事件监听
	* v-on:事件名, 可以缩写为: @事件名
	* 监视具体的按键: @keyup.keyCode   @keyup.enter
	* 停止事件的冒泡和阻止事件默认行为: @click.stop   @click.prevent
	* 隐含对象: $event
v-bind : 强制绑定解析表达式  
	* html标签属性是不支持表达式的, 就可以使用v-bind
	* 可以缩写为:  :id='name'
	* :class
	  * :class="a"  // 类名可变 
		* :class="{classA : isA, classB : isB}"  // 类名确定，但不确定有没有
	* :style
		:style="{color}"
v-model
	* 双向数据绑定
	* 自动收集用户输入数据
ref : 标识某个标签
	* ref='xxx'
	* 读取得到标签对象: this.$refs.xxx
```

# 8. 自定义指令
## 1). 注册全局指令
```js
Vue.directive('my-directive', function(el, binding){
  el.innerHTML = binding.value.toUpperCase()
})
```

## 2). 注册局部指令
```js
directives : {
  'my-directive' : function(el, binding) {
      el.innerHTML = binding.value.toUpperCase()
  }
}
```

## 3). 使用指令
```js
<div v-my-directive='xxx'>
```
