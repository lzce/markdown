

# Vue 第一天

## 什么是VueJs

**渐进式javascript框架**

**渐进式: 逐渐增强, 可以在项目中使用vue的一部分功能, 也可以使用vue的全家桶开发整个个项目**

**angular: 强主张, 一旦用了, 整个项目必须使用angular的全部功能**

- Vue.js 是目前最火的一个前端框架，React是最流行的一个前端框架（React除了开发网站，还可以开发手机App， Vue语法也是可以用于进行手机App开发的，需要借助于Weex）
- Vue.js 是前端的**主流框架之一**，和Angular.js、React.js 一起，并成为前端三大主流框架！
- Vue.js 是一套构建用户界面的框架，**只关注视图层**，它不仅易于上手，还便于与第三方库或既有项目整合。（Vue有配套的第三方类库，可以整合起来做大型项目的开发）

### 文档网站

1. [vue.js 1.x 文档](https://v1-cn.vuejs.org/)
2. [vue.js 2.x 文档](https://cn.vuejs.org/)

## 提高开发效率的发展历程

- 手写原生JS
- JQuery之类的类库
- 模板引擎(art-template)
- Angular.js / Vue.js / React.js



Vue.js框架的优点

- 减少不必要的DOM操作 , 提高渲染效率 ,
- 双向数据绑定
  - 通过框架的指令 , 前端只关心业务逻辑的处理, 不在关心DOM元素是如何渲染的

面试小提醒 : 

你平时不忙的时候 , 都在干嘛 ? 

答 : 没事的时候 , 会逛逛社区 , 看看前端相关的书籍 , 展现自己的学期能力



## 框架和库的区别 (frameWork and library)

**框架 :** 

是一套完整的解决方案 , 框架帮我们完成了大部分功能, 我们只需要在框架中完成部分功能

对项目的侵入性 较大, 项目如需更换框架 , 则需要重新构建整个项目 , 代价很大

PS  : node 中的 Express



**库 :  一系列函数的集合, 就是一个工具箱,提供了很多方法**

只是提供了一个小功能 , 项目中的插件 , 对项目的侵入性较小 , 如果某个库(插件) 如果满足我们的需求,可以很容易切换到其他库实现需求

- 从 JQuery 切换到 Zepto
- 从 EJS 切换到 art-template



## 后端(node)中的 MVC  和前端中的 MVVM 之间的区别

MVC 是后端分层开发的概念

M 就是 Model 层 ,  V 就是视图层View ,  C 就是 路由 和 controller

![](image\01.MVC和MVVM的关系图解.png)

### MVVM

![](image\MVVM.png)

- MVVM，一种软件架构模式，决定了写代码的方式。
  + M：model数据模型(ajax获取到的数据)	
  + V：view视图（页面）
  + VM：ViewModel 视图模型

- MVVM通过`数据双向绑定`让数据自动地双向同步  **不在需要操作DOM**
  - V（修改视图） -> M（数据自动同步）
  - M（修改数据） -> V（视图自动同步

**Model 、 View、VM  (ViewModel)**

**VM是`M `和`V `之间的调度者**

**M : 在发AJax请求 ,  M保存服务端响应的数据**

**VM : 是一个调度者 , M中的数据渲染到 V 中 ,** **位于 V 和 M中间 , 每当V想要	获取数据或者保存数据到 M 中都需要VM作为以一个中间者**

**V: 就是视图, 通过得到的数据展示的页面**

### Vue中的MVVM

虽然没有完全遵循 MVVM 模型，Vue 的设计无疑受到了它的启发。因此在文档中经常会使用 vm (ViewModel 的简称) 这个变量名表示 Vue 实例

注意：

**1. 在vue中，不推荐直接手动操作DOM！！！** 

**2. 在vue中，通过数据驱动视图，不要在想着怎么操作DOM，而是想着如何操作数据！！**

![](image/双向数据绑定.png)



## Vue起步

> 通过 Vue 提供的指令，很方便的就能把数据渲染到页面上，程序员不再手动操作DOM元素了【前端的Vue之类的框架，不提倡我们去手动操作DOM元素了】

在项目中引入`Vue` 的JS文件

当我们导入这个包之后 , window身上就多了一个 `Vue`  这个构造函数

```js
<script src="./lib/vue-2.4.0.js" ></script>
```



**创建Vue实例**

 `el` : 表示，当前我们 new 的这个 Vue 实例，要控制页面上的哪个区域

`data` : 这里的 data 就是 MVVM中的 M，专门用来保存 每个页面的数据的

> */ 注意：在 VM实例中，如果想要获取 data 上的数据，或者 想要调用 methods 中的 方法，必须通过 this.数据属性名  或  this.方法名 来进行访问，这里的this，就表示 我们 new 出来的  VM 实例对象*/

```javascript
 <div id="app">
    <p>{{ content }}</p> #====================这里就是 MVVM 中的 V
  </div>

  <script src="./lib/vue-2.4.0.js"></script>

  <script>
    var vm = new Vue({ //=================VM 就是 MVVM中的 VM
      el: '#app', 
      data: {
        content: 'vue初体验' //========================MVVM 中 M
      }
    })
  </script>
```

### 插值表达式

也叫mustache语法, 小胡子语法

**作用:** 可以显示data中的数据到视图中

插值表达式中允许出现表达式, 可以使用三元表达式, 也可以调用方法(字符串的方法等)

```js
<p>{{ obj.naem.toUpperCase() }}</p>
```

**注意点**

1. 在`{{}}` 中访问的数据必须在data中存在
2. `{{}}`  中不能出现JS中 关键字: if , for 等等

3. 不能再标签的属性中使用, 只能出现在标签的内部, 需要在属性中使用data, 可以使用`v-bind` 属性绑定



## vue基础指令 directives

### 什么是指令

vue 给我们的html的标签新增加了很多自定义属性。特点: 都是以 `v-` 开头

vue的指令用来标签的属性中, 在标签里用插值表达式

**vue一共提供了14个指令, 每一指令都有特殊的能力**



### v-bind : 绑定属性

 能够让标签属性的值变成一个变量, **`绑定属性的`**

`v-bind`可以简写 在属性前写 `:`  = `v-bind:`

v-bind绑定的属性的值必须在data定义

```js
 <input type="text" v-bind:value="msg"> 
 <input type="text" :value="msg + '我是拼接的'"> 
  var vm3 = new Vue({
      el:'input',
      data: {
        msg: '我是内容'
      }
    })
```



###  v-model 双向数据绑定

#### v-model使用

**只能应用于表单元素**

`v-bind` 是能实现数据的单向绑定, 从`vm` 绑定到 页面中 , 无法从页面中 绑定到 `vm` 中

所谓双向数据绑定, 就是在某一方的数据发生改变, 另一方的数据也随之改变

在表单元素中 , 表单中的值发生改变 , `VM` 的 `data中msg` 并不会改变

**注意点:**

`v-model` 只能运用在表单元素中, 对于其他元素`div` 等, 没有交互性, 所以不能使用`v-model`.

表单元素使用了`v-model` 之后, 会忽略原来的`value` 值

```html
 <div>
     <!--h3中的值 会随着表单中的值得改变而改变-->
    <h3>{{ msg }}</h3>
    <input type="text" v-bind:value="msg" v-model="msg" style="width: 300px">
 </div>

	var vm = new Vue({
      el: 'div',
      data: {
        msg: '我是v-model, 我支持双向数据绑定'
      },
    })
```



#### **什么双向数据绑定**

- view视图改变 数据model变

- model改变 view变

通过`vm.$data` 能够访问vm实例中的data属性, 但是`vue` 不推荐我们修改`$data` 

vue为了我们能够访问操作data中的数据, 会把`data` 上的属性绑定到 vm 实例上

**单向数据绑定**

- 数据变, 视图跟着变, 所有元素都有单向数据绑定的能力

#### 双向数据绑定原理 (面试)

**包括vm实例中data中的属性都会被劫持`Object.defineProperty()` , 所有数据变, 视图变**

1. **视图变 -> 数据变**

给表单注册事件, 事件触发改变data

可用的事件:` input change`  -> `input` 更合适

**input事件** : 文本框输入文本内容会触发 input 事件

change 事件: 文本框中内容中发生改变时才会触发, 但是只有输入完成(按enter 或 失去焦点) 时才会触发 

```js
   const input = document.querySelector('input')

    const obj = {
      name: 'taotao',
      yanzhi: 1
    }

    // 视图变 -> 数据变
    input.addEventListener('input', () => {
      obj.yanzhi = input.value
      console.log(obj.yanzhi)
    })
```



2. **数据变 -> 视图变**

难点: 如何知道对象的属性发生改变

**如何检测对象的属性发生改变**

1. 脏数据检查机制 (angular 1.x 中使用)

开定时器, 定时检测数据是否发生改变

2. **ES5 中 `Object.defineProperty() ` 数据劫持 vue2.x使用**

 `Object.defineProperty() ` 有三个参数

- param1 :  劫持的对象
- param2: 劫持的属性
- param3 : {}

```js
    const input = document.querySelector('input')
    
    const obj = {
      name: 'taotao',
      yanzhi: 1
    }

	//数据变 -> 视图变
    
    //需要定义个变量
    let temp = obj.yanzhi
    Object.defineProperty(obj, 'yanzhi', {
      //获取性的操作会进入get函数
      get() {
        return temp
        // return obj.yanzhi  不能return obj.yanzhi 否则会和 get 形成死递归
      }, 
      //设置性的操作,会进入set函数
      //value 是设置的值
      set(value) {
        temp = value
        // console.log('数据发生改变了')
        //数据发生改变 同步到页面中
        input.value = temp
      }
    })
```



3. ES6 中proxy  vue 3.x 使用  -> 数据代理





### v-on : 绑定事件

在元素身上绑定一个事件和 `el` , `data` 平级

缩写是 `@`  =  `v-on:`

**注意**

在元素中绑定事件可以加`()`  加了小括号就可以传参数了`@click='add(参数)'`

```js
<div class="box" v-on:click="show" v-html="msg" v-on:mouseenter="show"></div>

 <script>
    var vm = new Vue({
        el: '.box',
        data: {
          msg: '我是一个div'
        },
        methods: {
        show: function () {
            console.log('哈哈哈')
          }
        }
      }  
    )
```



#### 事件修饰符

- `.stop  `     **阻止冒泡**
  - 事件默认是冒泡机制 , 从里往外冒泡执行, 在元素身上添加, 就不会冒泡到父元素上

```js
<input type="button" value="戳他" @click.stop="btnHandler">
```

- `.prevent `   **阻止默认事件**
  - 对类似`a链接`的默认跳转行为, 可以用通过此修饰符阻止  

```js
<a href="http://www.baidu.com" @click.prevent="linkClick">有问题，先去百度</a>
```

- `.capture `   添加事件侦听器时使用事件捕获模式, **捕获阶段触发**
  - 事件默认是冒泡机制, 给目标事件的父元素调加这个修饰符, 就会在捕获阶段触发其身上的事件

```html
<div class="inner" @click.capture="div1Handler">
   <input type="button" value="戳他" @click="btnHandler">
</div>
```

- `.self  `     只当事件在该元素本身（比如不是子元素）触发时触发回调, **点自己才会触发**
  - 针对于通过冒泡被动触发的事件 , `.self` 能够阻止事件的触发

> 和 `.stop` 的区别, 在元素身上使用`.stop`  所有父元素的冒泡事件都不会被触发
>
> 但是`.self`  是只能阻止自己身上的被动事件的触发 

- `.once   `    **事件只触发一次**
  - 在一个元素身上注册的事件, 使用`.once` 之后, 使用一次之后, 事件就会失效, 不会在触发
- `passive` :  在移动端`onscroll` 事件中, 添加`passive` 能够提升滚动性能



- `.native` :  给第三方组件库的组件注册事件, 注册不上的时候, 加`.native`

- `.sync`      :   在 父传子的数据上 , 子组件想要修改 `props` 接收的值, 会报错,`props`不支持修改,  `:title.sync="fatherTitle"`  , `.sync` 会自动给父组件注册一个事件`update:xxx, xxx 是要修改的属性名`

  在 子组件中的事件中直接调用`this.$emit('update:title', '要修改的数据')` , 方便在于, 我们不需要自己在父组件注册事件

```js
<div id="app">
    // 父组件传数据给子组件, 子组件想要修改
    <demo :title.sync="fatherTitle"></demo>
</div>

Vue.component('demo', {
    template: `<h1>
	<button @click="fn">修改父组件的值</button>
	</h1>`,
    methods: {
        fn () {
            // 直接调用即可, 不需要在父组件上注册这个事件
            this.$emit('update:title', '这是子组件修改后的title')
        }
    }
})
```



#### 按键修饰符

- `@keyup.enter=""` 

`keyup` 和 `keydown`  一般我们使用`keyup` 因为 `keydown` 按下时会一直触发

特定`enter`键抬起的时候触发事件

**别名键盘码**

- `.enter`

- `.tab`
- `.delete`  能够监听退格 和 删除
- `esc`
- `space`
- `up`
- `down`
- `left`
- `right`

对于`Vue`没有提供的别名, 我们都可以通过`@keyup.13=""` 每个键对应的码值触发事件

```html
<input type="text" class="form-control" v-model="name" @keyup.13="add">
```

[js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)



#### 自定义键盘修饰符

**定义键盘修饰符**

`Vue.config.keyCodes.键盘别名 = 按键值` 自定义键盘修饰符

```js
Vue.config.keyCodes.f2 = 113
```

**使用自定义键盘修饰符**

```html
<input type='text' @keyup.f2="add">
```



# Vue 第二天



## Vue指令之 `v-for` 和 `key`

### `v-for` 指令

#### 遍历普通数组

用法的数组的`[].foreach()` 类似**, 重复渲染有`v-for` 指令的元素, 给要重复渲染的元素**

**语法**

> `v-for="(item[,i]) in array"`

- `item` 是要遍历的每一项
- `[i]` 是每一项的索引, 可选参数
- `array`  是要遍历的数组

```html
  <div>
    <p v-for="(item, i) in list">数组的每一项是: {{ item }} 对应的索引是: {{ i }}</p>
  </div>
  <script src="./lib/vue-2.4.0.js"></script>

  <script>
    var vm = new Vue({
      el: 'div',
      data: {
        list: ['小明', '小红', '校长'],
      },
    });
  </script>
```



#### 遍历对象数组

**语法**

> `v-for="( item,[index]") in array`

- `item`  需要遍历的每一个对象
- `[i]`  每一项的索引
- `list`  遍历的数组

```html
<div>
    <!-- <p v-for="(item, i) in list">数组的每一项是: {{ item }} 对应的索引是: {{ i }}</p> -->
    <p v-for="(user, i) in list"> 这是第{{i}}项, 姓名是{{user.name}} id是 {{user.id}}</p>
  </div>
  <script src="./lib/vue-2.4.0.js"></script>

  <script>
    var vm = new Vue({
      el: 'div',
      data: {
        // list: ['小明', '小红', '校长'],
        list: [
          {'id': 1, name: '小明'},
          {'id': 2, name: '小黑'},
          {'id': 3, name: '小花'},
          ]
      },
    });
  </script>
```





#### 遍历对象

**语法**

> `v-for="(value[, key, index]") in obj`

**参数**

- `value`  值
- `key`  键, **相对于数组来说, 键就是下标**
- `[index]`  索引
- `list`  遍历的对象

```html
  <div>
    <p v-for="(value, key, index) in list">value是{{value}}, 键是{{key}}, 还有索引{{index}}</p>
  </div>
  <script src="./lib/vue-2.4.0.js"></script>

  <script>
    var vm = new Vue({
      el: 'div',
      data: {
        // list: ['小明', '小红', '校长'],
        // list: [
        //   {'id': 1, name: '小明'},
        //   {'id': 2, name: '小黑'},
        //   {'id': 3, name: '小花'},
        //   ],

        list: {id: 1, name: '小红', gender: '女'},
      },
    });
  </script>
```



**迭代数字**

```html
    <p v-for="count in 10">这是第 {{ count }} 次循环</p>
```



#### `v-for` 补充

>  **就地更新策略:  vue在数据更新的时候, 只会更新必须要更新的DOM结构, 不会像`art-template` 重新生成一个DOM结构, 替换掉原来的DOM结构** 

**没有key-> 就地更新**

 当 Vue 正在更新使用 `v-for` 渲染的元素列表时，它默认使用“就地更新”的策略。如果数据项的顺序被改变，Vue 

将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染

 这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。 

 **我们希望可以在B和C之间加一个F，Diff算法默认执行起来是这样的:** **会复用之前的DOM结构**

![](image\没有key.jpg)

**有key -> 根据key, 更新DOM**

 为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 `key` 属性 ->  **为了更加高效更新虚拟DOM**

![](image\有key.jpg)

```js
<div v-for="item in items" v-bind:key="item.id">
  <!-- 内容 -->
</div>
```



### [key指令](https://www.zhihu.com/question/61064119/answer/183717717 )

>  **v-for 默认采用就地更新原则, 有key则根据key更新**

在组件中 , 使用`v-for` 的时候, 如果不使用 `v-bind:key()` , 可能会出现问题 , 使用key能够使页面的数据和`data`中的数据发生关联-----------> **能够提升性能, 避免一些BUG**



**使用`key`的注意事项**

- v-for 循环的时候，key 属性只能使用 `number`或者`string `
- key 在使用的时候，必须使用 v-bind 属性绑定的形式，指定 key 的值 

此案例中的`key`作用: 在复选框中勾选某个元素 , 如果不使用`key`绑定 , 在添加元素的时候, 被勾上的复选框, 不会改变, 但是数组中的成员发生改变, 不能随着成员的改变, 是复选框的跟着成员而移动

```html
 <div id="app">

    <div>
      <label>Id:
        <input type="text" v-model="id">
      </label>

      <label>Name:
        <input type="text" v-model="name">
      </label>

      <input type="button" value="添加" @click="add">
    </div>

    <!-- 注意： v-for 循环的时候，key 属性只能使用 number获取string -->
    <!-- 注意： key 在使用的时候，必须使用 v-bind 属性绑定的形式，指定 key 的值 -->
    <!-- 在组件中，使用v-for循环的时候，或者在一些特殊情况中，如果 v-for 有问题，必须 在使用 v-for 的同时，指定 唯一的 字符串/数字 类型 :key 值 -->
    <p v-for="item in list" :key="item.id">
      <input type="checkbox">{{item.id}} --- {{item.name}}
    </p>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        id: '',
        name: '',
        list: [
          { id: 1, name: '李斯' },
          { id: 2, name: '嬴政' },
          { id: 3, name: '赵高' },
          { id: 4, name: '韩非' },
          { id: 5, name: '荀子' }
        ]
      },
      methods: {
        add() { // 添加方法
          this.list.unshift({ id: this.id, name: this.name })
        }
      }
    });
  </script>
```



## `v-if`  和 `v-show` 指令

### 联系

这两个指令都能够让元素显示和隐藏

### 区别

但是显示和隐藏的方式 , 却完全不同

`v-if`  是**惰性的**如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。 

`v-show`   相比之下，`v-show` 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。 

### 优缺点

`v-if`  **具有较高的切换性能消耗 -> 如果控制条件为false, 则初始渲染时不会渲染DOM结构**

- 频繁的创建和删除元素
- 对于涉及到需要频繁切换的元素, 不建议使用`v-if`  推荐使用`v-show`

`v-show`  **具有较高的初始渲染性能消耗-> 不管显示还是隐藏都需渲染**

- 对于永远或者最开始渲染页面时, 不显示的元素, `v-show`  也会去创建一个元素, 消耗性能
- 对于在最开始渲染页面时, 可能永远也不希望被用户看到的元素, 推荐使用`v-if`

### 使用场景

`v-show`: 频繁切换元素的显示和隐藏

`v-if` :  要么存在显示, 要么不存在隐藏





## v-else 和 v-else-if

 `v-else` 元素必须紧跟在带 `v-if` 或者 `v-else-if` 的元素的后面，否则它将不会被识别。

**注意:  v-if , v-else 和 v-else-if 之间不能隔开**

### v-else

```js
//要么显示 男
<div v-if="gender === 1">
  <h3>男</h3>
</div>
//要么显示女
<div v-else>
   <h3>女</h3>
</div>
```



### v-else-if

```js
//要么显示 男
<div v-if="gender === 1">
  <h3>男</h3>
</div>
//要么显示女
<div v-else-if="gender === 0">
   <h3>女</h3>
</div>
//要么显示其他
<div v-else>
   <h3>不详</h3>
</div>
```











## v-text指令

- 和`v-cloak` 类似也能够给元素添加内容 , 但是没有闪烁问题 
- v-text会覆盖元素中原本的内容，但是 插值表达式  只会替换自己的这个占位符，不会把 整个元素的内容清空 

```html
<p v-cloak>++++++++ {{ msg }} ----------</p>
<h4 v-text="msg">==================</h4>
<div>{{msg2}}</div>
<div v-text="msg2"></div>
<div v-html="msg2">1212112</div>
```

`v-text` 和 `v-cloak` 不会解析标签 , 会原样输出



## v-html 指令

**能够解析html的标签 -----> 同 innerHTML**

```html
<div v-html="msg2">1212112</div>

var vm = new Vue({
      el: '#app',
      data: {
        msg: '123',
        msg2: '<h1>哈哈，我是一个大大的H1， 我大，我骄傲</h1>',
      }
    })
```



## v-pre 和 v-once

### v-pre

作用: 给某个元素添加, 这个元素会跳过vue的编译

```js
<span v-pre>{{ this will not be compiled }}</span>
//页面原样输出
{{ this will not be compiled }}
```

### v-once

作用: 这个元素会被vue渲染编译一次, 后续更新,vue会跳过这个元素

```js
<span v-pre>{{ this will not be compiled }}</span>
//会渲染一次
 this will not be compiled 
```



### 应用场景

**都是用来做性能优化的, 慎用**



## v-cloak 指令

实际开发中不常用, 由于webpack的存在, 不会存在插值表达式闪烁问题, webpack会在内存中预先编译

```js
<style>
	[v-cloak] {
      display: none; 
    }
</style>

#差值表达式
<div class="box" v-cloak>{{msg2}}</div>
var vm = new Vue({
      el: '.box',
      data: {
        msg: '哈哈哈哈',
      }
    })
```

**v-cloak能够解决  插值表达式闪烁问题**

在页面中的插值 `{{ content }}`  ,在 vue.js 还没加载完毕时 , 会显示 `{{ content }}`  , 所以可以给 有`v-cloak` 属性的元素隐藏, 当vue.js加载完毕后 ,  `v-cloak` 能够让元素显示



## 指令总结

### 经常用

```js
v-bind v-on v-model  v-for v-if v-show v-slot(插槽)
```



### 偶尔用的

```js
v-else  v-else-if  v-text v-html
```



### 基础不用

```js
v-pre v-once v-cloak
```









## 跑马灯效果

箭头函数中的`this` 就是 函数外部的 `this`  

```html
<div class="app">

    <input type="button" value="浪起来" @click="lang">
    <input type="button" value="低调" @click="stop">

    <h1>{{ msg }}</h1>
  </div>
  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '.app',
      data: {
        msg: '猥琐发育, 别浪, 稳住我们能赢!!!!',
        timeId: null //  把定时器的ID 存储在data数据中
      },
      methods: {
        lang () {
          //当timeId 不等于null说明上一个定时器没有执行完,就不执行下面的代码
          if (this.timeId) return

          this.timeId = setInterval(() => {
            //截取第一个字符串
            var start = this.msg.substr(0, 1)
            //截取尾部
            var end = this.msg.substr(1)
            //重新拼接
            this.msg = end + start
          }, 100)
        },
        stop () {
          clearInterval(this.timeId)
          this.timeId = null
        }
      }
    })
  </script>
```





## Todomvc案例

双击事件`@dblclick=""`





# Vue 第三天



## Vue中使用样式

**注意: `:class="{}"`  绑定的class 和 原生的`class` 共存**

```html
<div class="static" :class="{red: isRed}">
```

### class样式

1. 数组

第一种使用方式，直接传递一个数组，注意： 这里的 class 需要使用  v-bind 做数据绑定

```js
#类名需要用引号包起来, 不然会被当成一个变量
<h1 :class="['red', 'thin']">这是一个邪恶的H1</h1>
```

2. 数组中使用三元表达式

```
<h1 :class="['red', 'thin', flag?'active':'']">这是一个邪恶的H1</h1>
```

3. 数组中嵌套对象

由于三元表达式, 比较麻烦所以可以使用对象的方式

在数组中使用 对象来代替三元表达式，提高代码的可读性

```
<h1 :class="['red', 'thin', {'active': flag}]">这是一个邪恶的H1</h1>
```

4. 直接使用**对象**

此方式最好用 , 直接使用对象的方式

在为 class 使用 v-bind 绑定 对象的时候，对象的属性是类名，由于 对象的属性可带引号，也可不带引号

```
<h1 :class="{red:true, italic:true, active:true, thin:true}">这是一个邪恶的H1</h1>
```

也可以使用另一种方式

```html
<h1 :class="classObj" v-html="message"></h1>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: 'h1',
      data: {
        message: '<h3>我是一个大大的h1,大的你无法想象</h3>',
        classObj: {red: true, thin: true},
      },
    });
  </script>
```



### 内联样式Style

1. 直接在元素上通过 `:style` 的形式，书写样式对象

```php+HTML
<h1 :style="{color: 'red', 'font-size': '40px'}">这是一个善良的H1</h1>
```

2. 将样式对象，定义到 `data` 中，并直接引用到 `:style` 中

- 在data上定义样式：

```js
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' }
}
```

- 在元素中，通过属性绑定的形式，将样式对象应用到元素中：

```html
<h1 :style="h1StyleObj">这是一个善良的H1</h1>
```

3. 在 `:style` 中通过数组，引用多个 `data` 上的样式对象

- 在data上定义样式：

```javascript
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' },
        h1StyleObj2: { fontStyle: 'italic' }
}
```

- 在元素中，通过属性绑定的形式，将样式对象应用到元素中：

```
<h1 :style="[h1StyleObj, h1StyleObj2]">这是一个善良的H1</h1>
```





## ES6新增数组方法

### 数组的`Array.some()` 和 `.findIndex()`

`foreach() , some() , filter() , findIndex() `这些都是数组的新方法, 都会对数组的每一项, 进行遍历执行传入的函数

### `some(fn)`

`some()` 方法测试数组中是不是有元素通过了被提供的函数测试。它返回的是一个Boolean类型的值。

**注意：**如果用一个空数组进行测试，在任何情况下它返回的都是`false`。

> 需要 return true终止循环

**语法**

```js
arr.some(callback(element[, index[, array]])[, thisArg])
```

**返回值**

只要数组中有一个元素通过回调函数的测试就会返回**true**；所有元素都没有通过回调函数的测试返回值才会为false

```js
var array = [1, 2, 3, 4, 5];

var even = function(element) {
  // checks whether an element is even
  return element % 2 === 0;
};

console.log(array.some(even));
// expected output: true

```



`findIndex()`

`findIndex()`方法返回数组中满足提供的测试函数的第一个元素的**索引**。否则返回-1。

> 查找数组中对应对象的索引

**语法**

```js
arr.findIndex(callback[, thisArg])
```

**返回值**

返回找到的的数组中的成员的索引, 找不到返回-1

```js
// 删除功能
        del (id) {

          // findIndex()
          // var index = this.list.findIndex(() => {
          //   if (this.list.id === id) {
          //     return true
          //   }
          // })

          // this.list.splice(index, 1)


          //some的方法
          this.list.some((item, i) => {
            if (this.list.id = id) {
              this.list.splice(i, 1)
            }
          })
        }
```



### `Array.filter()`

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素

> 对数组进行过滤的
>
> **注意：** filter() 不会对空数组进行检测。
>
> **注意：** filter() 不会改变原始数组

**语法**

```
array.filter(function(currentValue,index,arr), thisValue)
```

**参数说明**

`function(currentValue,index,arr)`, 必须参数

![](E:\Vue\image\filter().png)



**实例**

```js
返回数组 ages 中所有元素都大于输入框指定数值的元素:

<p>最小年龄: <input type="number" id="ageToCheck" value="18"></p>
<button onclick="myFunction()">点我</button>

<p>所有大于指定数组的元素有？ <span id="demo"></span></p>

<script>
var ages = [32, 33, 12, 40];

function checkAdult(age) {
    return age >= document.getElementById("ageToCheck").value;
}

function myFunction() {
    document.getElementById("demo").innerHTML = ages.filter(checkAdult); //32 33 40
}
```



## ES6新增字符串方法

### 子串的识别

ES6 之前判断字符串是否包含子串，用` indexOf` 方法，ES6 新增了子串的识别方法。

- **includes()**：返回布尔值，判断是否找到参数字符串。
- **startsWith()**：返回布尔值，判断参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，判断参数字符串是否在原字符串的尾部。

**参数**

以上三个方法都可以接受两个参数，需要搜索的字符串，和可选的搜索起始位置索引。

**语法**

```js
string.includes('要包含的字符串')
#对应JQuery中的过滤选择器
#text=> 字符串
$('div:contains(text)')
```

```js
let string = "apple,banana,orange";
string.includes("banana");     // true
string.startsWith("apple");    // true
string.endsWith("apple");      // false
string.startsWith("banana",6)  // true
```

**注意点：**

- 这三个方法只返回布尔值，如果需要知道子串的位置，还是得用 indexOf 和 lastIndexOf 。
- 这三个方法如果传入了正则表达式而不是字符串，会抛出错误。而 indexOf 和 lastIndexOf 这两个方法，它们会将正则表达式转换为字符串并搜索它。



### 字符串补全`padStart()`和 `padEnd()`

- **padStart**：返回新的字符串，表示用参数字符串从头部（左侧）补全原字符串。
- **padEnd**：返回新的字符串，表示用参数字符串从尾部（右侧）补全原字符串。

**语法**

```js
padStart(maxLength, fillString)
padEnd(maxLength, fillString)
```

**参数**

以上两个方法接受两个参数，第一个参数是指定生成的字符串的最小长度，第二个参数是用来补全的字符串。如果没有指定第二个参数，默认用空格填充。

- 如果指定的长度小于或者等于原字符串的长度，则返回原字符串:
- 如果原字符串加上补全字符串长度大于指定长度，则截去超出位数的补全字符串:

```js
console.log("h".padStart(5,"o"));  // "ooooh"
console.log("h".padEnd(5,"o"));    // "hoooo"
console.log("h".padStart(5));      // "    h"
```



## 汽车品牌案例

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <link rel="stylesheet" href="./lib/bootstrap-3.3.7.css">
</head>
<body>
    <div id="app">
        <div class="panel panel-primary">
          <div class="panel-heading">
            <h3 class="panel-title">添加品牌</h3>
          </div>
          <div class="panel-body form-inline">
            <label>
              Id:
              <input type="text" class="form-control" v-model="id">
            </label>
    
            <label>
              Name:
              <input type="text" class="form-control" v-model="name">
            </label>
    
            <!-- 在Vue中，使用事件绑定机制，为元素指定处理函数的时候，如果加了小括号，就可以给函数传参了 -->
            <input type="button" value="添加" class="btn btn-primary" @click="add">
    
            <label>
              搜索名称关键字：
              <input type="text" class="form-control" v-model="keyword">
            </label>
          </div>
        </div>   
    
        <table class="table table-bordered table-hover table-striped">
          <thead>
            <tr>
              <th>Id</th>
              <th>Name</th>
              <th>Ctime</th>
              <th>Operation</th>
            </tr>
          </thead>
          <tbody>
            <!-- 要实现过滤的功能, 这个地方就不能传特定的数组进行渲染 -->
           <tr v-for="item in search(keyword)" :key="item.id">
             <td>{{ item.id }}</td>
             <td>{{ item.name }}</td>
             <td>{{ item.ctime }}</td>
             <td>
               <a href="javascript:;" @click.prevent="del(item.id)">删除</a>
             </td>
           </tr>
          </tbody>
        </table>
     
      </div>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {
        id: '',
        name: '',
        keyword: '',
        list: [
          {id: 1, name: '奔驰', ctime: new Date()},
          {id: 2, name: '宝马', ctime: new Date()},
        ]
      },
      methods: {
        add () {
          var car = {id: this.id, name: this.name, ctime: new Date()}
          this.list.push(car)
          this.id = this.name = ''
        },

        // 删除功能
        del (id) {

          // findIndex()
          // var index = this.list.findIndex(() => {
          //   if (this.list.id === id) {
          //     return true
          //   }
          // })

          // this.list.splice(index, 1)

          //some的方法
          var res = this.list.some((item, i) => {
            if (this.list.id = id) {
              this.list.splice(i, 1)
              return 
            }
          })
        },

        //搜索功能
        search (keyword) {

          // // 思路: 拿到keyword, foreach循环比对 indexof
          // // forEach() + indexOf()
          // var newList = []
          // this.list.forEach(item=>{
            
          //   if (item.name.indexOf(keyword) === -1) return
          //   newList.push(item)
          // })

          // return newList

         //  filter() + includes()
         // 数组新方法filter, 返回符合条件的新数组
          return this.list.filter(item => {
            // 字符串中的新方法, 返回true或者false
            if (item.name.includes(keyword)) {
              return item
            }
          })

        },
      }
    });
    
  </script>
