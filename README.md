## 面试经验
中小厂面试经 包括有外包也有创业公司

A公司

外包公司 所面试的项目组 使用vue和uniAPP
- vue router 两种区别，
- 讲讲diff算法
- webpack的掌握情况
- VScode插件开发  ×，公司级别组件开发
- uniAPP ，flutter  ×
- 组织过技术分享会吗×
- 说说关注的新技术×
- 博客 ×
- Python的掌握程度，说几个常用的sql  ×

B公司

- vue router
- diff
- js的事件机制，事件循环
- vue里面conplete和watch
- 从URL到页面战展示出来的过程
- http 三次握手 四次挥手
- 广度优先
- 解析二叉树

C公司

- es6新特性
- promise
- generator  让异步函数看起来像同步
- js事件流
- 不同设备或浏览器适配
- 路由传参，是对象的话
- 组件直接的通讯:
- props
-  event bus
-  this.$ref.parent
- vuex
- 如果你某次提交的有bug，别人又在你的代码上提交了很多次，你该怎么办
- canvas几款插件有了解过吗

D公司

- 活动页图片比较多的话，怎么优化性能？
- webp图片对所有浏览器都支持吗？
- dom事件流和事件委托   js事件，事件循环，冒泡
- 哪些标签有原生事件，a标签
- js怎么判断数据类型
- 然后根据这个判断数据类型实现一个深拷贝 
- this的指向
- 原型和原型链的考察
- nexttick里面可以写settimeout0吗
- websocke实现消息推送实现了什么功能
- 腾讯第三方实现即时通讯实现了什么功能
- electron，把vue打包成桌面应用，引入electron配置文件修改webpack配置修改命令实现打包
- 所做的项目里哪个对自己的提升比较大说明一下
- 自己对做web前端开发有哪些优势？
- 答:比较爱专研难题，工作中遇到难题会尽力想各种不同办法去解决，实在解决不了就找领导或者产品从其他角度解决
- 自己还有那些掌握的比较好的我没问到的吗？
- 答:vue的diff算法，还有一些vue使用到的设计模式

E公司

- webpack 打包之后看不到源代码，设置什么可以看到  productionSourceMap
- vue2和vue3有何不同  打包之后有什么不同
- 使用百度地图，地图如果标记的点比较多怎么办？
- 说说vuex的几个属性
- vue动态路由怎么设置 嵌套路由怎么设置 
- 路由懒加加载
- keepalive 保留到哪个生命周期
- 数据双向绑定
- 列表里面看key可以用用索引吗？ 不能
- 观察者 发布者 订阅者 之间的关系
- localStoare  sessionStoare  cookie的区别是什么
- 如何解决跨域问题的
- vue的模板编译原理 vue_loader
- vue里面自定义指令的原理是什么
- 跨域你们怎么实现的jsonp的实现原理

F公司
- 盒子模型 怎么实现 box-sizing ：boeder-box;
- css 动画的几种实现形式
- js的数据类型
- js的引用数据类型
- 宏任务和微任务
- this
- 闭包
- vue 的数据为啥用函数
- 组件之间传参
- setUP 定义一个可被监控的
 伪类 和伪元素用过没

G公司
- 适配要怎么做 答：rem  
- 怎么使rem怎么生效，怎么作用的？以什么为基准？ 比列标准是以谁为参照物 
- 根据根标签的font-sise
- 公司使用的公用的脚手架 如果有公用的util包， 如果不同的项目需要修改或者补充 对应的方法 项目比较多的话， 需要找不同项目需要迭代，这种情况怎么处理？怎么快速解决
- vue 双向绑定怎么做的？
- object.defineProto wahter是什么时候有的， watcher 函数是存哪的，
- new Vue之后做了什么事情？ newvue的时候已经有这些data，添加监听着，一个数组的时候时候push应该可以立刻触发到这个
- v-for的k是干嘛的
- vue.use()是干嘛的？自己会写吗？他引用的是vue插件，不是组件 有没有写过vue插件
- webpack 会用吗？压缩图片 url-loader 里面的limit默认是10000 是8k 把图片转换为base64
- 理解base64是什么东西吗 把图片转换成base之后 图片体积变大还是变小了？？ 实际是变大了。
- base64的编译原理，为啥体积变大了还要用这种不合理的方式，
- limit的值设置成99999合理吗？然后其他同事都在用， 自己又没有深究， 不知道是什么东西
- 解决完问题之后是需要继续跟进
- 对后面一份的定位？ 
- 你怎么去自我学习？ 业务稳定，人员稳定，不思进取，通过跳槽可以解决一部分。





