## vuex

### vuex是什么

**Vue应用程式的状态管理工具, 状态即数据**

是vue配套的公共数据管理工具, 他可以把一些共享的数据, 保存到vuex中, 方便整个程序中任何组件直接获取获取修改我们的数据

vuex是为了组件之间共享数据而诞生的, 如果组件之间有需要共享的数据, 可以直接挂载到vuex之中, 而不必要通过父子组件之间传值的方式了 , 如果组件之间的数据不需要共享, 此时这些不需要共享的私有数据, 没有必要放到vuex中

### props和data, vuex区别

1. 只有共享的数据, 才有权利放到vuex中

2. 组件内部私有的数据, 只要放到组件的data中即可
3. `props`存放父组件传递的值, data存放自己的私有数据, vuex存放共享数据



**结论**

**vuex**是一个全局的共享数据存储区域, 就相当于一个数据仓库



### vuex使用

**装包**

```shell
$ yarn add vuex -S
```

**初始化vuex,创建仓库**

```js
//  1 - 导包
import Vuex from 'vuex'
// 2- 挂载到vue上
Vue.use(Vuex)

//3-  如果在模块化构建系统中，请确保在开头调用了 Vue.use(Vuex)
const store = new Vuex.Store({
  state: {  # state类似于组件中的data, 用来存储数据的, 区别于data之处在于所有组件都能访问
    count: 0
  },
  mutations: { # 相当于组件中的methods
    increment (state) {
      state.count++
    }
  }
})

const vm = new Vue({
    el: "#app",
    data:{},
    store,  # 4- 把 store 挂载到 vm 实例上
})
```

访问`store` 仓库中的数据

1. `vue实例.$store.state.xxx`
2. `this.$store.state.xxx`
3. `store.state.xxx`

### 在项目中使用vuex

**1.安装包并引入**

```js
yarn add vuex

//在mian.js中引入
import Vuex from 'vuex'
```

**2.在main.js中配置vuex**

```js
//注册vuex
Vue.use(Vuex)

//创建一个store
const store = new Vuex.Store({
  state: {   //this.$store.state.***
    count: 0
  },
  mutations: { //this.$store.commit('方法名', '按需传入唯一的参数')
    increment (state) {
      state.count++
    }
  },
  getters: {  //this.$store.getters.***
    
  }
})
```

**3.将store挂载到根组件上**

```js
const vm = new Vue({
  el: '#app',
  render: c => c(app),
  router, //1-4 在app组件中挂载路由
  store   //挂载状态管理对象
})
```



### mutations

**在组件(vm)中挂载之后, 就可以访问store中的数据了, 通过`this.$store.state `**

**注意点**

如果要操作 store  中state 中, 只能通过调用  `mutations `提供的方法, 才能操作对应的数据, 不推荐直接操作 state 中的数据, 因为直接操作state中的数据, 可能会导致数据紊乱, 不能快速定位到错误的原因, 因为每个组件都可能有操作数据的方法

> Vuex的数据, 请不要让组件修改, 请交给vuex自己修改, 提交给mutations

**`$store.commit('方法名', 传递过来的参数)`** 

**注意: mutations中的函数的参数列表中只能传递二个参数, 并且第一个参数永远是state**

```js
const store = new Vuex.Store({
  state: {  # state相当于组件中的data, 用来存储数据的
    count: 0
  },
  mutations: { # 相当于组件中的methods
    //在mutations中定义, 组件通过 this.$store.commit('方法名')调用          
    increment (state) {
      state.count++
    }
  }
})

#在组件中调用
const vm = new Vue({
    el: '#app',
    methods:{
        add(){
            this.$store.commit('increment') //调用store中的方法
        }
    }
})
```



#### 提交载荷Payload

`mutations中的方法, 只能接受一个commit参数`

### getters

是`Vuex.store()` 的配置属性之一,基于state的计算属性, **只负责对外提供数据,** 如果想要修改 state  中的数据,  去找`mutations ` , `getter` 中的计算属性的第一个参数也都是`state`

 Vuex 允许我们在 store 中定义“getter”（可以认为是 store 的计算属性）。就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。 

```js
getters: {
    todoLength (state) {
        return state.list.length
    }
}
```

和 vue 中的`computed` 区别: 

- 没有`computed` 的完成形态. 只能获取, 不能设置