</body>
</html>
```





## Vue调试工具`vue-devtools`的安装步骤和使用

[Vue.js devtools - 翻墙安装方式 - 推荐](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN)



## computed 计算属性

### 为什么要用计算属性

 模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护 ;

**所以当我们在模板(插值表达式)中处理大量的JS的复杂逻辑的时候, 我们就应该用计算属性**

```html
<h3>{{ msg.split('').reverse().join('') }}</h3> 
```



### 什么是计算属性

>  **计算属性都会依赖到别的属性, , 计算属性通过一定 逻辑计算后得到的一个属性, 把要处理逻辑的数据在计算属性computed中处理逻辑**

在`computed` 中能够定义一些属性, 这些属性叫计算属性, 本质上这些属性都是方法, 但是我们在使用的时候, 不会把它当做一个方法使用, 而是类似`data`中的属性去使用 , **必须 `return` 计算属性的值**



###  使用注意点

**注意点 1** 

**计算属性, 在使用的时候, 一定不要加()调用, 直接把它当做属性使用; 计算属性是属性,不是方法**

计算属性中的属性和`data` 中的数据不能同名, 因为计算属性和data中的属性都会挂载到vm实例上 

**注意点 2** 

在计算属性, function内部, 计算属性所用到的data中的依赖属性发生改变时, 计算属性就会重新计算

**注意点 3** 

> 计算属性性能更高, 多次使用会缓存, 只会执行一次计算属性

依赖属性特性: 计算属性的值, 会缓存起来, 方便在页面中多次使用, 只要计算属性所依赖的值没有发生改变, 就不会对计算属性重新求值

**注意点 4**

计算属性默认情况下是不允许被修改的

### 计算属性完整形态

**计算属性完整形态是一个对象, 有get和set方法**

```js
  <div id="app">
    <input type="text" v-model="first"> +
    <input type="text" v-model="last"> =
    //默认计算属性不能修改, 所以不能使用v-model, 但是如果就像使用, 就需要使用计算属性的完整形态    
    <input type="text" v-model="fullname">
  </div>

    const vm = new Vue({
      el:'#app',
      data: {
        first: '',
        last: ''
      },
      computed: {
         
        fullname(){
          return this.first + '-' + this.last
        },
        //计算属性的完整形态
          fullname: {
              #当访问计算属性的值, 会调用get方法, 缓存
              get(){
                  
              },
        		#修改计算属性的时候, 会调用set方法
              set(value){
        		#解构赋值	
                 [this.fitst, this.last] = value.split('-')
              }
          }
      }
    })
```







## keyup监听事件

动态拼接名称案例

```js
  <div id="app">
    <input type="text" v-model="firstname" @keyup="getname"> +
    <input type="text" v-model="lastname" @keyup="getname"> =
    <input type="text" v-model="fullname">
  </div>
  <script>
    let vm = new Vue({
      el: '#app',
      data: {
        firstname: '',
        lastname: '',
        fullname: ''
      },
      methods:{
        getname () {
          this.fullname = this.firstname + '-' + this.lastname
        }
      }
    })
  </script>
```



## watch 监听属性

作用

监视某个属性的变化, 只要这个属性变化了, 就可以监听了

### watch监听data

watch能够监听data中到的数据的改变, 当data中数据的改变, 都会触发watch中对应名称的方法的触发

- `watch` 属性和 `el, data, methods` 平级
- data中的值都是`watch` 的方法名. 能够监听对应值的改变而触发方法
- 对应的方法都有两个参数 `(newVal, oldVal)`分别监听的值的最新值, 和发生改变前的值

**监听属性, 只能监听简单数据类型, 当data中的属性是一个对象时, 就无法监听到了**

```js
    let vm = new Vue({
      el: '#app',
      data: {
        firstname: '',
        lastname: '',
        fullname: ''
      },
      watch: {
        firstname(newVal, oldVal) {
          this.fullname = newVal + this.lastname
        },
        lastname(newVal) {
          this.fullname = this.firstname + newVal
        }
      }
    })
```



### watch完整形态

如果想要监听复杂数据类型里的属性的变化, 需要`deep:true`

```js
    let vm = new Vue({
      el: '#app',
      data: {
      	car: {
            brand: '马萨拉蒂',
            price: 10
        }
      },
      watch: {
        car:{
            deep: true, // 深度监听: 能够监听到car属性内部属性的变化
            handler(value) { # value 是改变后的值
                console.log('变了' , value)
            },
            immediate:true // 页面加载会立即加载一次
        }
      }
    })
