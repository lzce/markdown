# fastClick 插件- 300ms点击延迟
FastClick 是 FT Labs 专门为解决移动端浏览器 300 毫秒点击延迟问题所开发的一个轻量级的库。简而言之，FastClick 在检测到touchend事件的时候，会通过 DOM 自定义事件立即触发一个模拟click事件，并把浏览器在 300 毫秒之后真正触发的click事件阻止掉。使用方法如下

```js
import FastClick from 'firstclick'
FastClick.attach(document.body)
```

# 移动端1像素边框问题
有的手机的分辨率比较高可能是二倍屏或者三倍屏, 我们在页面上写的`border: 1px solid #ccc` 是css的像素单位,而不是屏幕的物理像素,在二倍屏下看它实际上不是一个物理像素,而是2个或者3个物理像素

为了解决这个问题,可以引入一个解决1像素边框问题的css文件

## better-scroll 区域滚动插件
它是iscroll 的一个封装, 在使用上更好用

gitHub地址: https://github.com/ustbhuangyi/better-scroll

使用步骤: 

html结构:
```html
<!-- 两层盒子包裹 -->
<div class="wrapper" ref="scroll">
  <div class="content">
  
    <!-- 这是要滚动的内容 -->
    <div>...</div>
    ...
    
  </div>
  <!-- 这里可以放一些其它的 DOM，但不会影响滚动 -->
</div>
```

JS 使用: 
```js
import BScroll from 'better-scroll'
mounted () {
    this.scroll = new BScroll(this.$refs.scrollList)
  }
```

### scrollToElement()方法
在城市选择页面中，点击右侧字母索引左侧可以滚动到对应区域时，可以使用scrollToElement()

参数：
  - el: DOM元素，也可以是选择器
  - time: 执行动画的时间

## Vue组件name属性作用
### 递归组件
组件的name属性，是在我们在组件中使用自己使其作用

组件内部使用组件自己就是递归组件

### 不被缓存
在`keep-alive`包裹的路由出口, 组件都会被缓存,但是`exclude="Detail"`可以排除缓存组件
```vue
<keep-alive exclude="Detail">  //除了detail组件都会被缓存
    <router-view />
</keep-alive>
```

### 在调试工具组件名字
在调试工具中显示的组件名字就取决于 `name` 的名字


## vue-router 滚动行为
在路由切换中,不同页面之间的滚动会相互影响, 简单来说,就是上一页面的滚动会在下一个页面保持同步

```js
const router = new VueRouter({
  routes: [...],
  scrollBehavior (to, from, savedPosition) {
    // return 期望滚动到哪个的位置
    return { x: 0, y: 0 }
  }
})
```