使用`getters` 中的 属性 `$store.getters.方法名`

### 结合Vuex实现Todos


## vuex辅助函数

能够简化我们在组件中使用vuex中的数据

`getters` => `mapGetters`

`state` => `mapState`

`mutations` => `mapMutations`



### mapGetters 辅助函数的使用

**mapGetters 是一个函数, 作用: 将vuex中的 getters 直接映射给组件作为计算属性**

<https://vuex.vuejs.org/zh/guide/getters.html>

1. 先导入
2. 展开混入

```js
// 1- 先导入
import { mapGetters } from 'vuex'

// 2- mapGetters中的每一项都会映射成一个计算属性
export default {
    computed: {
        // 第一种写法, 写计算属性数组
        //...mapGetters(['isShowFooter', 'leftCount', 'isShowClear'])
        
        
        // 第二种写法, 写对象, 键作为我们的自定义的计算属性名, 值是vuex的getters中的计算属性
        ...mapGetters({
            isClear: 'isShowClear'
        })
    }
}
```



### mapState 辅助函数

**作用: 可以映射一个state属性**

改造=> TodoMain 的 list

先导入

```js
import { mapState } from 'vuex'
```

将来要使用 state 中的数据 :

```js
  computed: {  
    // 只要 store中 state中的 list 发生变化, list 就跟着改变
    // list () {
    //   return this.$store.state.list
    // }
    ...mapState(['list'])
  },
```





### mapMutations 辅助函数的介绍

**如果一个函数, 只是提交 mutations,  可以将 mutations 的提交操作, 进行简化操作**

**作用: 可以映射一个mutations方法**

前提: 在方法中, 只进行了提交 mutations 可以简化, 只做了`mutations` 提交才能简写(所以不常用)

<https://vuex.vuejs.org/zh/guide/mutations.html>



```js
import { mapMutations } from 'vuex'

methods: {
    // delTodo (id) {
    //   // 根据 di 去删除对应的数据 (数据在哪???)
    //   // 触发提交一个 mutation
    //   this.$store.commit('delTodo', id)
    // },
    // changeState (id) {
    //   this.$store.commit('changeState', id)
    // },

    // 映射方法, 就相当于上面的代码
    ...mapMutations(['delTodo', 'changeState']),
}
```





# vuex - actions

## todos - vuex 中 actions 的使用

**需求: 在一秒之后, 清空所有的已完成的内容**

```js
const mutations = {
  ...
  clearTodo (state) {
    setTimeout(() => {
      state.list = state.list.filter(item => !item.flag)
    }, 1000)
  }
}
```

**强制要求:**  一条重要的原则就是要记住 **mutation 必须是同步函数**。**强烈要求`mutations`中不能出现异步 , 如果要异步, 扔到 action 里面**

mutaion: <https://vuex.vuejs.org/zh/guide/mutations.html>

action: <https://vuex.vuejs.org/zh/guide/actions.html>



定义 actions

- 所有 `actions` 中的 函数的第一份参数都是`context`=>上下文, 就是 `store` 对象

```js
// actions 和 mutations 类似, 都是提供方法
// actions 不能直接操作 state, 需要提交 mutation
const actions = {
  // context: 上下文, 就是store对象
  clearTodoAction (context) {
    setTimeout(() => {
      context.commit('clearTodo')
    }, 1000)
  }
}
```

使用

```js
import { mapActions } from 'vuex'

// clearTodoAction () {
//   使用 dispatch 分发 action
//   this.$store.dispatch('clearTodoAction')
// }
...mapActions(['clearTodoAction'])
```



`mutations ` 和 `actions` 区别

1. `mutations ` 必须是同步的, 可以直接修改`state` 的数据
2. `actions` 可以是异步的, 可以是同步的, 但是不能直接修改`state`中的数据, 可提交`mutations` 就是调用`mutations` 中的方法



# vuex 的使用流程图

1. state:  存放数据
2. mutations:  存放修改数据的方法
3. getters:  存放基于state派生的一些属性 (state的计算属性)
4. actions: 存放一些异步的方法


# vuex五大特性

如果业务复杂不用vuex的话，可维护性下降\
要修改数据要改三个地方，可读性也下降。\
会让耦合性增加。\
耦合性指模块间相互联系紧密程度的一种度量。\
耦合性越强，独立性越差