```





### watch监听路由

**对于非DOM元素, 通过一个window提供的监听事件就无法监听,watch能够监非DOM元素**

vm实例`this.$route`上记录了, 路由相关信息, `path`属性是路由地址

```js
      watch: {
        // 监听路由
        '$route.path': function (newVal, oldVal) {
          if (newVal === '/login'){
            console.log('欢迎来到登录页面')
          } else {
            console.log('欢迎来到注册页面')
          }
        }
      }
```





### `watch`  `computed` 和 `methods` 对比

1. `computed`属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。主要当作属性来使用；
2. `methods`方法表示一个具体的操作，主要书写业务逻辑；
3. `watch`一个对象，键是需要观察的表达式，值是对应回调函数。主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑操作；可以看作是`computed`和`methods`的结合体



# [vue指令综合练习(todos)](http://todomvc.com/ )



# Vue 第四天



## Vue实例的生命周期

### 什么书生命周期

从Vue实例创建, 运行, 到销毁期间, 总是伴随着各种事件, 这些事件统称为生命周期

vue是框架, 内部帮我们处理了非常多的事情, 我们需要了解vue内部的流程

**我们希望能够在vue的某个阶段去做了什么事**

### 生命周期钩子

vue会在生命周期中特定的时机, 会自动调用这些钩子函数

生命周期钩子只是生命周期事件的别名而已

生命周期钩子 = 生命周期函数 = 生命周期事件



### 生命周期函数

#### 初始化阶段的生命周期钩子

```js
<div id="app">
    <input type="button" value="修改msg" @click="msg='No'">
    <h3 id="h3">{{ msg }}</h3>
</div>

var vm = new Vue({
      el: '#app',
      data: {
        msg: 'ok'
      },
      methods: {
        show() {
          console.log('执行了show方法')
        }
      },
```

**数据初始化前后的两个钩子函数**

##### `beforeCreate` 

- 第一个生命周期函数
- 此时实例刚在内存中被创建出来, 还没进行初始化, `data` 和 `methods`  中的数据和事件还没初始化 
- 数据初始化前自动调用

```js
 beforeCreate() { // 这是我们遇到的第一个生命周期函数，表示实例完全被创建出来之前，会执行它
        console.log(this.msg) // log  {{ msg }}
        this.show() //show is a not function
        // 注意： 在 beforeCreate 生命周期函数执行的时候，data 和 methods 中的 数据都还没有没初始化
      },
```

##### `created`

- 第二个生命周期函数
- 实例已经被创建出来, 并且`data`  和`methods` 已经被初始化好了	
- 数据初始化之后自动调用

```js
created() { // 这是遇到的第二个生命周期函数
         console.log(this.msg) // ok
         this.show()		  // 执行了show方法
        //  在 created 中，data 和 methods 都已经被初始化好了！
        // 如果要调用 methods 中的方法，或者操作 data 中的数据，最早，只能在 created 中操作
      },
```



**虚拟DOM  -> 真实DOM 挂载前后的两个钩子函数**

##### `beforeMount`

- 第三个生命周期函数
- 表示模板已经在内存中编译完成了, 但是还未把编译好的模板渲染到页面中
- 在` beforeMount `执行的时候，页面中的元素，还没有被真正替换过来，只是之前写的一些模板字符串
- 此时内存中是最新的, 页面中还未渲染

```js
 beforeMount() { 
     // 这是遇到的第3个生命周期函数，表示 模板已经在内存中编辑完成了，但是尚未把 模板渲染到 页面中
      console.log(document.getElementById('h3').innerText)  // {{ mag }}
     // 在 beforeMount 执行的时候，页面中的元素，还没有被真正替换过来，只是之前写的一些模板字符串
```

##### `mounted`

- 这是第四个生命周期函数,  也是实例创建期间的最后一个生命周期函数
- 此函数, 表示内存中的模板已经真实的挂载到页面中, 用户已经可以看到渲染之后的页面了
- 当执行完`mounted`  之后, `Vue` 实例就已经被完全的创建出来了, 此时如果没有其他操作, 这个实例就静静的躺在内存中, 一动不动, **脱离创建阶段, 进入运行阶段**
- 如果通过某些插件操作**页面上**的`DOM`节点, 最早要在`mounted`中进行
- 此时页面中已经是最新的

```js
 mounted() { 
         console.log(document.getElementById('h3').innerText) // ok
        // 注意： mounted 是 实例创建期间的最后一个生命周期函数，当执行完 mounted 就表示，实例已经被完全创建好了，此时，如果没有其它操作的话，这个实例，就静静的 躺在我们的内存中，一动不动
      },
```



#### 运行期间的生命周期函数

**DOM更新前后两个钩子函数**

这两个事件会根据`data`的改变而触发, 换而言之, 数据不更新, 运行阶段的生命周期函数就不会执行

##### `beforeUpdate`

- 当`data` 数据发生改变的时候, 才会触发`beforeUpdata`, 在触发的时候, 内存中的`data`已经更新
- 但是页面中的`data`还未同步

##### `updataed`

- 当函数执行的时候, 页面中的显示数据已经和内存中的`data` 保持同步, 都是最新的



#### 销毁前后的两个生命周期函数

当页面不存在时, 就已经从运行阶段进入到了销毁阶段

##### `beforeDestroy`

- 当执行`beforeDestroy`钩子函数时, Vue实例就从运行阶段进入到了销毁阶段
- 执行`beforeDestroy` 时, 实例身上的所有`data` 和 `methods` 以及指令, 过滤器 ....都是出于可用状态, 此时还未执行真正的销毁过程

##### `destroy`

- 当执行到`destroy`函数的时候, 组建已经被完全销毁, 此时组件中的所有数据, 方法, 指令, 过滤器都已经不可用了

### 生命周期图

![](image\lifecycle.png)



### 八个生命周期钩子的应用场景

**发送ajax渲染数据 created  -----> 最常用**

最早最好在`created(){}` 钩子函数中发送, 数据初始化之后, 把能替换el中的数据



**DOM操作  mounted  ----> 最常用**

需要进行DOM操作的时候, 最早在mounted钩子中操作

在使用到第三方库的时候, 需要操作DOM的时候 **swiper 轮播图插件 iscroll 区域滚动插件  mui** 等比需要DOM初始化的时候, 最早在`mounted` 中初始化



**updated 操作数据更新后的DOM**

当我们想要操作数据更新后的DOM结构时使用



**beforeDestroyed 释放资源时使用**

适合释放自己开启的资源, vue自己的资源, 会自己释放, 自己的资源, 例如 定时器等window身上的事件



**actived 和 deactived**

 keep-alive 组件激活时调用  /  keep-alive 组件停用时调用 

**errorCaptured**

 当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。此钩子可以返回 `false` 以阻止该错误继续向上传播。 

## 父子组件生命周期执行顺序

 父组件先创建，然后子组件创建；子组件先挂载，然后父组件挂载 

 Vue父子组件生命周期钩子的执行顺序遵循：从外到内，然后再从内到外，不管嵌套几层深，也遵循这个规律。 

![](./image/父子组件生命周期执行顺序.png)

​	

所以在进行父子组件传值的时候， 不能再父组件`mounted` 中发`ajax` 这个时候, 子组件已经挂载, 无法在初始化data

## mock数据

mock 假数据

当在公司开发接口没有些写好的, 需要前端或者后端合作根据mock数据, 写接口

### 后端mock数据



### 前端mock数据

1. express koa nodejs 写一些借口
2. mock.js 库  需要配置
3. **json-server 会根据json文件**

### json-server 接口生成工具--->论文设计  

根据json文件自动生成借口

安装

```js
yarn global add json-server
```

使用

- 准备一个json文件
- 使用命令, 创建接口

```js
json-server data.json
```

### 接口说明

**rest风格接口**

接口地址都相同, 但是请求方式不同, 接口类型不同

查询:  GET

添加: post

删除: delete

修改: put / patch

put和 patch的区别

patch:  只会修改传递的参数

put: 会修改所有的字段, 如果使用put  需要把所有的字段都传递



## axios 发送ajax

> 如果是 `get / delete` 请求, 请求参数放在 `params` 中
>
> 如果是 `put/post/patch` 请求参数放在`data` 中

**axios和vue , react 没有半毛钱关系**

下载

```shell
yarn add axios
```

发送ajax

```js
axios({
    method: 'get',  //请求方式
    url: '/user'  //接口地址
})
//成功的处理
.then(res => {
    
})
//失败的处理
.catch(err => {
    
})
```



### **使用axios都会发送两次请求**

第一次的请求方法为 options 又叫做**预检请求**

第二次的请求方法为 真实的请求地址和方法, **叫做真实请求**

请求分为: 简单请求 和 非简单请求

 

**只要同时满足以下两大条件，就属于简单请求 :** 

1) 请求方法是以下三种方法之一：

- HEAD
- GET
- POST

（2）HTTP的头信息不超出以下几种字段：

- Accept
- Accept-Language
- Content-Language
- Last-Event-ID
- Content-Type：只限于三个值`application/x-www-form-urlencoded`、`multipart/form-data`、`text/plain`

 凡是不同时满足上面两个条件，就属于非简单请求。 

**原因:** 

 前后端未满足“同源策略/SOP”，俗称请求跨域。浏览器一旦发现请求跨域，就会使用CORS通信，自动添加一些附加的头信息，简单请求只会有一次请求，只有非简单请求会附加一次请求。 



## 使用json-server 和 axios 实现tudos



## [Vue-resource 发送ajax](https://github.com/pagekit/vue-resource)

除了 vue-resource 之外，还可以使用 `axios` 的第三方包实现实现数据的请求

### 测试的URL请求资源地址：

- get请求地址： http://vue.studyit.io/api/getlunbo
- post请求地址：http://vue.studyit.io/api/post
- jsonp请求地址：http://vue.studyit.io/api/jsonp

### `vue-resource`的基本使用

[API使用文档](https://github.com/pagekit/vue-resource/blob/develop/docs/http.md)

```html
<div id="app">
    <input type="button" value="get请求" @click="getInfo">
    <input type="button" value="post请求" @click="postInfo">
    <input type="button" value="jsonp请求" @click="jsonpInfo">
</div>

<script>
	var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
          getInfo () {}
          postInfo () {}
          jsonpInfo () {}
      }
    });
</script>
```



#### `$http.get()`

**参数**

`get(url, [config])`

- parm1 :  请求地址
- parm2 : 可选, 配置选项 

当发送`ajax`之后, 拿到通过`.then(callback)` 拿到服务器的数据, 

- 服务器响应的数据`result ` 中 `result.body` 中是响应的数据

```js
getInfo() { // 发起get请求
          //  当发起get请求之后， 通过 .then 来设置成功的回调函数
          this.$http.get('http://vue.studyit.io/api/getlunbo').then(function (result) {
            // 通过 result.body 拿到服务器返回的成功的数据
            // console.log(result.body)
          })
	},
```



#### `$http.post()`

`post(url, [body], [config])`

**参数**

- parm1 : 请求路径
- parm2 : 请求体

- parm3 : 配置选项, 可选

```js
postInfo() { // 发起 post 请求   application/x-wwww-form-urlencoded
          //  手动发起的 Post 请求，默认没有表单格式，所以，有的服务器处理不了
     //  通过 post 方法的第三个参数， { emulateJSON: true } 设置 提交的内容类型 为 普通表单数据格式
       this.$http.post('http://vue.studyit.io/api/post', {}, { emulateJSON: true })					.then(result => {
            	console.log(result.body)
          	})
	},
```



#### `$http.jsonp()`

`jsonp(url, [config])`

**参数**

- parm1 : 请求路径
- parm2 : 配置选项, 可选

```js
 jsonpInfo() { // 发起JSONP 请求
          this.$http.jsonp('http://vue.studyit.io/api/jsonp').then(result => {
            console.log(result.body)
          })
      }
```





## JSONP的实现原理

### 出现背景

由于浏览器的安全性限制, 不允许`Ajax` 访问域名不同, 端口不同, 协议不同的数据接口	

### 原理

可以动态的创建script标签, 把script的src属性, 指向数据接口地址, 因为script不存在跨域限制, 就可以获取道我们想要的数据, 这种数据获取方法就叫做`JSONP`

> 注意 : 根据JSONP的实现原理，知晓，JSONP只支持Get请求 

### 实现过程

- 前端先定义一个方法, 以script方式发送给后台

#### 客户端

```html
		<script>
			function  show123(data) {
				console.log(data);
			}
		</script>
		
		<!- 通过script标签, 实现jsonp的跨域请求-->
		<script src="http://127.0.0.1:3000/jsonp?callback=show123"></script>
```

#### 服务端

```js
var http = require('http')
var urlModule = require('url')

var server = http.createServer()

server.on('request', function (req, res) {
	// 把url请求路径转化为一个query对象
	var url = urlModule.parse(req.url, true)

	// query对象pathname属性数问号前面的路径
	var pathname = url.pathname
	if (pathname === '/jsonp') {

		// 拿到query对象中callback属性的值
		var proprety = url.query.callback

		var data = {
			name: '小明',
			age: 18,
			gender: '女孩子',
			hobby: ['吃饭', '睡觉', '打豆豆']
		}
        
        //把对象响应给客户端
        // JSON.stringify()将对象序列化为对象字符串,响应给客户端
		res.end(`${proprety}(${JSON.stringify(data)})`)
	}	
		
})

server.listen(3000, function () {
	console.log('the server is running....');
})
```









## 汽车品牌案例改造

### 渲染页面

从数据库获取`list`JSON数据, 渲染到页面中

- getList

```js
	methods: {
				getList() {
                    //get请求返回的数据中body是数据
					this.$http.get('api/getprodlist').then(resutl => {
						var data = result.body
						if (data.status !== 0) return

						// 把服务器的数据赋值给list
						this.list = data.message
					})
				}

			},
                
    // 在created生命周期发送ajax请求
	created () {
				this.getList()
		},
```

### 添加功能

```js
// 添加功能
	add() {
// 点击添加按钮的时候, 以post的方式把{name: this.name}发送给服务器
	this.$http.post('api/addproduct', {name: this.name}, {emulateJSON: true})
		.then(result=> {
			if (result.body.status === 0) {
				// 添加成功后, 重新发送ajax请求, 重新渲染页面
				//this.getList()可以发送ajax请求, 渲染页面
					this.getList()
			}else {
					alert('添加失败')
			}
		})
	},
```

### 删除功能

```js
// 删除功能
del(id) {
	this.$http.get(`http://vue.studyit.io/api/delproduct/` + id)
		.then(result => {
			if (result.body.status === 0 ) {
				// 删除成功
				this.getList()
			}else {
				alert('删除失败')
			}
		})
} 
```

## `vue-resource`  配置

### root配置

Set default values using the global configuration.

- 如果我们通过全局配置了请求的数据接口根域名, 则每次发起 http 请求的时候, 请求的 `url` 路径必须以相对路径开头, **前面不能带`/`**, 否则, 不会启用路径拼接

```js
#设置根域名, 这个配置只能在相对路径中生效, 
//在get.post请求中, 我们必须使用相对路径开头才能生效
Vue.http.options.root = '/root';

Vue.http.headers.common['Authorization'] = 'Basic YXBpOnBhc3N3b3Jk';
```

### emulateJSON配置

处理`post`请求时, 设置提交的内容为普通表单大户局类型

```js
Vue.http.options.emulateJSON = true
```









# Vue第五天

## 响应式数据

**在vue中, 把被劫持的数据, 叫做响应式数据, 一旦数据发生了改变, 数据对应的DOM会被更新, 但是这个过程是异步**

JS 是单线程: js同一时间只能做一件事情

JS 异步:  同一时间做多件事情,, 异步不会阻塞



**一旦数据发生改变, vue 会自动去更新DOM, 这个过程是异步的**

**原因: 为了性能**

**造成的影响: 改完数据, 不能立即获取更新的DOM, 需要操作更新后的DOM, 需要vm.$nextTick()**



### 事件循环

异步操作: ajax  注册的事件  定时器  fs文件操作

**JS 主线程  -->    浏览器   -->  队列   --> JS  就形成了事件循环**



**JS异步的处理**

**JS遇到异步代码,会把异步代码交给 浏览器, 浏览器是多线程的, 浏览器会解析代码, 把JS要做的事件放在队列中,  当JS主线程加载完毕, 会出队列中查看异步要做的事件, 当做主程序去执行队列中的代码**





## vue.nextTick()-DOM异步更新

修改完数据, 立即操作对应的DOM, 可能拿不到, 因为DOM更新是异步的

如果在updated中操作DOM, 会导入任何数据更新都会触发

**vue.nextTick() 会在数据修改后, DOM更新完立即执行**

vue在组件内部也把vue.nextTick()挂载到组件上, 通过`vm.$nextTick( () => {} )`





## 动态添加的数据不是响应式的以及$set

### vue中对象的更新检测

响应式数据: 被vue劫持的数据, 属性的值是`(...)`

动态给vue添加的属性,  它不是响应式的数据(没有被vue劫持)



### vue.set

给响应式的对象,添加一个响应式属性, 并确保这个新属性也是响应式的, 且触发视图更新

**由于JS的限制, vue不允许给根级别的data, 添加响应式的属性, 但允许, 给根级别下的对象属性添加属性**



### [vue中数组的更新检测](https://cn.vuejs.org/v2/guide/list.html)

**由于JS的限制, 即使在vue的data中定义的数组, vue不能劫持到数组的下标和长度的变化**

原因: ES5的 object.defineProperty(), 无法检测到数组的下标和长度

```js
var vm = new Vue({
  data: {
    items: ['a', 'b', 'c']
  }
})
vm.items[1] = 'x' // 不是响应性的
vm.items.length = 2 // 不是响应性的
```



解决方法: 

1. vm.$set()

```js
//你也可以使用 vm.$set 实例方法，该方法是全局方法 Vue.set 的一个别名：
vm.$set(vm.items, indexOfItem, newValue)

// Vue.set
Vue.set(vm.items, indexOfItem, newValue)
```



1.  数组变异: vue对数组的方法进行包裹

   - 调用数组的方法

   ```js
   vm.items.splice(newLength)
   ```

   



## Vue 中的组件

### 什么是组件

 组件的出现，就是为了拆分Vue实例的代码量的，能够让我们以不同的组件，来划分不同的功能模块，将来我们需要什么样的功能，就可以去调用对应的组件即可

### 组件化和模块化

模块化: 是基于代码逻辑进行划分的, 方便代码的分层开发, 保证每一个功能模块的职能单一

​			一个文件就是一个模板, 每一模板就实现一个功能

组件化: 是基础UI界面进行划分的, 前端的组件化方便UI组件的重用

​			把一个大的页面, 拆分成一个一个的组件, 一个组件有自己独立的结构(html), 样式(css), 行为(js)

### 全局组件的定义方式

#### 组件创建方式一

1. 使用`Vue.extend()`和 `Vue.component()`

- `Vue.extend({})` 能够创建一个组件模板对象
- `Vue.component('组件名称', Vue.extend{})`  定义一个真正的全局的组件
  - 组件名称如果采用驼峰命名, 在使用组件的使用需要用`-`连接, 大写转小写
  - 组件名称如果不采用驼峰命名, 直接使用即可

```html
	
 <div class="app">
    <!-- <my-com></my-com> -->
    <mycom></mycom>
  </div>

