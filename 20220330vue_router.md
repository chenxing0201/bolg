## vue router  还是很重要的点
参考文档
[vue router 官方文档](https://router.vuejs.org/)
[vue router 使用详情](https://www.jianshu.com/p/5dff6811252d)

##vue router的原理

常用的两种模式 hash 和history
SPA(single page application):单一页面ß应用程序，只有一个完整的页面；它在加载页面时，不会加载整个页面，而是只更新某个指定的容器中内容。单页面应用(SPA)的核心之一是:更新视图而不重新请求页面;vue-router在实现单页面前端路由时，提供了两种方式：Hash模式和History模式。

####1.hash模式
随着 ajax 的流行，异步数据请求交互运行在不刷新浏览器的情况下进行。而异步交互体验的更高级版本就是 SPA —— 单页应用。单页应用不仅仅是在页面交互是无刷新的，连页面跳转都是无刷新的，为了实现单页应用，所以就有了前端路由。类似于服务端路由，前端路由实现起来其实也很简单，就是匹配不同的 url 路径，进行解析，然后动态的渲染出区域 html 内容。但是这样存在一个问题，就是 url 每次变化的时候，都会造成页面的刷新。那解决问题的思路便是在改变url的情况下，保证页面的不刷新。在 2014 年之前，大家是通过 hash 来实现路由，url hash 就是类似于：
````
http://www.xxx.com/#/login
````
这种 #。后面 hash 值的变化，并不会导致浏览器向服务器发出请求，浏览器不发出请求，也就不会刷新页面。另外每次 hash 值的变化，还会触发hashchange 这个事件，通过这个事件我们就可以知道 hash 值发生了哪些变化。然后我们便可以监听hashchange来实现更新页面部分内容的操作：
````
function matchAndUpdate () {
   // todo 匹配 hash 做 dom 更新操作
}

window.addEventListener('hashchange', matchAndUpdate)
````

###2.history 模式
14年后，因为HTML5标准发布。多了两个 API，pushState 和 replaceState，通过这两个 API 可以改变 url 地址且不会发送请求。同时还有popstate事件。通过这些就能用另一种方式来实现前端路由了，但原理都是跟 hash 实现相同的。用了HTML5的实现，单页路由的url就不会多出一个#，变得更加美观。但因为没有 # 号，所以当用户刷新页面之类的操作时，浏览器还是会给服务器发送请求。为了避免出现这种情况，所以这个实现需要服务器的支持，需要把所有路由都重定向到根页面。
````
function matchAndUpdate () {
   // todo 匹配路径 做 dom 更新操作
}

window.addEventListener('popstate', matchAndUpdate) 
````


##vue router的使用

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


