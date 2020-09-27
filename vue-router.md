### vue 的路由 vue-router

1. vue 基础之上用的一些插件
2. 单页面实现多页面，单页面怎么跳转到多页面
3. 想要实现各种各样的插件怎么使用
4. 第一个要讲的就是 vue 路由

对于 `vue` 这种单页面应用，官方提供了` vue-router` 库，来实现多页效果。

- 如何实现
  **创建**

- 安装 `vue-router` 包
- 新建 `router.js` 里面创建路由。
  - 导入页面所有需要的页面组件
  - 根据页面组件创建路由数组
  - 创建 `vue` 路由实例
- 在 `main.js` 导入创建好的路由实例，加入到整个 `vue` 项目中

**使用**

需要用 `vue-use(VueRouter)` 将 `vue-router` 内自带的组件制作成 `vue` 的插件，也就是说在整个 `vue` 项目中可以随意使用 `vue-router` 内自带的组件了。
`router-view` 组件代表这个路由，使用 `router-link` 组件进行路由跳转。

快速创建路由方式(前提是 `vue` 的环境时 `vue-cli3.0` 以上)

- 使用 `vue ui` 安装插件，选择安装 `vue-router` 的插件
- 使用命令行工具执行 `vue add vue-router`

快速安装之后，项目内就会自带一个路由 `demo` ，直接使用即可。

对于 `router-view `和 `router-link` 组件的各种配置参考 [vue-router 官方文档](https://router.vuejs.org/zh/)

### 安装 vue-router

- 图形化界面安装: 小的用依赖，大的用插件(这里有个问题:必须是不写东西的时候安装，如果写东西了再安装不会生效)
- 或者到依赖里面安装也行，就可以改变那个不生效的问题
  vue-router 属于大的，点击 `插件`，看到右上键的 `添加 vue-router`
- 也可以用命令行根据安装(可以随时随地的安装，什么时候都行)

  1. 直接输入 `npm i vue-router`
  2. 手动安装相当于安装依赖

- 安装好了之后去看官方的文档
- !(lodash 官方文档)[https://router.vuejs.org/zh/guide/]
- `HTML` 安装方式是对于初学者而言的，我们只需要看 `javaScript` 的内容就行了

- 先有几个组件代表页面，然后根据这个组件创建成路由，然后将定义好的路由创建成路由实例，然后把实例给到 `App.vue` 项目中就有页面了。

以下是简单的应用和跳转

```html
<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 -->
  <router-view></router-view>
</div>
```

- 在 `src` 文件夹下创建 `views` 文件夹一般都是放着大组件的。

接下来就创建一个路由给 `App` 用。

- 最后一步把路由新建一个文件，叫做 `router.js`
  因为路由创建的时候不是一个组件，要写一个 `router.js` 然后再导入到 `main.js` .

```js
//  路由文件
// 捋一遍:第一你的 vue 要使用多页面实现，首先要安装 vue-router 。
// 安装方式有两种:
// 1. 通过图形化界面工具 依赖 安装插件搜索 vue-router 点击安装。
// 2. 打开命令行工具，直接使用官方推荐的命令 npm install vue-router
// 安装好之后需要我们去创建，创建一个 vue 路由实例，供你整个项目去使用。
// 如何创建路由实例
// 1. 将需要的页面其实就是组件导入到 js 中，导入完好后根据这些东西创建成一个路由数组，路由是什么?一个路由就是一个页面。路由包括什么?包括路由的路径和需要展示的页面组件。路径用 path 替代，component 就是组件。/ 就是 http://localhost:8000。其实地址就是我们设置的，想要什么就什么，xxxx 也行。
// 路由创建好了之后，我们就通过 类 创建成路由实例(就是将数组内的页面创建成路由实例)，这样整个路由就创建好了。
// 使用的时候就将路由导出。给我们的整个项目，在 mian.js  new Vue 中给。但是这还不算完毕，这只能算是我能用了。
// 用分两步：1. 先加载到我的项目中  2. 需要借助 vue-router 中的组件才能展示我的路由。
// 怎么用 vue 的组件呢？
// 1. 是从包里面导入，但是这样导入有点局限，很多组件都需要，会很麻烦。
// 2. 所以我们将 vue 当做全局的一个插件，使用 vue.use 方法将 vue-router 里面的组件共享给 vue 的整个项目，那么所有的东西我们都可以用了。所以我们需要导入 import VueRouter from "vue-router"; 以及 import Vue from 'vue' ;
// 使用 Vue 里面的 use 方法将里面的组件当成 vue 项目公共的东西。这就是以后要给大家将的一个重点 插件。插件的用法
// 都准备好了之后，就可以在项目内任意一个地方使用 `<router-view></router-view>` 都可以访问路由。访问的是哪个页面呢？该组件展示的就是路由(页面) 路由的匹配规则要根据当前页面地址和路由的 path 进行匹配
//  一. 创建页面路由

//  1. 导入页面组件,可以从其他文件 import 进来  (什么叫页面组件:这个项目到底有几页,这几页分别代表哪个组件)
import VueRouter from "vue-router";
import Vue from "vue";
import Home from "./views/Home.vue";
import About from "./views/About.vue";
import Computed from "./views/Computed.vue";

// 因为路由创建完毕之后是需要使用一些 vue-router 内自带组件展示和跳转页面，所以需要时使用 use 方法。
//  use 方法使用了之后，vue-router 内自带组件就可以在整个 vue 项目中使用了。
// 比如我的十个页面都想要跳转，那么跳转的那些组件都是 vue-router 自己的，vue 是没有的，那么 vue 里面想要使用 vue-router 的东西那么使用 use
Vue.use(VueRouter);
//  2.根据页面组件创建路由数组 (名字随便取)
const routes = [
  // 该数组内的每一项就相当于一个页面，页面一般由两部分组成 1. 页面地址  2. 页面对应的页面组件
  //   / 的意思代表当前服务器的根目录，我们现在其实就是 http://localhost:8000
  { path: "/", component: Home },
  { path: "/about", component: About },
  { path: "/Computed", component: Computed },
];
// 3.根据路由数组创建路由实例
//  创建路由实例的时候是可以选择路由模式的
//  路由模式分为两种 1. hash 使用 URL 的 hash 默认的 2. history 完全模拟浏览器
//  可以使用 mode 设置路由模式
// 创建实例的时候需要传递 router 属性，属性值是路由数组。
const router = new VueRouter({
  // 当对象的属性名 VueRouter 和他的值对应的那个变量名相同的时候就可以省略
  routes: routes,
  mode: "history",
});
//  4. 创建完毕之后，导出路由实例，添加到整个 vue 项目中，参考 main.js 的写法。
export default router;

// 二. 使用路由
// 在组件内部使用 <router-view> 就可以展示路由了。
```