<script>
	// 使用Vue.extend()定义一个全局的组件模板对象, 会返回创建的组件模板对象
    var com1 = Vue.extend({
      template: '<h1>我是通过Vue.extend创建的全局组件</h1>'
    })

    // 使用Vue.component('组件名称', 创建的组件模板对象)注册为一个真正的组件
    // Vue.component('myCom', com1)
    Vue.component('mycom', com1)


    var vm = new Vue({
      el: '.app',
    });
</script>
```



#### 组件创建方式二

> 不论以哪种方式创建的组件, template中也只能有一个根元素

直接使用`Vue.component('组件名称', {})`

- `template`  属性中, 只能有一个根元素
- `template` 指向模板字符串

```html
  <div class="app">
    <mycom2></mycom2>
  </div>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>

    Vue.component('mycom2', {
      template: '<div><h1>template中只能有一个根元素</h1></div>'
    })
  
    var vm = new Vue({
      el: '.app',
    });
  </script>
```



#### 组件创建方式三

和第二种类似, 由于在`template` 中书写模板字符串, 没有智能提示, 可以把模板抽离出去, 在`html` 中书写

但是, 需要在`VM` 控制的区域外部写

```html
  <div class="app">
    <mycom3></mycom3>
  </div>

  <!- 在.app的外部定义template-->
  <template id="temp">
    <div>
      <h3>这是有智能提示的template</h3>
      <h4>好用!!!!!!!!!!</h4>
    </div>
  </template>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>

    // 定义一个组件
    Vue.component('mycom3', {
      template: '#temp'
    })

    var vm = new Vue({
      el: '.app',
    });
  
  </script>
```



### 组件中的data

组件中的data必须是个函数,且必须return 一个对象

**一个组件的 `data` 选项必须是一个函数**，因此每个实例可以维护一份被返回对象的独立的拷贝： 

**保证每一组件都有自己独立的数据**, 所以data为一个函数, return一个 字面量 `{}`

```html
<div id="components-demo">
  <button-counter></button-counter>
  <button-counter></button-counter>
  <button-counter></button-counter>
</div>
```





## 定义私有组件

在`VM` 实例中, 和`data el methods` 以及生命周期钩子函数平级的属性`components`

```js
var vm = new Vue({
    el: '.app',
    //定义私有组件
    components: {
        template: '#temp'
    }
})
```

**example**

 ```html
  <div class="app">
    <mycom></mycom>
  </div>

  <div class="app2">
    <mycom></mycom>   <!--error-->
  </div>

  <template id="temp">
    <div>
      <h1>这是.app的私有组件</h1>
    </div>
  </template>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>
  
    var vm = new Vue({
      el: '.app',
      data: {},
      methods: {},
      filters: {},
      directives: {},
      components: {
        mycom: {
          template: '#temp'
        }
      },

      // 生命周期钩子函数
      beforeCreat(){},
      created(){},
      beforeMount(){},
      mounted(){},
      beforeUpdate(){},
      updated(){},
      beforeDestroy(){},
      destroyed(){}
    });


    var vm2 = new Vue({
      el: '.app2'
    });
  
  </script>
 ```





## 目前所学的VM实例的属性成员

```js
var vm = new Vue({
    el: '.app',
    data: {},
    methods: {},
    filters: {},
    directives: {},
    components: {},
   
    // 八个生命周期函数
    beforeCreat(){},
    created(){},
    beforeMount(){},
    mounted(){},
    beforeUpdate(){},
    updated(){},
    beforeDestroy(){},
    destroyed(){}
})
```



## 组件中的属性

### 组件中的`template`

能够存放模板字符串

### 组件中的`data`

- `data` 必须为一个`function` ,不同于Vue实例中的`data`为一个对象
- `data` 而且必须有返回值, 且必须返回一个对象
  - 返回这个对象最好是一个对象字面量
  - 如果return的是一个对象的地址, 则多个组件实例操作同一个对象
- `data` 中的数据, 外部可以使用

```js
Vue.component('com', {
    template: '<div>{{ msg }}</div>'
    data() {
		return {
            msg: '这是组件中的msg'
        }    
	}
})
```



**计数器案例**

```html
  <div id="app">
    <mycom></mycom>
    <hr>
    <mycom></mycom>
    
  </div>
  <!-- 定义一个模板字符串 -->
  <template id="temp">
    <div>
      <input type="button" value="+1" @click="add">
      <p>{{ msg }}</p>
    </div>
  </template>


  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    // 计数器组件
    Vue.component('mycom', {
      template: '#temp',
      data() {
        return {
          msg: 0
        }
      },
      methods: {
        add(){
          this.msg++
        }
      }
    })
    //vue实例
    var vm = new Vue({
      el: '#app',
    });

  </script>
```



## 使用`v-if` 和 `v-else` 切换组件

- `v-if="flag"`  当flag = true 时显示元素
- `v-else`  当flag = false 时才显示元素 

```html
  <div id="app">

    <a href="#" @click.prevent="flag = true">登录</a>
    <a href="#" @click.prevent="flag = false">注册</a>

    <login v-if="flag"></login>
    <register v-else="flag"></register>
  </div>
  <script src="./lib/vue-2.4.0.js"></script>
  <script>

    // 定义一个组件
    Vue.component('login', {
      template: '<h1>登录组件</h1>',
    })

    Vue.component('register', {
      template: '<h1>注册组件</h1>',
    })

    var vm = new Vue({
      el: '#app',
      data: {
        flag: true,
      },
    });
  
  </script>
```



## 多个组件之间的相互切换(动态组件)

- 需要借助`Vue` 提供的`<component :is="组件名"></component>`  标签实现多个组件之间的切换
- `<component>`  是一个标签, `:is` 中 要显示的组件
  - `<component :is=" 'login' "></component>`  `=`  `<login></login>`
  - `:is="变量"`  操作这个变量就可以实现切换多个组件之间的切换

```html
<component :is="comName"></component>
```



**多个组件切换案例**

```html
  <div id="app">
    <a href="#" @click.prevent="compoName='login'">登录</a>
    <a href="#" @click.prevent="compoName='register'">注册</a>
    <a href="#" @click.prevent="compoName='other'">其他</a>
    <component :is="compoName"></component>

  </div>

  <!--定义三个要展示的组件模板-->
  <template id="temp1">
    <h1>这是登录模块的组件</h1>
  </template>

  <template id="temp2">
    <h1>这是注册模块的组件</h1>
  </template>


  <template id="temp3">
    <h1>这是其他模块的组件</h1>
  </template>
  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    //定义组件
    Vue.component('login', {
      template: '#temp1'
    })

    Vue.component('register', {
      template: '#temp2'
    })

    Vue.component('other', {
      template: '#temp3'
    })

    var vm = new Vue({
      el: '#app',
      data: {
        //默认展示login组件
        compoName: 'login'
      }
    });
  </script>
```



## [组件切换动画]([https://cn.vuejs.org/v2/guide/transitions.html#%E5%A4%9A%E4%B8%AA%E7%BB%84%E4%BB%B6%E7%9A%84%E8%BF%87%E6%B8%A1](https://cn.vuejs.org/v2/guide/transitions.html#多个组件的过渡))

- 只需要在`<component></component>`  外包裹一个`<transition></transition>` 即可
- 动画两个条件都要满足, 还需要定义动画
  - `.v-enter, .v-leave-to {}`
  - `.v-enter-active, .v-leave-active {}`

- 为了保证上一个离开动画结束后, 在执行进入动画, 可以在添加`mode` 属性  `<transition mode="out-in">`

  

```html
<style>
    .v-enter,
    .v-leave-to {
      opacity: 0;
      transform: translateY(30px)
    }

    .v-enter-active,
    .v-leave-active {
      transition: all .5s;
    }
  </style>

  <div id="app">
    <a href="" @click.prevent="compoName = 'login'">登录</a>
    <a href="" @click.prevent="compoName = 'register'">注册</a>

    <!-- 把组件中 transition 包裹 -->
    <transition mode="out-in">
      <component :is="compoName"></component>
    </transition>
  </div>

  <!-- 定义组件模板 -->
  <template id="login">
    <h1>登录组件</h1>
  </template>
  <template id="register">
    <h1>注册组件</h1>
  </template>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    // 定义组件
    Vue.component('login', {
      template: '#login'
    })
    Vue.component('register', {
      template: '#register'
    })
    var vm = new Vue({
      el: '#app',
      data: {
        compoName: 'login'
      }
    });
  </script>
```



## 组件通讯



### 父组件向子组件传值

**必须在父组件的template中使用子组件, 才能形成父子组件**

默认情况下, 父组件data中的值, 在子组件中是无法访问的

1. 需要在子组件中以属性绑定的形式, 在子组件中绑定一个属性传递父组件的值,

2. 在子组件中的定义`props`属性, props是一个数组, 把绑定的属性, 在`props` 定义

3. 使用绑定的属性,就可以使用父组件data的中的值

**父组件提供数据 --> 父组件把数据传给子组件 --> 子组件接收父组件传递的数据 --> 子组件渲染数据**

**`props`中的定义的属性都是父组件中传递过来的, 数据都是只读的(可以修改,但是会报错)**

**子组件自己的`data` 是自己私有的, 比如子组件通过ajax请求回来的数据, 都可以放到`data`上 , data上的数据都是可读可写的**

```html
<div id="app">
    
    <!-- 在子组件中绑定一个自定义属性, 把msg传递给子组件 -->
    <mycom :parentmsg="msg"></mycom>
</div>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {
        msg: '123, 这是父组件中的值'
      },
      methods: {},
      components: {
        mycom: {
            //无法使用data中的msg
          template: '<h1>这是子组件中的值 --- {{ parentmsg }}</h1>',
            //在子组件中把父组件传递的属性,在props在定义
          props: ['parentmsg'],
          data(){
              return {
                 msg: '这是子组件自己的数据'
              }
          }
        }
      }
    })
  </script>
```





### 父组件把方法传递给子组件

父组件向子组件传递方法使用事件绑定机制`v-on:func="传递的事件"` 子组件就能够通过某种方式, 来调用父组件的传递的方法 

在子组件的模板字符串中,绑定事件, 在事件中通过`this.$emit('func')` 触发父组件传递的绑定的事件名 

```html
 <div id="app">
     <!-- 把父组件的事件传递给子组件 -->
    <mycom v-on:func="show"></mycom>
  </div>

  <template id="temp">
    <div>
        <!-- 子组件绑定事件, 触发父组件传递的事件 -->
      <button @click="emit">这是子组件</button>
    </div>
  </template>
  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
        show(data){
          alert('哈哈')
        }
      },
      components: {
        mycom: {
          template: '#temp',
          data(){
              return {
                  sonmsg: {name: '大头儿子', age: 18}
              }
          },
          methods: {
            emit(){
                //$emit('父组件传递的事件')触发
              this.$emit('func', this.sonmsg)
            }
          }
        }
      }
    })
  </script>
```



### 子组件给父组件传值

**利用父组件给子组件传递方法时, 可以传递参数, 在父组件的方法中, 拿到子组件传递的参数,并保存在自己身上**

- 在vm实例控制的区域中, 在子组件身上把父组件的事件传递给子组件
- 在子组件中, 定义方法触发父组件传递过来的事件, 触发父组件的方法时,可以传参, 这个参数就能够被父组件的方法接受到, 进而父组件能够得到子组件传递的参数

1. 组组件准备数据
2. 子组件触发一个自定义事件, 传递参数`this.$emit('自定义事件名', 参数)`

```js
this.$emit('func',[ parm1, parm2, ...])
	参数1: 在组件上绑定的属性
    参数2~: 调用父组件方法, 传递的实参 
```

```js
  <div id="app">
      
     #把父组件的方法绑定到子组件身上 
    <mycom @func="father"></mycom>
  </div>

   <template id="temp">
     <div>
       <h1>这是子组件</h1>
		
		#在子组件注册的事件中使用this.$emit('father', 传递给父组件的值)触发父组件的事件, 并且能够把值传递给父组件
       <button @click="sendFather">你长大了,要孝顺爸爸我</button>
     </div>
   </template>   


let mycom = {
      template: '#temp',
      data(){
        return {
          msg: '要孝顺爸爸'
        }
      },
      methods: {
        sendFather(){
          this.$emit('func', this.msg)
        }
      }
    }
  
    let vm = new Vue({
      el: '#app',
      data: {
        sonmsg: null
      },
      methods:{
          #在子组件调用父组件的方法时, 能够通过函数参数, 把值传递给父组件
        father(data){
          this.sonmsg = data
          console.log(this.sonmsg)
        }
      },
      components:{
        mycom,
      }
    })
```



### 组件传值案例---追加评论

```html
  <div id="app">
    <mycom @func="loadContent"></mycom>

    <ul class="list-group">
      <li class="list-group-item" v-for="item in list">
        <span class="badge">评论人:{{ item.user }}</span>
         {{ item.content }}
      </li>
    </ul>
  </div>

  <!-- 组件的模板字符串 -->
  <template id="temp">
    <div>
      <div class="form-group">
        <label for="">评论人</label>
        <input type="text" class="form-control" v-model="user">
      </div>
      <div class="form-group">
        <label for="">评论内容</label>
        <input type="text" class="form-control" v-model="content">
      </div>
      <div class="form-group">
        <input type="button" class="btn btn-success" value="发表评论" @click="publish">
      </div>
    </div>
  </template>
  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {
        //假数据
        list: [{
          id: Date.now(),
          user: '李白',
          content: '李白乘周将于性'
        }]
      },
        
      //子组件
      components: {
        mycom: {
          template: '#temp',
          data(){
            return {
              user: '',
              content: ''
            }
          },
          methods: {
            publish(){

              //从localStrorage中读取对象字符串, 如果是第一次发表则返回一个 '[]'
              var list = JSON.parse(localStorage.getItem('content') || '[]')

              //获取表单中的数据, 包装成一个对象
              var text = {id: Date.now(), user: this.user, content: this.content}

              //把表单中的数据追加到localStrorage中
              list.unshift(text)

              //把list序列化为对象字符串,在存储到localStrorage中
              localStorage.setItem('content', JSON.stringify(list))

              //清空表单
              this.user = this.content = ''

              //父组件把方法传递给子组件中, 调用
              this.$emit('func')
            }
          }
        }
      },
      created(){
        //在created生命周期函数中, 调用loadContent方法
        this.loadContent()
      },
      methods: {
        //定义一个方法,咋页面加载时,就读取localStorage中的数据
        loadContent(){
          //读取内存中的数据
          var list = JSON.parse(localStorage.getItem('content') || '[]')
          
          //用内存中的数据覆盖假数据
          this.list = list
        }
      }
    })
  </script>
```



## 单向数据流

 所有的 prop 都使得其父子 prop 之间形成了一个**单向下行绑定**：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解 

**防止父组件中的数据变化, 所有子组件的数据都跟着变化**

 额外的，每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你**不**应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告 

**总结来说:** 

**父组件的属性的变化会流动到子组件**

**子组件不能修改父组件的数据(props是只读的)** 

注意: 

props是简单数据类型, 如果传递的是复杂数据类型, 能够修改父传递的数据,并且不会报错





## 基于组件todos案例



## 非父子组件通信

### vm.$on 

A -> B 传值

1. 创建一个bus, vm实例
2. 组件A准备数据
3. 组件B使用$on在 created钩子中定义bus的自定义函数,
4. 组件A触发bus的自定义函数使用$emit触发事件, 并把值传递过去

```js
#1- 定义bus
const bus = new Vue()

Vue.component('big-son', {
      template:'#bigSon',
      methods: {
        send(e){
          this.$emit('sonwife-one', this.bigWife)
          #3-  父组件内容改变则触发定义的方法
          bus.$emit('dasao', e.target.value)
        }
      }
    })

Vue.component('small-son', {
      template: '#smallSon',
      data(){
        return {
          dasao: ''
        }
      },
      created(){
          # 2.给bus定义方法, 拿到兄弟传递的值, 在自己身上定义
        bus.$on('dasao' , data => {
          this.dasao = data
        })
      }
    })
```



# Vue 第六天



## 组件插槽

### slot 

也叫默认插槽, 匿名插槽, 适用于单个插槽

默认情况下, 没有slot, 组件内容会被忽略

在template中, 可以使用一个特殊的标签`<slot></slot>`



### 具名插槽

v-slot指令: 指定具体的插槽, 可以指定多个插槽

语法使用

```vue
<slot name="名字"></slot>

//在组件标签内部定义template
<template v-slot:title>
<p>我是标签</p>
</template>
```



### 作用域插槽

1. 在组件中的`template` 中使用`slot` 标签占位, 给`slot` 添加自定义属性
2. 所有添加的自定义属性, 都给添加到一个对象中

```js
<slot money="100" :item="item"></slot>
{ money:100, item:{} }
```

3. 在使用插槽时在`template` 中, 就可以通过`v-slot="对象"` 接收

   这个对象里的属性就是在定义插槽的时候传递的自定义属性的值

```vue
<template v-slot="obj">
<p>{{ obj.item.id }}</p>
</template>
```



带有数据的插槽

```vue
<demo>
    <template v-slot="obj">  //obj会变成一个对象, 存储数据	
		<div>
        	{{ obj.count }}
        </div>
    </template>
</demo>

//在组件的template中
Vue.component('demo', {
	template: `
	<slot :count="leftCount"></slot>
	`
})
```





## Vue中的过滤器

### **概念**

Vue.js 允许自定义过滤器，**可被用作一些常见的文本格式化**。过滤器可以用在两个地方：**mustache 插值和 v-bind 表达式**。过滤器应该被添加在 JavaScript 表达式的尾部，由管道符`|`指示

### 在差值表达式中使用

**使用moment格式化插件配合过滤器**

允许存在多个过滤器, 每一个过滤器之间中管道符`|`隔开

在渲染data中的`msg` 时, 会经过过滤器处理之后, 在渲染到页面中

```html
 <div id="app">
    <p>{{ msg | msgFormat('疯狂+1', '123') | test }}</p>
  </div>
```

**定义过滤器`Vue.filter()`**

**语法**

```js
Vue.filter('过滤器名字', function(data, [arg1, arg2....]) {})
```

```js
// 定义一个 Vue 全局的过滤器，名字叫做  msgFormat
    Vue.filter('msgFormat', function (msg, arg, arg2) {
      // 字符串的  replace 方法，第一个参数，除了可写一个 字符串之外，还可以定义一个正则
      return msg.replace(/单纯/g, arg + arg2)
    })

    Vue.filter('test', function (msg) {
      return msg + '========'
    })
