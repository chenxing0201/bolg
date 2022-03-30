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