## vue router  还是很重要的点
 可以 去官方文档学习下 https://router.vuejs.org/zh/guide/essentials/nested-routes.html

常用的两种模式 hash 和history

- 如何配置动态路由使用 
````
const User = {
  template: '<div>User</div>',
}
const routes = [
  // 动态字段以冒号开始
  { path: '/users/:id', component: User },
]
````
参数会可以用 this.$route.params 这个获取到，此外也可以通过$route.query获取到url后面的参数

动态字段发生变化，同一个路由对应的组件，对应的组件不会重新创建， 复用的会更加高效， 对应的生命周期也不会再次触发， 我们如果需要对参数改变做出变化， 需要在watch 中进行监控$router.pramas发生改变时再进行相应的操作，如下示例：
```
const User = {
  template: '...',
  created() {
    this.$watch(
      () => this.$route.params,
      (toParams, previousParams) => {
        // 对路由变化做出响应...
      }
    )
  },
}
```
或者也可以使用beforeRouteUpdate 路由守卫 ，在路由发生改变之前， 也可以对路由跳转进行取消
```
const User = {
  template: '...',
  async beforeRouteUpdate(to, from) {
    // 对路由变化做出响应...
    this.userData = await fetchUser(to.params.id)
  },
}
```

-  路由懒加加载
可以有三种方式实现，
1. 通过require 引入异步组件 
2. 通过es6的import 引入
3. 通过webpack的 require.ensure() 实现按需加载
第一种通过require 实现会打包进一个js
```
{
  path: '/home',
  name: 'home',
  component: resolve => require(['@/components/home'],resolve)
},

```
第二种使用import
```
// 下面2行代码，没有指定webpackChunkName，每个组件打包成一个js文件。
/* const Home = () => import('@/components/home')
const Index = () => import('@/components/index')
const About = () => import('@/components/about') */
// 下面2行代码，指定了相同的webpackChunkName，会合并打包成一个js文件。 把组件按组分块
const Home =  () => import(/* webpackChunkName: 'ImportFuncDemo' */ '@/components/home')
const Index = () => import(/* webpackChunkName: 'ImportFuncDemo' */ '@/components/index')
const About = () => import(/* webpackChunkName: 'ImportFuncDemo' */ '@/components/about')
```
第三种
 




## vuex的几个属性
 
共5个属性

1. state 存储变量的地方
2. getter 相当于对数据进行二次计算的的一个计算属性
3. mutations 在这里定义改变state中的数据的方法
4. action 一种异步改变state的方式不能直接改变 需要调用mutation中的方法用但是要引入store 使用store.commit
5. modules 给state 进行模块化， 针对不同的模块进行分别管理上面四个属性


数组的新方法
[...arr1,...arr2]  arr.map  arr.fliter arr.flat  arr.includes arr1.concat(arr2)
array.from 将类数组转换成数组
array.of() 将一组值转化成数组
对象的 object.asign()

## 谈谈对Promise的理解
promise 就是对异步操作的容器用来保存一个异步的结果， 如果已经有结果就会立即执行，有三个状态pending 进行中，  resolve成功的结果 reject 失败的结果，一旦定义就立即执行， 无法撤销。 将异步的操作同步化，可以使用.then 获取结果， 也可以使用链式避免回调地狱。


原型链 
https://juejin.cn/post/6844903749345886216

### localStoare  sessionStoare  cookie的区别是什么

https://blog.csdn.net/weixin_46419373/article/details/107265523

一定要对自己简历中的技术熟悉就要熟悉，多方位了解透彻。了解透彻再进行面试选好公司 一击即中。