```



### 过滤器-格式化时间

```js
		//全局过滤器,格式化时间
 		Vue.filter('format', function (data, data1='') {
 			var dt = new Date(data)
 			var y = dt.getFullYear()
 			var m = (dt.getMonth() + 1).toString().padStart(2, '0')
 			var d = dt.getDate().toString().padStart(2, '0')

 			//判断需要详细时间还是简略时间
 			if (data1.toLowerCase() === 'yyy-mm-dd') {
 				return `${y}-${m}-${d}`
 			} else {
                
                //使用字符串新方法, 不全字符串
 				var hh = dt.getHours().toString().padStart(2, '0')
 				var mm = dt.getMinutes().toString().padStart(2, '0')
 				var ss = dt.getSeconds().toString().padStart(2, '0')

 				return `${y}-${m}-${d} ${hh}:${mm}:${ss}` 
 			}
 		})
```



## 私有过滤器(filters)

> 在全局定义的过滤器叫做全局过滤器

私有过滤器在VM实例中定义

- 也是一个对象

**语法**

在VM实例的`filters`属性中定义

```js
filters: {
    过滤器名: function(data, [arg1, arg2...]) {
        
    }
}
```

```js
var vm = new Vue({
    el: '.app',
    data: {},
    methods: {},
    filters: {
        format: function(){}
    }
})
```

### 过滤器调用原则

**就近原则**

- 自己有的, 则调用自己的过滤器
- 如果私有过滤器和全局过滤器重名, 则采用私有过滤器











## `$refs` 获取DOM节点和组件

`ref` : 可以给任意的DOM元素和组件添加一个属性, 加了`ref`  就相当于给元素加了标记

`vm.$refs.a` 拿到这个DOM元素或者组件对象

> 组件通过`js` 获取元素的方式, 无法获取, 但是使用 `vm.$refs` 可以获取

### 获取DOM元素

在VM实例上有`$refs` 属性, 是一个对象, 这个对象上能够存储DOM元素

但是需要在元素身上添加属性`ref="引用名"`

```html
  <div id="app">
    <button @click="handle">点击触发事件</button>
    <h3 ref="msg">这是一个h3元素</h3>
  </div>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
        handle(){
          console.log(this.$refs.msg.innerText)
        }
      },
    })
  </script>
```



### 获取组件

**VM实例不仅能够获取DOM元素, 也能够获取组件,从而获取子组件中的数据和方法**

```html
  <div id="app">
    <button @click="handle">点击触发事件</button>
    <h3 ref="msg">这是一个h3元素</h3>
    <mycom ref="mycom"></mycom>
  </div>

  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
        handle(){
          // console.log(this.$refs.msg.innerText)
          console.log(this.$refs.mycom.msg)
        }
      },
      components: {
        mycom: {
          template: '<h1>这是子组件中的msg</h1>',
          data(){
            return {
              msg: '这是子组件中的msg'
            }
          }
        }
      }
    })
  </script>
```



# Vue 第七天







## [Vue 中的动画]([https://cn.vuejs.org/v2/guide/transitions.html#%E6%A6%82%E8%BF%B0](https://cn.vuejs.org/v2/guide/transitions.html#概述))

vue官网动画文档

[[https://cn.vuejs.org/v2/guide/transitions.html#%E6%A6%82%E8%BF%B0](https://cn.vuejs.org/v2/guide/transitions.html#概述)]([https://cn.vuejs.org/v2/guide/transitions.html#%E6%A6%82%E8%BF%B0](https://cn.vuejs.org/v2/guide/transitions.html#概述))



### 过渡动画

- 分为两个部分, 进入部分和离开部分

  - `enter` 状态 和 `leave`

- 进入`enter`的动画

  - 两个时间点 `v-enter` `v-enter-to`

    - `enter`动画进入之前的起始状态

    - `v-enter-to` 进入之后的结束状态

  - 一个时间段`v-enter-active`  动画进入的时间段

- `leave`  离开动画
- 两个时间点

  - `v-leave ` 离开起始状态

  - `v-leave-to` 离开结束状态

- `v-leave-active` 离开时间段

![](E:\Vue\image\transition.png)

### 使用过渡类名实现动画

1. 使用transition元素, 把需要控制的元素包裹起来, `transition`  是vue官网提供的
2. 自定义两组样式, 来控制`transition` 内部的元素实现动画

```html
  <style>
    /* 定义两组动画 */
    .v-enter,
    .v-leave-to {
      opacity: 0;
      transform: translateX(100px)
    }

    .v-enter-active,
    .v-leave-active {
      transition: all 1s ease-in;
    }
  
  </style>


<div class="app">
    <!-- 使用transition包裹 -->
    <input type="button" value="toggle" @click="flag=!flag">
    <transition>
      <h1 v-show="flag">我是一个大大的h1, 我怕谁</h1>
    </transition>
  </div>

```



#### 修改动画前缀

作用

- 能够区分不同组之间的动画
- 在`transition` 中`name` 属性值为私有前缀

```html
<style>
	.other-enter,
    .other-leave-to {
      opacity: 0;
      transform: translateY(100px)
    }

    .other-enter-active,
    .other-leave-active {
      transition: all 1s ease-in;
    }
</style>

	<input type="button" value="toggle" @click="flag2=!flag2">
    <transition name="other">
      <h3 v-if="flag2">这是一个小小的h3</h3>
    </transition>
```



#### 使用css3的 animation 定义动画

1. 使用`@keyframes ` 定义动画
   - animation有一个属性 动画能够从100%到 0% 执行动画`reverse`
2. 使用`.v-enter-active` 和 `.v-leave-active` 定义进入和离开的动画



### 使用第三方animate.css实现动画

[animate.css第三方动画类库](https://daneden.github.io/animate.css/)

**自定义过渡类名**

- `enter-class` 指定进入前的类名 默认是` .v-enter`
- `enter-active-class`  指定进入的active的类名
- `enter-to-class` (2.1.8+)
- `leave-class`
- `leave-active-class`
- `leave-to-class` (2.1.8+)

> 他们的优先级高于普通的类名，这对于 Vue 的过渡系统和其他第三方 CSS 动画库，如 [Animate.css](https://daneden.github.io/animate.css/) 结合使用十分有用

**自定义类名的使用**

- 在`transition` 中添加 `enter-active-class` 和 `leave-active-class`
- 动画类名参照`animate` 官方文档
- 基础类`animated` 可以放在`transition`身上,也可以放在做动画的元素身上
- `:duration="{}"`  设置动画入场和立场的时间
  - 可以传一个对象, 设置入场和离开的时间

```html
<link rel="stylesheet" href="./lib/animate.css">

<div class="app">
    <input type="button" value="toggle" @click="flag=!flag">
    <transition enter-active-class="animated bounceIn" leave-active-class="animated bounceOut" :duration="{enter: 400, leave: 600}">
      <h1 v-show="flag" class="animated">我是一个大大的h1</h1>
    </transition>
  </div>
```



### 使用钩子函数实现半场动画

对于半场动画, 过渡类名和第三方类名都无法实现

**声明钩子函数**

- 动画钩子函数的第一个参数：el，表示 要执行动画的那个DOM元素，是个原生的 JS DOM对象
- `beforeEnter(el){}`, 表示动画入场之前, 此时动画还未开始, 可以在这个钩子中设置动画开始的样式
- `enter(el,done){}`  表示动画结束的状态(样式)
- `afterEnter(el){}` 表示动画完成之后的状态, 动画完成之后会调用`afterEnter`

```html
<transition
  /*入场的钩子函数 */        
  v-on:before-enter="beforeEnter" //能够设置每一次动画开始的位置
  v-on:enter="enter"
  v-on:after-enter="afterEnter"
  v-on:enter-cancelled="enterCancelled"

    /*离场的钩子函数 */          
  v-on:before-leave="beforeLeave"
  v-on:leave="leave"
  v-on:after-leave="afterLeave"
  v-on:leave-cancelled="leaveCancelled"
>
  <!-- ... -->
</transition>

<script>
	var vm = new Vue({
        methods: {
            beforeEnter(el) {},
            enter(el, done) {
                ...
                done()
            },
            afterEnter(el) {}
        }
    })

</script>
```



**模拟半场动画小球案例**

```html
  <div class="app">

    <input type="button" value="动画跑起来" @click="flag=!flag">

    <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    >
      <div class="ball" v-show="flag"></div>
    </transition>

  </div>

  <script>
    var vm = new Vue({
      el: '.app',
      data: {
        flag: false 
      },
      //动画的钩子函数在methods中
      methods: {
        //动画的钩子函数都有一个原生JS对象el
        beforeEnter(el) {
          //动画开始之前的状态
          el.style.transform = 'translate(0, 0)'
        },
        enter(el, done) {
          // el.offset系列能够让元素具有动画效果
          // 这句话，没有实际的作用，但是，如果不写，出不来动画效果；
          // 可以认为 el.offsetWidth 会强制动画刷新
          el.offsetTop

          el.style.transition = 'all 1s ease'
          el.style.transform = 'translate(300px, 500px)'

          // done() 就是afterEnter函数的调用
          done()
        },
        afterEnter(el) {
          this.flag = !this.flag
        }
      }
    });
    
  </script>
```





### 动态为列表设置动画

- 当动画为多个,列表的时候, 就不能再使用`transition` 组件包裹, `transition` 只能为单个元素绑定动画

- 需要使用`transition-group` 组件包裹要`v-for` 循环创建的元素
  - `transition-group` 默认渲染为`span`
  - `tag="ul" ` 能够指定`transition-group` 渲染为`ul` 元素
- 为列表, 定义一组动画
- `.v-move`  和 `.v-leave-active` 配合使用, 能够实现后续元素, 渐渐的飘上来的效果

- `transition-group`属性 添加`appear`  入场的效果

```html
  <style>
  
  li {
      border: 1px dashed #999;
      margin: 5px;
      line-height: 35px;
      padding-left: 5px;
      font-size: 12px;
      width: 100%;
    }

    .v-enter,
    .v-leave-to {
      opacity: 0;
      transform: translate(0px, 80px);
    }

    .v-enter-active,
    .v-leave-avtive {
      transition: all 1s;
    }
    

    /* 为删除之后, 后续列表元素重新渲染添加动画 */
    .v-move {
      transition: all 1s;
    }
    .v-leave-active {
      position: absolute;
    }
  </style>
  <div class="app">

    <label for="">
      Id: <input type="text" v-model="id">
    </label>

    <label>
        Name: <input type="text" v-model="name">
      </label>

      <input type="button" value="添加" @click="add">
    <!--<ul>-->
      <transition-group appear tag="ul">
        <li v-for="(item, i) in list" :key="item.id" @click="del(i)">
          {{ item.id }} --- {{ item.name }}
        </li>
      </transition-group>
    <!--</ul>-->

  </div>
  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '.app',
      data: {
        id: '',
        name: '',
        list: [
          {id: 1, name: '赵高'},
          {id: 2, name: '李斯'},
          {id: 3, name: '韩非子'},
          {id: 4, name: '荀子'},
        ]
      },
      methods: {
        add() {
          this.list.push({id: this.id, name: this.name})
        },
        del(i) {
          this.list.splice(i, 1)
        },
      },
    });
  
  </script>
```



## 自定义指令

[Vue自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

#### **语法**		

```js
Vue.directive('指令名', {})
```

#### **参数**

- 参数1 :  指令名, 不需要带`v-`  前缀,Vue会自动添加前缀
- 参数2 :  是一个对象, 这个对象身上有一些指令相关的函数, 这些函数会在特定的阶段, 执行相应的操作

#### 5个钩子函数

**前三个较为常用**

- `bind`  : 绑定指令
  - 触发时机 : 当指令绑定到元素上,  在内存中, 会立即执行bind函数 , 只执行一次
  - 和样式相关的操作, 一般都可以在`bind` 中执行
- `inserted`
  - 触发时机 : 元素插入到`DOM` 树中,页面中已经显示,  执行`inserted` 函数, 只执行一次
  - 有关JS行为相关的操作最好在`inserted`中执行
- `update` 

  - 触发时机: 指令的值发生改变的时候
- `componentUpdated` 
  - 触发时机 : 整个组件都更新完成的时候
- `unbind`
  - 触发时机: 指令与DOM元素解绑的时候触发

```js
Vue.directive('focus', {
     // 每当指令绑定到元素上的时候，会立即执行这个 bind 函数，只执行一次
    // 注意： 在每个函数中，第一个参数，永远是 el ，表示 被绑定了指令的那个元素，这个 el 参数，是一个原生的JS对象
      bind: function (el) {
        // 在元素 刚绑定了指令的时候，还没有 插入到 DOM中去，这时候，调用 focus 方法没有作用
        //  因为，一个元素，只有插入DOM之后，才能获取焦点
        // el.focus()
      },
    
     // inserted 表示元素 插入到DOM中的时候，会执行 inserted 函数【触发1次】
      inserted: function (el) { 
        el.focus()
      // 和JS行为有关的操作，最好在 inserted 中去执行，放置 JS行为不生效
      },
    
    // 当VNode更新的时候，会执行 updated， 可能会触发多次
      updated: function (el) {  

      }
    })

// 自定义color指令
 		Vue.directive('color', {
 			bind: function (el, binding) {
 				el.style.color = binding.value
 			}
 		})
```



#### 钩子函数的参数

- `el`：指令所绑定的元素，可以用来直接操作 DOM 。

- `binding`

  ​	**一个对象，包含以下属性：**

  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数, 可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。


**后面两个基本用不到**

- `vnode`：Vue 编译生成的虚拟节点。移步 [VNode API](https://cn.vuejs.org/v2/api/#VNode-接口) 来了解更多详情。

- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

> 除了 `el` 之外，其它参数都应该是只读的，切勿进行修改。如果需要在钩子之间共享数据，建议通过元素的 [`dataset`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/dataset) 来进行。



#### v-text实现原理

```js
<h3 v-mytext.bold="msg"></h3>  

Vue.directive('mytext', function (el, binding) {
      el.innerText = binding.value
      if (binding.modifiers.bold) {
        el.style.fontWeight = "700"
      }
    })
```

#### v-bind实现原理

```js
<h3 v-mybind:class="show">{{msg}}</h3>  

Vue.directive('mybind', function(el, binding) {
      console.log(binding)
      if (binding.arg) {
        el.setAttribute(binding.arg, binding.value)
      }
    })
```

#### v-on实现原理

```js
    Vue.directive('myon', (el, binding) => {
      console.log(binding.arg)
      if (binding.arg) {
        el.addEventListener(binding.arg, binding.value)
      }
    })
```





### 私有(局部)自定义指令

在`VM` 实例中的`directive`  属性中定义的指令

```js
 <h3 v-color="'pink'" v-fontstyle="'italic'">{{ dt | format }}</h3>

var vm = new Vue({
    el: '.app',
    directives: {
       'fontweight': {
          bind: function (el, binding) {
               el.style.fontWeight = binding.value
          }
       } 
    }
})
```



### 自定义指令简写

**在很多时候，你可能想在 `bind` 和 `update` 时触发相同行为，而不关心其它的钩子。比如这样写:**

> 把对象可以简写成一个函数, 这个函数会在`bind`  和 `update` 中都写一份

```js
Vue.directive('color-swatch', function (el, binding) {
  el.style.backgroundColor = binding.value
})
```



## 单页应用程序 SPA

### SPA-单页应用程序

一个应用只有这一个页面

网易云音乐

**优点**

1.  用户体验好，快，内容的改变不需要重新加载整个页面，基于这一点spa对服务器压力较小 
2.  前后端分离 , 前端做的更多, 后面做的更少

**缺点**

1. 开发成本高(需要学习路由) vue-router  react-router
2. 不利于SEO优化
3.  初次加载时耗时多 

<img src="E:\Vue\image\单页面.png" alt="size" style="zoom:30%; height: 30%" />



## Vue中的路由

### 什么是路由

**后端路由**

对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源

**前端路由hash**

1. 对于单页面应用程序来说，主要通过URL中的hash(#号)来实现不同页面之间的切换，同时，hash有一个特点：HTTP请求中不会包含hash相关的内容；所以，单页面程序中的页面跳转主要用hash实现；
2. 在单页面应用程序中，这种通过hash改变来切换页面的方式，称作前端路由（区别于后端路由）

相关博客 : [URL中的hash（井号）](http://www.cnblogs.com/joyho/articles/4430148.html)



### 路由的两种模式

hash 和 history

**hash** —— 即地址栏 URL 中的 `#` 符号（此 hash 不是密码学里的散列运算）。
比如这个 URL：`http://www.abc.com/#/hello`，hash 的值为 `#/hello`。它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。



**history** —— 利用了 HTML5 History Interface 中新增的 `pushState()` 和 `replaceState()` 方法。（需要特定浏览器支持）
这两个方法应用于浏览器的历史记录栈，在当前已有的 `back`、`forward`、`go` 的基础之上，它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求



 一般场景下，hash 和 history 都可以，除非你更在意颜值，`#` 符号夹杂在 URL 里看起来确实有些不太美丽 



> `history `模式优点: 地址栏没有丑陋的 `#`
>
> 缺点: 需要后端[配合, 因为我们是单页面, , 后端收到任何请求地址, 都返回 index.html

### [Vue中的路由vue-router](https://router.vuejs.org/zh/)

#### 下载安装

直接下载[下载地址](https://unpkg.com/vue-router/dist/vue-router.js)

#### 引入

```html
<script src="/path/to/vue.js"></script>
<script src="/path/to/vue-router.js"></script>
```

#### 路由的基本使用

1. 引包
   - vue-router需要在vue之后引入
   - 引包之后, window身上就多了一个构造函数`VueRouter` 能够new 路由规则对象
2. 创建路由规则对象
   - `routes` 是一个数组, 是路由匹配规则, 必须有两个属性`path` 和 `component`
   - 属性1`path` 监听哪个路由链接地址
   - 属性2`component` 路由是`path`匹配到的地址则展示对应的组件, `component`的值必须是组件模板对象
3. 路由规则对象`routerObj`和`vm`实例关联
   - vm实例有一个`router`属性, 值是路由规则对象`routerObj` 
   - `router`属性能够监听地址栏的变化
4. 配置路由出口`router-view`
   - `<router-view>`能够显示对应的组件, 是一个占位符

**路由规则匹配过程**

1. 点击a链接后, 地址栏发生变化, vm实例`router`属性能够监听地址栏的变化
2. 路由规则对象, 会查找路由规则`routes`中`path` 有没有符合规则的`path` 有则展示对应的组件模块

```html
<div id="app">
    <a href="#/login">登录</a>
    <a href="#/register">注册</a>
    <router-view></router-view>
  </div>

  <script src="./lib/vue-2.4.0.js"></script>
  <script src="./lib/vue-router.js"></script>
  <script>

    var login = {
      template: '<h1>这是登录组件</h1>'
    }
    var register = {
      template: '<h1>这是注册组件</h1>'
    }

    // 引包之后, window身上就有VueRouter构造函数,可以new
    var routerObj = new VueRouter({
      //routes是路由匹配规则
      routes: [
        //path: 是匹配的路径, component是组件 , 值是组件模板对象, 不是组件名称
        {path: '/login', component: login},
        {path: '/register', component: register}
      ],
    })
    
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      //vm实例上有router属性, 能够把VueRouter实例和vm实例关联起来
      router: routerObj,
    })
  </script>
```



### router-link

是vueRouter提供的一个html标签, 能够替代a标签

- `tag="div"` 属性能够把便签解析成指定的html标签

```html
	<div id="app">
	<!--<a href="#/login">登陆</a>
		<a href="#/register">注册</a> -->
		<router-link to="/login" tag="span">登陆</router-link>
		<router-link to="/register">注册</router-link>
		<router-view></router-view>
	</div>
```



### 当前导航高亮

router-link不仅会渲染成a链接, 而且会给当前的匹配的路由添加类名`router-link-exact-active router-link-active`

`router-link-exact-active`: to属性必须和地址栏的地址完成一样, 才会加上这个类 -> **精确匹配**

`router-link-active`: router-link的to属性包含在地址栏中, 就会加上这个类 -> **模糊匹配**

注意: 

1. 但凡遇到`/`的路由, 可以给`<router-link to="/" exact >` 加上`exact` 精确匹配

**2. 修改路由默认路由类名linkActiveClass, linkExactActiveClass**

默认展示的路由都会添加一个默认类名 : ` router-link-active ` 

 设置链接激活时使用的 CSS 类名。默认值可以通过路由的构造选项 `linkActiveClass` 来全局配置。 

```js
let router = new VueRouter({
    routes: [],
    linkActiveClass: 'myClass'
})
```





### 页面路由重定向redirect

能够指定访问根路径, 重定向地址的hash值, 为`/login`

跟后端`node`中的`redirect`完全不是一回事, node中的redirect是服务器重定向

```js
		let routerObj = new VueRouter({
			routes: [
            //指定跟路径展示, 指定的组件    
			{path: '/', redirect: '/login'},
                
			{ path: '/login', component: login },
			{ path: '/register', component: register }
			]
		})
```



### 声明式导航和编程式导航

声明式导航: 使用`router-link` 即可

编程式导航: 可以通过JS的方式实现路由的跳转

在VM实例中有一个`vm.$router.push('/home')` 能够跳转到对应的组件





### 在路由中使用动画

把路由容器使用`transition` 占位符包裹即可

```html
 <style>
  .myclass {
    font-size: 30px;
    color: pink;
  }
  .v-enter, .v-leave-to {
    opacity: 0;
    transform: translateY(100px);
  }
  .v-enter-active,
  .v-leave-active {
    transition: 1s;
  }
</style>	 

<div id="app">
    <router-link to="/login" tag="span">登陆</router-link>
    <router-link to="/register" tag="span">注册</router-link>
    <transition mode="out-in">
      <router-view></router-view>
    </transition>
 </div>
```



## 动态路由匹配

在配置我们的路由规则的时候, path可以不用写死, 可以在配置路由规则时, 使用动态路由参数

```js
const router = new VueRouter({
  routes: [
    // 动态路径参数 以冒号开头
    { path: '/user/:id', component: User }
  ]
})
```



### 路由规则-路由传参二 params

在路由地址中可以不使用查询字符串,  在vm实例中的`$route`对象中的 `params` 对象中存储了路由地址传递的参数

```js
  <div id="app">
      
     //在路由地址中可以使用这种方式
    <router-link to="/login/10/ls" tag="span">登陆</router-link>
    <router-link to="/register" tag="span">注册</router-link>
    <transition mode="out-in">
      <router-view></router-view>
    </transition>
  </div>

    let login = {
      template: '<h1>这是一个登陆路由 --- {{ $route.params.id }} --- {{ $route.params.name 						}}</h1>',
      created(){
          console.log(this.$route.params) //  {id: 10, name: ls}
      }  
  },
    
      #修改路由匹配规则
      let routerObj = new VueRouter({
     	 routes: [
      	{ path: '/login/:id/:name', component: login },
      	{ path: '/register', component: register }
      	]
    })
```



### 路由规则-路由传参一 query

在VM实例和组件对象中都有一个`$route` 对象, 这个对象存储了地址栏的相关信息, `query` 也是一个对象, 存储了地址栏`?`后面的内容

在router-link中的跳转路由地址中传参

```html
  <div id="app">
    <!-- 在router-link中的跳转路由地址中可以传参, 传一个查询字符串 -->
    <router-link to="/login?id=10&name=zs" tag="span">登陆</router-link>
    <router-link to="/register" tag="span">注册</router-link>
    <transition mode="out-in">
      <router-view></router-view>
    </transition>
  </div>

<script>
let login = {
    // this可以省略
   template: '<h1>这是一个登陆路由 --- {{ $route.query.id }} --- {{ $route.query.name }}				  </h1>',
     created(){
        console.log(this)
      }
    }
</script>
```



### 动态路由参数带来的问题

多个路由共用一个组件, 当我们根据动态路由参数发送ajax, 拿数据渲染页面, 但是动态路由参数变了, created只会执行一次, 导致路由变化的时候, 不会重复的渲染

解决方案: 使用watch 侦听属性, 监听路由的变化

vm实例`this.$route`上记录了, 路由相关信息, `path`属性是路由地址

```js
      watch: {
        // 监听路由
        '$route.path': function (newVal, oldVal) {
          if (newVal === '/login'){
            console.log('欢迎来到登录页面')
          } else {
            console.log('欢迎来到注册页面')
          }
        }
      }
```





## $router 和 \$route

$router: 是整个路由实例,  整个项目就一个路由实例, 并且有一些方法, push, splice 等能够使用编程式导航

$route:也是一个对象,  是当前路由规则, 能够获取**当前的路由信息, 是根据当前的路由的变化而变化**, **也就是地址栏`#` 后面的部分(不包括#号)**

query和params等动态路由参数

fullpath: 完整的路径, 不包括#号

path:  路径, 不包括 ? 后面的值

query: 查询字符串

params: 获取 : 号后面的值



### keep-alive 面试题

 `keep-alive` 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染 

```js
<keep-alive>
  <component>
    <!-- 该组件将被缓存！ -->
  </component>
</keep-alive>
```



配合 router-view

 `router-view` 也是一个组件，如果直接被包在 `keep-alive` 里面，所有路径匹配到的视图组件都会被缓存 

```js
<keep-alive>
    <router-view>
        <!-- 所有路径匹配到的视图组件都会被缓存！ -->
    </router-view>
</keep-alive>
```



## 路由嵌套

**在路由规则routes中, 有children属性能够写子路由的路由匹配规则** 

**在父路由组件中可以嵌套子路由组件**

- 在子路由匹配规则中不能带 `/,` 带` / `则认为是根路由

```js
  <div id="app">  
    <router-link to="/account">Account</router-link>
    <router-view></router-view>
  </div>

  <template id="temp">
    <div>
      <h1>这是account的组件</h1>
      <router-link to="/account/login">登录</router-link>
      <router-link to="/account/register">注册</router-link>
      <router-view></router-view>
    </div>
  </template>


//父组件
    let account = {
      template: '#temp'
    }

    let login = {
      template: '<h3>这是登录</h3>'
    }
    let register = {
      template:'<h3>这是注册</h3>'
    }
    // 路由实例
    let router = new VueRouter({
      routes: [
        #在路由规则中, 有children属性能够写子路由的路由匹配规则  
        {
          path: '/account',
          component: account,
          # 在子路由匹配规则中不能带 /, 带 / 则认为是根路由
          children: [
          {path: 'login', component: login},
          {path: 'register', component: register}
          ]
        }
      ]
    })

    //vm实例
    let vm = new Vue({
      el: '#app',
      router,
    })
```





## 命名视图实现经典布局

默认情况下, 在一条路由规则下只能显示一个路由组件, 可以通过把`component` 改写成一个对象`components:{}` 属性值作为`router-view`的name属性值, 进而在一条路由规则中显示不同的路由组件 

```js
  <style>
    body, html {
      margin: 0;
    }
    .header {
      margin: 0;
      height: 100px;
      background-color: lightgreen;
      width: 100%; 
    }
    .container {
      display: flex;
      height: 600px;
    }
    .left {
      flex: 2;
      background-color: lightseagreen;
    }
    .main {
      flex: 8;
      background-color: lightpink;
    }
  </style>

  <div id="app">
	
    #根据路由规则routes, 默认显示default的组件, 可以给router-view指定name值, 显示指定的路由组件
    <router-view></router-view>
    <div class="container">
      <router-view name="left"></router-view>
      <router-view name="main"></router-view>
    </div>
  </div>


    let header = {
      template: '<h1 class="header">这是头部</h1>'
    }

    let left = {
      template: '<div class="left">这是左边侧边栏</div>'
    }

    let main = {
      template: '<div class="main">这是主体部分</div>'
    }

    let router = new VueRouter({
      routes: [
        {
          path: '/',
            
          #如果想要在这一条路由规则中显示多个组件, 则可以把components变成一个对象指定router-view的				name值  
          components: {
            default: header,
            left: left,
            main: main
          }
        }
      ]
    })

    let vm = new Vue({
      el: '#app',
      router,
    })
```



## 导航守卫

 正如其名，`vue-router` 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。有多种机会植入路由导航过程中：全局的, 单个路由独享的, 或者组件级的 

### 全局前置守卫







# Vue 第八天



## `nrm`

### 什么是nrm

提供了一些最常用的NPM包镜像地址，能够让我们快速的切换安装包时候的服务器地址；**不是一个装包工具**

什么是镜像：原来包刚一开始是只存在于国外的NPM服务器，但是由于网络原因，经常访问不到，这时候，我们可以在国内，创建一个和官网完全一样的NPM服务器，只不过，数据都是从人家那里拿过来的，除此之外，使用方式完全一样

> 注意： nrm 只是单纯的提供了几个常用的 下载包的 URL地址，并能够让我们在 这几个 地址之间，很方便的进行切换，但是，我们每次装包的时候，使用的装包工具，都是  npm

### 安装nrm

```shell
$ npm i -g nrm
```

### 切换镜像下载地址

```shell
$ nrm use taobao(npm/ cnpm/ ...)
```

### 查看镜像切换地址

```shell
$ nrm ls
```



## webpack

### 什么是webpack

**是一个模块打包器, 多个文件导包成一个文件, 并且能顾进行语法的转换**

webpack是前端项目构建工具, 是基于nodejs开发出来的前端工具

### webpack的作用

**语法转换**

sass/scss/less/stylus: css预处理器 --> 转成css文件

typescript ---> JS 文件

Es6+的语法 ---> ES3/5语法

**打包文件**

对文件进行压缩 合并 混淆



**提供一个开发环境**

1. 自动打开浏览器
2. 监听文件的变化, 自动刷新浏览器



总结: webpack在开发的时候回使用到, 而且扎起项目上线之前, 都会使用webpack进行打包处理, 在上线

在项目上线的环境中, 不会用到webpack

**webpack是一个模块打包器**

1. 在wenpack中所有的资源都是资源, (JS/ css/ 图片等)
2. webpack兼容所有模块化语法
   - 浏览器端模块化规范 : AMD CMD 
   - 服务器端模块化规范: CommonJS  nodejs require 

### 在网页中常见的静态资源？

+ JS
  - .js  .jsx  .coffee  .ts（TypeScript  类 C# 语言）
+ CSS
  - .css  .less   .sass  .scss
+ Images
  + .jpg   .png   .gif   .bmp   .svg
+ 字体文件（Fonts）
  - .svg   .ttf   .eot   .woff   .woff2
+ 模板文件
  - .ejs   .jade  .vue【这是在webpack中定义组件的方式，推荐这么用】

### 网页引入静态资源过多带来的问题

- 网页加载速度慢,  需要发很多二次请求
- 要处理错综复杂的依赖关系

### 如何解决上述两个问题

1. 合并、压缩、精灵图、图片的Base64编码
2. 可以使用之前学过的requireJS、也可以使用webpack可以解决各个包之间的复杂依赖关系；



### 如何完美实现上述的2种解决方案

1. 使用Gulp， 是基于 task 任务的；(地球上的珠穆朗玛峰)
2. 使用Webpack， 是基于整个项目进行构建的 , 适用于大型项目( 地球周边的卫星 )

+ 借助于webpack这个前端自动化构建工具，可以完美实现资源的合并、打包、压缩、混淆等诸多功能。
+ 根据官网的图片介绍webpack打包的过程



## webpack使用

**一般在项目中使用**

### 基础使用

1. 初始化项目

```shell
yarn init -y  #生成package.json文件
```

2. 安装依赖包

```shell
yarn add webpack webpack-cli -D
```

3. 在package.json文件中`"scripts": {}`配置一条命令

```js
//使用webpack对main.js进行打包, 打包到dist/bundle.js
"scripts": {
    "build": "webpack"
    //"build": "webpack --config webpack.config.js" //能够指定配置文件
}
```

4. 准备配置文件

```js
    // 导入处理路径的模块
    var path = require('path');

    // 导出一个配置对象，将来webpack在启动的时候，会默认来查找webpack.config.js，并读取这个文件中导出的配置对象，来进行打包处理
    module.exports = {
        //path.join()也可以
        entry: path.resolve(__dirname, 'src/js/main.js'), // 项目入口文件
        output: { // 配置输出选项
            path: path.resolve(__dirname, 'dist'), // 配置输出的路径
            filename: 'bundle.js' // 配置输出的文件名
        },
        // webpack 4X之后, 需要指定告知 webpack 使用相应模式的内置优化 production:生产环境
         mode: 'development'
    }
```

5. 运行命令打包

```js
//yarn 命令 或者 npm run 命令
yarn build 
npm run build
```



#### npm install 详解

```js
//本地安装包
npm i 包名 -S   // -S === --save 安装的包会记录到dependencies  现在的npm 默认使用 --save
//本地安装包
npm i 包名 --save-dev  // 简写 -D 包会记录到 devDependencies中 安装的包在开发阶段中使用到的, 项目中的包用到用 -S  例如: wenpack gulp less scss 等开发阶段中使用
```

#### yarn add 详解

```js
//yarn add 安装包也支持这些参数, 但是只支持简写 -S -D 等
```



#### package.json中scripts详解

scripts: 可以用来配置一些命令脚本

```json
//配置
"scripts": {
    "aa": "yarn add jquery"
}
//使用
npm run 命令 //如果命令是start 和 stop 可以省略
//npm run start  其实就是在package.json中配置一条命令 "start": "node app.js"
```



### 安装webpack

学习版本 `webpack`

1. 运行`npm i webpack -g`全局安装webpack，这样就能在全局使用webpack的命令
2. 在项目根目录中运行`npm i webpack --save-dev`安装到项目依赖中



### 使用webpack构建项目

**建立一个项目根目录** `webpack-item`

**创建目录**

- `src` -> 放js, css, iamges, index.html 等代码
- `dist ` -> 存放项目的成功的文件

**初始化`npm init -y`**

**下载`jquery`**

```shell
$ 在webpack-item目录下
$ npm i jquery@1.12.4 
```



**准备`index.html`**

在src目录下创建index.html,  不推荐引入各种js, css文件



**准备main.js**

在src目录下创建main.js , 作为项目的 JS入口文件

`import  ** from **` 是ES6 中导入模块的方式

```js
//浏览器无法解析这行代码
import $ from 'jquery'
```



**使用webpack处理`main.js`**

```shell
$ webpack .\src\main.js .\dist\boundle.js
```

webpack打包语法

```shell
$ webpack 要打包的文件路径  打包好输出的文件路径
```



**在`index.html ` 中引入`bundle.js`**



**webpack做了什么事情**

`webpack` 能够解决文件之间的互相依赖关系, 在主页面中, 我们只主要引入一个文件`bundle.js` 即可

webpack能够处理JS兼容性问题, 把浏览器不识别的语法, 转为低级的, 浏览器识别的语法



### webpack基本配置

虽然可以在package.json中年配置webpack, 但是webpack的配置太多了, 可以抽离出去为一个配置文件

在项目根路径下, 建一个`webpack.config.js` 的webpack的配置文件, 因为webpack是node开发的, 完全支持node语法, **有个配置文件, 就可以在控制直接输入`webpack` 就可以打包入口JS文件**

```js
    // 导入处理路径的模块
    var path = require('path');

    // 导出一个配置对象，将来webpack在启动的时候，会默认来查找webpack.config.js，并读取这个文件中导出的配置对象，来进行打包处理
    module.exports = {
        //path.join()也可以
        entry: path.resolve(__dirname, 'src/js/main.js'), // 项目入口文件
        output: { // 配置输出选项
            path: path.resolve(__dirname, 'dist'), // 配置输出的路径
            filename: 'bundle.js' // 配置输出的文件名
        },
        // webpack 4X之后, 需要指定告知 webpack 使用相应模式的内置优化 production:生产环境
         mode: 'development'
    }
```



**在控制台执行`webpack` 命令时, 做的几件事情**

- 首先, webpack发现我们没有以命令的形式给他指定入口和出口
- webpack就会去项目的根目录找`webpack.config.js` 配置文件
- 然后解析配置文件,解析完配置文件之后, 就得到了配置文件中导出的配置对象
- 当webpack的到了配置对象, 就知道了入口和出口, 就进行打包构建





## `html-webpack-plugin`插件配置启动页面

 [https://www.webpackjs.com/plugins/html-webpack-plugin/#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95](https://www.webpackjs.com/plugins/html-webpack-plugin/#基本用法) 

**作用:** 

1. 会把我们的index.html也生成到dist文件夹中
2. 在内存中根据模板页面 , 生成一份
3. 自动把`bundle.js`  引入到页面, 不需要引入物理磁盘中的`bundle.js`

由于使用`--contentBase`指令的过程比较繁琐，需要指定启动的目录，同时还需要修改index.html中script标签的src属性，所以推荐大家使用`html-webpack-plugin`插件配置启动页面.

**使用配置:**

1. 运行`cnpm i html-webpack-plugin --save-dev`安装到开发依赖
2. 修改`webpack.config.js`配置文件如下：

```js
    // 导入处理路径的模块
    var path = require('path');
    // 导入自动生成HTMl文件的插件
    var htmlWebpackPlugin = require('html-webpack-plugin');

    module.exports = {
        entry: path.resolve(__dirname, 'src/js/main.js'), // 项目入口文件
        output: { // 配置输出选项
            path: path.resolve(__dirname, 'dist'), // 配置输出的路径
            filename: 'bundle.js' // 配置输出的文件名
        },
        plugins:[ // 添加plugins节点配置插件
            new htmlWebpackPlugin({
                template: path.resolve(__dirname, 'src/index.html'),//模板路径
                filename: 'index.html'//自动生成的HTML文件的名称
            })
        ]
    }
```

3. 修改`package.json`中`script`节点中的dev指令如下：

```
"dev": "webpack-dev-server"
```

4. 将index.html中script标签注释掉，因为`html-webpack-plugin`插件会自动把bundle.js注入到index.html页面中！





## loader加载器处理配置css样式表

**webpack默认只能够打包处理JS文件, 无法处理其他类型的文件,想要处理非JS文件, 需要手动安装一些第三方loader加载器**

**webpack的配置文件中`module` 用于配置所有第三方模块加载器**

**rules处理所有第三方模块匹配规则,** 当webpack在打包的时候遇到css的文件, 不认识时不会直接报错, 而是去配置文件的module的`rules` 中查看有没有能够匹配的规则

### 打包处理css文件

1. 需要安装 `style-loader` 和 `css-loader` 这两个加载器

```shell
$ npm i style-loader css-loader -D
```

2. 在`webpack.config.js` 配置对象中, 新增一个配置节点`module` , 它是一个对象, 这个对象上有一个`rules` 属性, 是一个数组, 这个数组中存放了, 所有第三方文件的匹配和处理规则

**注意点: loader的处理顺序从后往前处理, 所以`use: ['style-loader', 'css-loader'] ` 顺序不能变**

```js
module: { // 用来配置第三方loader模块的
        rules: [ // 文件的匹配规则
            { test: /\.css$/, use: ['style-loader', 'css-loader'] }//处理css文件的规则
        ]
    }
```

**webpack 处理第三方文件类型的过程:**

1. 当要处理的文件呢不是js文件时, 就回去配置文件中查找有没有对应的第三方 loader 规则
2. 如果有对应的第三方规则, 就会调用对应的loader去处理这种文件类型
3. 在调用loader时, 是**从后往前调用的**
4. 当最后一个loader调用完毕, 会把处理的结果交给webpack进行打包合并, 最终输出`bundle.js`中 



## loader处理less, sass文件

### 导入less. scss文件

```js
import './src/css/index.less'
import './src/css/index.scss'
```

### 安装loader

```shell
$ npm i less-loader sass-loader -D
## less-loader 内部依赖less
$ npm i less -D
## sass-loader 内部依赖node-sass
$ npm i node-sass -D
```

### 定义匹配规则

```js
  module: {
    rules: [
      //配置处理css文件
      {test: /\.css$/, use: ['style-loader', 'css-loader']},
      // 配置处理less文件
      {test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader']},
      //配置sass匹配规则
      {test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader']}
    ]
  }
```





## url-loader和 file-loader

**file-loader**

我们在css中使用图片, 字体图标等, webpack默认也是无法处理的, 需要`file-loader` 或者 `url-loader`

`file-loader` 能够打包各种文件类型, 它**不能**把图片等文件打包到`main.js` 中

`url-loader` 也能够处理文件, 并且**能**够打包文件到入口文件`main.js`中



**url-loader**

 `url-loader` 功能类似于 [`file-loader`](https://github.com/webpack-contrib/file-loader)，但是能够控制打包到`bundle.js`的文件的大小 , 可以返回一个 DataURL。

-  能够将文件打包到`bundle.js` 并且转成base64编码格式的, base64格式文件大小会放大30%左右

- 默认情况下, webpack无法处理css文件中的url地址, 即使有`css-loader style-loader` 也是无法处理url地址的

需要借助第三方插件处理url路径`url-loader`

注意: `url-loader` 内部依赖`file-loader` 

### 安装插件

```shell
$ npm i url-loader file-loader -D
```

### 图片文件路径规则

- **loader可以传参 ,传参方式和url地址完全一样**但是参数是固定的

- `limit` 是 给定的值, 是图片的大小, 单位是byte, 如果图片大于或等于给定的limit值, 则不会被转为base64格式的字符串地址, 大于`litmit` 会把图片交给`file-loader` , 小于给定的`litmit` 会打包到`bundle.js` 中

   如果小于limit的值 , 则会转成base64格式的字符串地址

- `name` 默认图片的路径地址会被转成不重复的地址, name属性能够让webpack不转地址, 原名输出地址
  
  - `[hash:8]-[name].[ext]` 会在图片地址不转的前提下加上8位的hash值

```js
// url-loader
{test: /\.(jpg|png|gif|jpeg|bmp|svg)$/, use: 'url-loader?limit=7686&name=[hash:8]-[name].[ext]'}

{
    test: /\.(jpg|png|gif|jpeg|bmp|svg)$/, 
    use: {
        loader: 'url-loader',
        options: {
            // 小于 8k 则打包到bundle.js中, 大于8k的图片交给file.js
            litmit: 8 * 1024 //8k
        }
    }
}

//file-loader
{test: /\.(jpg|png|gif|jpeg|bmp|svg)$/, use: 'file-loader'} //不会打包到入口js中
```



### 字体文件路径规则

子体文件也属于url-loader的处理范围, 可以使用`url-loader` 去处理

```js
{test: /\.(ttf|eot|svg|woff|woff2)/, use: 'url-loader'}
```





# Vue 第九天



## webpack-dev-server自动打包工具

能够实现自动打包编译的功能

**webpack-dev-server想要正常运行, 要求在本地项目中, 必须安装webpack**, 否则无法正常运行

**在项目中安装的不是在全局安装的, 无法在powershell运行`webpack-dev-server` 这个脚本命令**

powershell只能直接执行`-g` 全局安装的工具 

所以在`package.json` 中的`script` 属性中`"dev": "webpack-dev-server"`

用`npm run dev` 命令 代替 `webpack-dev-server` 去执行`webpack-dev-server` 这个工具

### 安装

- -S 安装到上线环境  <==> --save
- -D 安装到开发环境  <==> --save-dev
- -g 安装到全局

将webpack-dev-server安装到项目的本地开发依赖环境

```shell
$ yarn add webpack-dev-server -D
```

在package.json中配置

```json
"scripts": {
    "dev": "webpack-dev-server --open --port 3000"
}
```



### 作用

**能够自动打包编译,能够自动刷新浏览器**

> 并不会打包到物理内存中, 只会打包到内存中

webpack-dev-server会开启一个服务器, 把编译的文件托管在网站的根路径下, 而不是像webpack会编译在我们指定的目录下, 所以在页面中引入`bundle.js` 应该引入网站根路径下的`bundle.js`



`webpack-dev-server` 帮我们生成的`bundle.js` 并没有生成在电脑的物理磁盘中, **而是在电脑的内存中**, 所以我们的项目根目录中没有打包好的`bundle.js` 



我们可以认为`webpack-dev-server` 把打包好的文件以一种虚拟的形式, 托管到了咱们的项目的根目录, 和dist, src平级, 存在一个看不见的`bundle.js` 文件



**使用总结**

- webpack-dev-server非全局安装,所以在package.json的script中添加`dev: webpack-dev-server` 使用`npm run dev` 替代执行

- webpack-dev-server使用必须在本地安装webpack => `npm i webpack -D`

  - 如果是webpack 3X 就不需要单独安装`webpack-cli`
  - webpack 4X 需要单独安装`webpack-cli`

- html页面中引入`bundle.js` 需要引用内存托管在根目录的`bundle.js`  

  - <script src="/bundle.js"> 

### 常用命令

运行`webpack-dev-server` 自动打开浏览器并打开指定的端口号且打开指定目录, 在`package.json` 中设置

- `--open`  : 打开浏览器
- `--port 3000`  指定打开的端口
- `--contentBase src`  :  **设置托管目录**
- `--hot` : 热重载, 热更新, 当我们修改代码之后, 都会重新生成一个`bundle.js` , `--hot` 不会重新生成, 只会把局部修改的代码,相当于补丁, 更新原有的`bundle.js` , **而且浏览器会无刷新重载**

```js
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    //    
    #打开浏览器, 并指定端口   
    "dev": "webpack-dev-server --open --port 3000  --contentBase src --hot"
  },
```



**在package.json中配置dev-server**

上面是在`package.json` 中配置dev-server, 也可在在`webpack.config.js` 配置文件的配置对象中设置

```js
const path = require('path')
// 2- 引webpack模块
const webpack = require('webpack')


//配置文件向外暴露一个配置对象
module.exports = {
  entry: path.join(__dirname, './src/main.js'),
  output: {
    path: path.join(__dirname, './dist'),
    filename: 'bundle.js'
  },
  //webpack 4X 
  mode: 'development',
    
  // 1-  
  devServer: {
    //--open --port 3000  --contentBase src --hot
    open: true, //是否自动打开浏览器
    port: 3000, //设置运行的端口
    contentBase: 'src', // 指定托管目录
    hot: true, //启用热更新第一步 ==== 在 webpack 4.x中 这一步就可以了  
  },
  plugins: [
    // 3- 第三步
    new webpack.HotModuleReplacementPlugin(),
  ]
}
```



## babel-loader

### ES6定义类语法

- 静态属性, 挂载在类(构造函数)身上的属性, 构造函数可以` Person.info` 
- 实例属性: 挂载在实例对象身上的属性, 实例对象可以`.` 的属性

```js
class Person() {
    static info = {name:'zs', age: 18}
}

let p1 = new Person()
```



### babel

在webpack中默认只能处理一部分ES6 的新语法, 一些高级的ES6, ES7新语法, webpack是处理不了的, 这时候就需要借助第三方`loader` 去帮助`webpack` 处理这些高级语法, 第三方`loader` 处理之后, 会把结果交给`webpack` 去打包到`bundle.js` 中

**通过`babel` 可以把ES6高级语法转换成低级语法, 交给webpack**	



### 安装babel相关的包

**在webpack中可以运行两套命令安装两套包, 去安装babel相关的loader相关功能**

**babel 6**

1. 第一套  相当于babel的转换工具

```shell
$ yarn add babel-core babel-loader@7 babel-plugin-transform-runtime -D
```

2. 第二套 语法插件  preset : 语法

```shell
$ yarn add babel-preset-env babel-preset-stage-0 -D
```



**babel 7**

```shell
#babel 插件
$ yarn add @babel/core babel-loader @babel/plugin-transform-runtime -D
$ yarn add @babel/preset-env @babel/preset-stage-0 -D	

#语法插件
$ cnpm i @babel/preset-react -D
#$ cnpm i babel-preset-mobx -D

#执行命令
$ cnpm i @babel/plugin-proposal-class-properties -D
$ cnpm i @babel/runtime -D

#=======================================================================================

#简单插件配置 
$ yarn add babel-loader @babel/core @babel/preset-env -D
```



### 配置

在`webpack.config.js` 的` module`节点下的`rules`数组中, 添加一个新规则

`exclude` : 不包含的意思, 不转换`node_modules` 下的js文件, 只需要转换我们自己写的js代码即可

- 如果不排除`node_modulels` 则`babel`会把所有`node_modules` 中的所有第三方JS文件打包编译, 这样会非常消耗CPU, 同时打包速度非常慢
- 即使`babel`把 node_modules 打包编译完成, 项目也无法正常运行

```js
//
{test: /\.js$/, use: 'babel-loader', exclude: '/node_modules/'}

// 不需要.babelrc配置
  {
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['@babel/preset-env']
        }
      }
    }
```



**在项目的根目录新建一个叫`.babelrc` 的 babel配置文件, 这个文件属于JSON格式, 所以在写`.babelrc` 时必须符合JSON语法规范 : 不能写注释, 必须用双引号**

配置文件内容: 

```json
//babel 6.X
{
	# presets: 语法的意思, 以babel-presets开头的语法插件
    "presets": ["env", "stage-0"],
    
    #babel的插件, 以babel-plug开头的插件
    "plugins": ["transform-runtime"]
}

//babel 7.x
{
    "presets": ["@babel/preset-env","@babel/preset-react", ["mobx"]],
  	"plugins": ["@babel/plugin-transform-runtime","@babel/plugin-proposal-class-		  properties"]	
}
```



**安装的注意点**

`babel-loader` :已经更新到@8, 需要7.X

```js
Error: Cannot find module '@babel/core'
babel-loader@8 requires Babel 7.x (the package '@babel/core'). If you'd like to use Babel 6.x ('babel-core'), you should install 'babel-loader@7'.
```





## ES6 模块化

### import 导入

导入规则和node中的require 一样

默认的导入

1. `import './a.js'`  使用于模块没有导出, 只是加载模块的代码

精确的导入

2. `import { 变量名 } from './a.js'`  适用于模块有导出



###   export default 和 export

#### export 精确导出

- exports 向外暴露的成员必须使用 `{}` 导入
- 允许多次暴露
- import导入时, 需要的在 `{ }` 按需接收, 不需要则不定义
- `export`   到导出的成员, 在导入时, 必须严格按照导出的名称, 在 `{  }` 中按需接收
  - 但是可以起别名 , 使用`{title as title123}`

```js
# 按需导出
export var title = '小星星'
export var content = '皮皮虾'

# 统一导出
export { title, content }

#其他文件导入, 必须和导出的变量名相同
import {title as title123, content}
```







#### export default 默认导出

默认导出的成员,  在import导入时不需要使用 加`{ 精确的变量名 }`

- `  export default`向外暴露的成员, 可以`import`接收时可以定义任意变量接收 

- 只允许向外暴露一次

- 在一个模块中, 可以同时使用`export ` 和 `export default` 向外暴露成员



在node中向外暴露成员的形式

```js
module.exports = {}
```

**在es6 中也规范的定义了导入导出模块的方法**

**导入模块**

```js
import 模块名 from '模块表示符'
//导入文件
import '路径'
```

**导出模块**

```js
// ES6 中 export default 和 export向外暴露成员
export default {
    data () {
        return {
            msg: '这是.vue的data'
        }
    }
}

#其他文件导入
import mm(自定义变量名接受)
```



**使用规范**

如果使用node中的`module.exports = {}` 导出就配合使用 `require` 

如果使用ES6 中的`export default{}` 导出就使用`import ` 导入 





# git的使用

### 什么是git

> git是一个开源的, 免费的分布式的版本控制系统

版本控制系统 ( git ): 一类软件, 用于管理项目, 管理项目的代码和文档

主流的版本控制系统: 

1. git :  分布式的版本控制系统 
2. svn: 集中式的版本控制系统



### git安装

官网安装



### git使用

1. `git init`  初始化一个git的仓库

```shell
#在项目根目录
git init
```



### git的三个区

git init 之后, git 会把我们的整个项目分成是三个区

1. 工作区: 就是我们整个项目, 在里面写代码
2. 暂存区: 暂存区和仓库区都在 `.git` 隐藏文件中, `git add` 会将工作区的代码提交到暂存区
3. 仓库区: `git commit` 提交到仓库区



### git基本命令

1. `git init` : 初始化一个git仓库, 使用git命令必须有一个仓库
2. `git status` : 查看文件状态,  文件为红色, 则代表文件在工作区

```shell
git status -s  #状态简写
```

1. `git add  文件名` : 将文件添加到暂存区, 文件变成绿色

```shell
#当前目录下所有文件都添加到暂存区
git add . 
git add -A
git add --all
```

4. `git commit -m  '提交信息'` : 将暂存区的文件添加到本地仓库

```shell
#第一次提交需要git 账号, 密码, 邮箱  , 推荐用github上的   工作中公司会分配邮箱和密码, 账户
git config --global user.email 'github注册的邮箱'
git config --global user.name 'github用户名'

#提交到仓库
git commit -m '提交说明'

# 如果不写提交说明，会进入vi编辑器，没有写提交说明，是提交不成功的。 :q!
git commit   # 需要使用vi输入内容  vi编辑器常用操作

#修改最新这一次提交, 不会新增加提交, 只会修改最近一次的提交
git commit --amend -m '提交说明'

#能够跳过暂存区, 能够将工作区的文件提交到仓库区, 但是这个文件必须被提交过, 新文件不行
git commit -a -m '提交说明'
```



5. `git log` : 能够查看提交的用户和时间

```js
#提交信息很多, 一行显示
git log --online
#查看所有版本信息
git reflog 
```

6. `git reset --hard 版本号`: 版本回退, 将代码代码回退到提交的某个版本中

- `git reset --hard head~1`将版本回退到上一次提交
  - ~1:上一次提交
  - ~2:上上次提交
  - ~0:当前提交


- 当使用了`git reset`命令后，版本会回退，使用`git log`只能看到当前版本之前的信息。使用`git reflog`可以查看所有的版本信息

### git config配置

如果是第一次提交，需要配置提交者信息，推荐和github的账号邮箱一致

```Bash
# git config  user.name 你的目标用户名
# git config  user.email 你的目标邮箱名

# 使用--global参数，配置全局的用户名和邮箱，只需要配置一次即可。推荐配置github的用户名和密码
git config  --global user.name hucongcong
git config  --global user.email flycc258@163.com

# 查看配置信息
git config --list

# 取消配置
git config --unset --global user.name
git config --unset --global user.email 
```

![](./image/git01.png)

### git忽略文件

配置git忽视文件 , 在项目根目录中添加一个`.gitignore`

```js
#忽略node_modules, .gitignore不推荐忽略
node_modules
```



# git分支操作

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个平行宇宙里努力学习SVN。

如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了Git又学会了SVN！

![](image/fenzhi.png)

## 为什么要有分支？

- 如果你要开发一个新的功能，需要2周时间，第一周你只能写50%代码，如果此时立即提交，代码没写完，不完整的代码会影响到别人无法工作。如果等代码写完再提交，代码很容易丢失，风险很大。
- 有了分支，你就可以创建一个属于自己的分支，别人看不到，也不影响别人，你在自己的分支上工作，提交到自己的分支上，等到功能开发完毕，一次性的合并到原来的分支。这样既安全，又不影响他人工作。


## git分支命令

> 在git中，分支实质上仅仅是一个指针，每次代码提交后，这个分支指针就会向后移动，保证一直指向最后一次提交的的版本。git中使用HEAD指向当前分支

### 创建分支

- `git branch 分支名称`创建分支，分支中的代码，在创建时与当前分支的内容完全相同。
- git在第一次提交时，就有了一个叫`master`的主分支。
- `git branch dev`，创建了一个叫做dev的分支

### 查看分支

- `git branch`可以查看所有的分支
- 在我们第一次提交代码的时候, 会创建一个`master` 分支, 当我们直接提交会提交到`master` 分支中
- 在当前分支的前面会有一个`*`,  当前分支是绿色的
- 在git中，有一个特殊指针`HEAD`,永远会指向当前分支

### 切换分支

- `git checkout 分支名称`切换分支  HEAD指针指向了另一个分支
- 在当前分支的任何操作，都不会影响到其他的分支，除非进行了分支合并。
- 提交代码时，会生产版本号，当前分支会指向最新的版本号。

### 创建并切换分支

- `git checkout -b 分支名称` 创建并切换分支
- 切换分支会做两件事情
  - 创建一个新分支
  - 把head指针指向当前的分支

### 合并分支

- `git merge 分支名称` 将其他分支的内容合并到当前分支。
- 在`master`分支中执行`git merge dev` 将`dev`分支中的代码合并到`master`分支
- [分支合并](https://git-scm.com/book/zh/v1/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6)
- 合并到`master` 需要先切换到`master` 上

### 删除分支

- `git branch -d 分支名称` 可以删除分支
- 注意：不能在当前分支删除当前分支，需要切换到其他分支才能删除。
- 注意：`master`分支是可以删除的，但是不推荐那么做。

## git合并冲突

- 对于同一个文件，如果有多个分支需要合并时，容易出现冲突。
- 合并分支时，如果出现冲突，只能手动处理，再次提交，一般的作法，把自己的代码放到冲突代码的后面即可。
- vscode会智能提示冲突, 合并代码

手动解决: 将vscode提供的几个箭头, 删除掉, 手动调整好顺序, 在上传





# git远程仓库

## github与git

git与github没有直接的关系。

- git是一个版本控制工具。
- github是一个代码托管平台，开源社区，是git的一个远程代码仓库。

```javascript
//1. gitHub是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。
//2. github免费，代码所有人都能看到，但是只有你自己能修改。付费的可以隐藏。
//3. 创建git项目时，不能有中文。
```

[github官网](https://github.com/)

[开源中国-git](https://git.oschina.net/)

## git clone

- 作用：克隆远程仓库的代码到本地
- git clone [远程仓库地址]
- `git clone git://github.com/hucongcong/test.git`会在本地新建一个`test`文件夹，在test中包含了一个`.git`目录，用于保存所有的版本记录，同时test文件中还有最新的代码，你可以直接进行后续的开发和使用。
- git克隆默认会使用远程仓库的项目名字，也可以自己指定。需要是使用以下命令：`git clone [远程仓库地址] [本地项目名]`

> 工作中仓库地址公司提供, github账户, 密码公司提供
>
> 根据公司老大提供的仓库地址git clone 仓库地址

## git push

- 作用：将本地仓库中代码提交到远程仓库
- `git push 仓库地址 master` 在代码提交到远程仓库，注意master分支必须写，不能省略
- 例子：`git push git@github.com:hucongcong/test.git master` 如果第一次使用，需要填写github的用户名和密码

## git pull

- 作用：将远程的代码下载到本地


- 通常在push前，需要先pull一次。

`$ git pull <远程主机名> <远程分支名>:<本地分支名>`

```bash
# 获取远程仓库的更新，并且与本地的分支进行合并
git pull
```

## git remote

每次push操作都需要带上远程仓库的地址，非常的麻烦，我们可以给仓库地址设置一个**别名**

```bash
# 给远程仓库设置一个别名
git remote add 仓库别名 仓库地址
git remote add hucongcong git@github.com:hucongcong/test.git

# 删除hucongcong这个别名
git remote remove hucongcong

# git clone的仓库默认有一个origin的别名, origin的地址就是克隆的地址
```





## 推送远程仓库冲突问题

当推送同一个文件时, 发生冲突问题时, 在`git push origin mater` 之前 `git pull` 先拉取远程仓库地址更新代码, 在推送

```shell
git add .
git commit -m '提交代码'
git pull 
git push origin master
```



## SSH免密码登陆

ssh协议: 远程登录协议

git支持多种数据传输协议：

- https协议：`https://github.com/hucongcong/test.git`  需要输入用户名和密码
- ssh协议：`git@github.com:hucongcong/test.git`   可以配置免密码登录

每次push或者pull代码，如果使用https协议，那么都需要输入用户名和密码进行身份的确认，非常麻烦。

- github为了账户的安全，需要对每一次push请求都要验证用户的身份，只有合法的用户才可以push
- 使用ssh协议，配置ssh免密码，可以做到免密码往github推送代码

## SSH免密码登录配置

注意：这些命令需要在bash中敲

- 1 创建SSH Key：`ssh-keygen -t rsa`
- 2 在文件路径 `C:\用户\当前用户名\` 找到 `.ssh` 文件夹
- 3 文件夹中有两个文件：
  - 私钥：`id_rsa`
  - 公钥：`id_rsa.pub`
- 4 在 `github -> settings -> SSH and GPG keys`页面中，新创建SSH key
- 5 粘贴 公钥 `id_rsa.pub` 内容到对应文本框中
- 5 在github中新建仓库或者使用现在仓库，拿到`git@github.com:用户名/仓库名.git`
- 6 此后，再次SSH方式与github“通信”，不用输入密码确认身份了



# git结合远程仓库的使用

## 建立空仓库

必须建立一个空仓库, 不能初始化`README.md` vue-cli会自动创建

```shell
#关联远程仓库
#码云 remote给远程仓库起一个别名
git remote add origin https://gitee.com/lzce/vue-study.git
#github
git remote add origin git@github.com:lzce/lzc_lib.git

#这条, 会把本地项目push 码云上, 每天代码写完后, 可以push 一下
git push -u origin master
```

## 项目中使用

1. 可以在项目中创建分支
2. 最后到合并到主分支`master`中

3. 在`git push ` 之前`git pull origin master` 
4. `git push origin master`





# vue-cli脚手架

js代码加不加分号: https://www.zhihu.com/question/20298345







# render函数渲染组件

`render`是一个函数, 和`el, data`平级, 参数`createElement` 是一个方法

`createElement` 的参数是, 组件模板对象, 调用方法, 会返回html字符串, 并替换掉`el` 控制的区域, 也能够渲染组件 

```js
   let login = {
      template: '<h1>这是一个登陆组件</h1>'
    }
    let vm = new Vue({
      el: '#app',
      methods:{},
      data:{},
      render:  (createElement) => {
        return createElement(login)
      }
    })
```





# webpack项目中使用Vue

在 webpack 中, 使用`import Vue from 'vue'` 导入的`vue` 构造函数, 功能是不完整的

### 包的查找规则

**`import` 的查找规则和`require`的查找规则一模一样**

1. 在项目的根目录中找有没有`node_modules` 文件夹
2. 在`node_modules` 中根据包名找对应的`vue`**包名文件夹** 
3. 在`vue` 包中找`package.json`的包配置文件
4. 如果有配置文件, 在配置文件中查找`main`属性, `main`属性指定了加载包的时候的入口文件



`import` 到如的`vue` 包的`package.json`的main属性加载的是`dist/vue.runtime.common.js`

并不是`dist/vue.js` 所有功能不全, **`vue.js` 是在网页中使用的vue**

**解决方法**

1. 直接修改vue的`package.json` 的main属性的入口文件

2. 第二种

```js
import Vue from '../node_modules/vue/dist/vue.js'
```

3.修改`webpack.config.js` 配置文件

```js
# 在配置文件中添加一个节点
module.exports = {
    resolve: {
        alias: {
          "vue$": "vue/dist/vue.js"
        }
    }
}
```



### 在webpack使用vue

### `runtime-only` 模式使用vue



1. **创建一个`.vue` 的组件模板对象**

```vue
<template>
  <div>
    <h1>这是通过 .vue方式定义的组件</h1>
  </div>
</template>
<script></script>
<style></style>
```



2. **在`mian.js`中 引入并使用分离出去的组件**

```js
import login from './login.vue'

let vm = new Vue({
    
    
})
```

3. **默认`webpack` 处理不了`.vue` 的文件, 需要第三方`loader` , 并定义规则**

```shell
# vue-loader 内部 依赖 vue-template-compiler
$ npm i vue-loader cue-template-compiler -D
```

4. **定义loader 配置规则**

```js
const VueLoaderPlugin = require('vue-loader/lib/plugin');

plugins: [
    new VueLoaderPlugin()
  ],

module: {
    rules: [
      {test: /\.vue$/, use: 'vue-loader'},
    ]
  }
```

5. **配合`render`函数, 在页面中展示组件**

**在webpack中, 如果想要通过`vue` 把一个组件放到页面中展示,只能通过 vm的render函数实现**

```js
import Vue from '../node_modules/vue/dist/vue.js'
import login from './login.vue'

let vm = new Vue({
  el: '#app', //页面中 id为app的盒子
  data:{
    msg: '尝试使用vue'
  },
  // components: {
  //   login,
  // }
  render(createElement){
    return createElement(login)
  }
})
```





## webpack项目使用vue-router

### 安装

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter) //手动安装路由功能
//如果使用全局的 script 标签，则无须如此 (手动安装)。
```

### 使用

1. 下包, 引包

2. 手动安装`VueRouter`
3. 定义路由匹配规则对象
4. 在render() 函数渲染的组件内定义路由模块

```js
import Vue from 'vue'
import app from './App.vue'
// 1. 引包
import VueRouter from 'vue-router'

//2.手动安装
Vue.use(VueRouter)

import account from './main/Account.vue'
import goodList from './main/GoodList.vue'


//3.定义路由对象
let router = new VueRouter({
  routes: [
    {path: '/account', component: account},
    {path: '/goodList', component: goodList}
  ]
})

let vm = new Vue({
  el: '#app',
  render: c => c(app),
  router,
})


# 4.在App.vue组件中使用路由
<template>
  <div>
    <h1>这是我们的APP组件 --- {{ msg }}</h1>
    <!-- 4.在app组件中显示路由 -->
    <router-link to="/account">Account</router-link>
    <router-link to="/goodList">goodList</router-link>
    <router-view></router-view>
  </div>
</template>
```

**注意点**

APP.vue组件是通过vm使用的render()函数渲染出来的,	render() 函数会替换掉 el 控制的区域, 所以不要把 `router-link` 和 `router-link ` 写在el 的区域内, 应该写在`APP.vue` 组件中



### webpack 中路由嵌套

1. 定义两个子组件文件, 在入口函数中`import`

2. 在路由匹配规则的`rules`一条规则中, 调加`children` 属性, 数组中添加子路由
3. 在父路由组件中添加`router-link` 和 `router-view` 

```js
#1.引入子组件
import login from './subcom/login.vue'
import register from './subcom/register.vue'

//3.定义路由对象
let router = new VueRouter({
  routes: [
    {
      path: '/account',
      component: account,
        # 2.设置子路由
      children: [
        {path: 'login', component: login},
        {path: 'register', component: register},
      ]
    },
    {path: '/goodList', component: goodList}
  ]
})

#3. 在父路由组件中写路由结构
<template>
  <div>
    <h1>这是Account组件</h1>

    <router-link to="/account/login">登录</router-link>
    <router-link to="/account/register">注册</router-link>

    <router-view></router-view>
  </div>
</template>
```





## `.vue` 中的 style 标签

### scoped



在子组件的`style` 标签中能够书写样式, 但是如果不加特定的属性, 样式也会作用在父组件身上, `scoped` 能够设置样式只作用于当前组件 

**只要style标签在`.vue` 组件中定义的,  那么在`style` 标签中都推荐开启`scoped` 属性**

实现原理: 

1. 当我们在`style` 上加上scoped时, 给当前组件`template` 所有元素添加一个自定义属性`data-v-...` 的自定义属性
2. 会给所有的选择器自动添加一个属性选择器

```vue
<style scoped>
    div {
        color:red;
    }
</style>
```



**scoped 的坑**: 

 [https://vue-loader.vuejs.org/zh/guide/scoped-css.html#%E6%B7%B7%E7%94%A8%E6%9C%AC%E5%9C%B0%E5%92%8C%E5%85%A8%E5%B1%80%E6%A0%B7%E5%BC%8F](https://vue-loader.vuejs.org/zh/guide/scoped-css.html#混用本地和全局样式) 

它的作用域: scoped的作用域只是当前作用域 模板中 的 组件, 对于我们使用的第三方组件, **组件内部的子组件, 控制不到**

解决方案: 

1. 在`vue` 中	写两个`style`  一个加`scoped` 一不加`scoped` 让它向下渗透

```vue
<style></style>
<style lang="less" scoped></style>
```

2. 深度作用选择器 `// 在 less 中是 /deep/ 在 scss中是 ::deep 原生的是 >>>`

加上深度作用选择器之后, 样式会向下渗透

```vue
<style scoped>
	.a >>> .b { /* ... */ }
</style>
<style scoped lang="less">
    /deep/ .quill-edit {
        
    }
</style>
```

3. 去掉style 中的 `scoped`

### lang

默认普通的`style` 标签只支持普通的 css 样式语法, 不支持 `scss` 和 `less ` 语法, `lang` 属性能够指定`css` 指定使用`less` 和 `scss` 语法

```vue
<style lang="scss">
    body {
        div {
            font-style: italic; 
        }
    }
</style>
```



## 抽离路由

### 把路由用到的组件抽离到路由文件中

### 把路由匹配规则抽离

### 导出路由匹配规则对象

```js
// 1. 引包
import VueRouter from 'vue-router'

//引入组件
import account from './main/Account.vue'
import goodList from './main/GoodList.vue'

//引入子组件
import login from './subcom/login.vue'
import register from './subcom/register.vue'

//3.定义路由对象
let router = new VueRouter({
  routes: [
    {
      path: '/account',
      component: account,
      children: [
        {path: 'login', component: login},
        {path: 'register', component: register},
      ]
    },
    {path: '/goodList', component: goodList}
  ]
})

//导出
export default router
```

### 在入口JS文件导入路由

```js
//导入路由
import router from './router'
```





# Vue 第十天

## [mint UI](http://mint-ui.github.io/#!/zh-cn )  组件库

基于Vue.js的移动端组件库

### mui和 mint UI

> 注意： MUI 不同于 Mint-UI，MUI只是开发出来的一套好用的代码片段，里面提供了配套的样式、配套的HTML代码段，类似于 Bootstrap； 而 Mint-UI，是真正的组件库，是使用 Vue 技术封装出来的 成套的组件，可以无缝的和 VUE项目进行集成开发；
> 因此，从体验上来说， Mint-UI体验更好，因为这是别人帮我们开发好的现成的Vue组件；
> 从体验上来说， MUI和Bootstrap类似；
> 理论上，任何项目都可以使用 MUI 或 Bootstrap，但是，MInt-UI只适用于Vue项目；

### 安装 和 引入

```shell
$ cnpm i mint-ui -S
```

**完整导入**

```js
// 引入全部组件
import Vue from 'vue';
// 1.导入组件
import Mint from 'mint-ui';
// 2. 导入css样式, node_modules 这层目录可以省略
import 'mint-ui/lib/style.css'
// 3. 手动安装
Vue.use(Mint);
```

### 使用

mint UI 一共分为三种组件

JS Components  Css Components  Form Components

#### JS components 使用

1. 即使在main.js中导入了整个`mint-ui` 在 组件中使用mint-ui的js组件, 按需导入对应组件
2. [其他更过组件, 查看文档](http://mint-ui.github.io/docs/#/zh-cn2 )

```js
<mt-button type="primary" size="normal" @click="show">primary</mt-button>

//在组件中使用JS components 需要引入对应的组件
import { Toast } from 'mint-ui'
export default {
  methods: {
    show() {
      Toast({
        message: "您好呀, 我是小傻子",
        position: "top",
        duration: 3000,
        iconClass: 'glyphicon glyphicon-ok',
        className: 'mytoast'
      });
    }
  }
}
```

####  Css Components 

1. css组件直接使用mint-ui提供的便签即可, 



### 按需导入

借助 [babel-plugin-component](https://github.com/QingWei-Li/babel-plugin-component)，我们可以只引入需要的组件，以达到减小项目体积的目的。

1. 首先，安装 babel-plugin-component：

```shell
$ npm install babel-plugin-component -D
```

2. 修改`babelrc` 

```js
{
  "presets": [
    ["es2015", { "modules": false }]
  ],
      
   //这是要添加的
  "plugins": [
      ["component", [
    {
      "libraryName": "mint-ui",
      "style": true
    }]]
  ]
}
```

3. 在main.js 中引入

```js
import Vue from 'vue'
import { Button, Cell } from 'mint-ui'
import App from './App.vue'

//Vue.component(Button.name, Button) // Button.name 是在页面以<mt-button>标签名称引入组件
//Vue.component(Cell.name, Cell)

Vue.component('mycell', Cell)
/* 或写为
 * Vue.use(Button)
 * Vue.use(Cell)
 */

new Vue({
  el: '#app',
  components: { App }
})
```



## MUI 

> *mui不能使用npm 去下载*, 只能去github上下载, 拷贝到项目中, 用法和bootstrap一样

mui用法不同于其他基于VUE 开发的组件, 需要使用`Vue.use` 手动安装

只需要在入口文件`main.js` 中引入即可

```js
import './lib/mui/css/mui.min.css'
```









# 反向代理 (webpack反向代理- 开发中的配置)

jsonp: 利用script:src

cors: 跨域资源共享, 前端什么都不做. 后端把资源权限开放即可

**主要用于开发中的跨域**

原理: 跨域只发生在浏览器中, 同源跨域策略是浏览器安全策略, 服务器与服务器之间是没有跨域问题的

我们的webpack开启的服务器就是一个代理服务器

1. 我们请求我们自己的webpack的服务器
2. 让服务器去访问后台服务器

devServer的配置

```js
module.exports = {
    devServer: {
        proxy: {
            // 只要请求路径中包含 /aaa 就会被代理到 ->http://localhost:8888/api/private/v1/aaa/login
            '/aaa': {
                target: 'http://localhost:8888/api/private/v1/',
                
                // /aaa/login => 就会被代理到http://localhost:8888/api/private/v1/login
                // /aaa 会被重写成 ''
                pathRewrite: {
                    '^/aaa': ''
                }
            }
        }
    }
}
```

修成main.js 中的axios的baseURL配置

```js
axios.defaults.baseURL = '/aaa'
```





 ![](image\反向代理.png)



# 技术栈

技术栈: 开发整个项目所使用的一整套技术

### 3条技术栈

jquery +  jQuery插件 + $.ajax + art-template + bootstrap(ui框架)  => 操作DOM, 性能不高

vue + vue-router + vuex(状态管理) +axios +  vue插件 + vue的 ui 框架 ( 组件库  element-ui )

react + react-router + redux + axios + react 插件 + react 的 ui 框架 ( ant-design  蚂蚁金服的ui组件库) 





# minix 混入



# vue只有一个实例



# Vue.use

它其实是帮我们注册一些全局的组件, 我们 import 包Vue 插件之后, 想要使用它的组件, 还必须注册组件`Vue.component()` , 

但是使用`Vue.use()` 就相当于了我们, Vue自动帮我们注册全部的插件提供的组件

另一种方式, 我们可以按需导入, 但是需要手动注册组件`Vue.component`



### 基于Vue的插件

需要 `Vue.use()`, 进行全局组件的注册



### 不是基于Vue 的插件

直接`import` 即可, 但是如果希望在很多页面上使用, 可以挂载到 `Vue.prototype` 原型上