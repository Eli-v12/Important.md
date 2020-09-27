#### 自定义主题

**Element** 默认提供一套主题，**CSS** 命名采用**BEM** 的风格，方便使用者覆盖样式。我们提供了四种方法，可以进行不同程度的样式自定义。
使用方法

1. 在线编辑查看效果满意后直接下载
2. 把 `fonts` 文件夹 和 `index.css` 文件都放在 `vue` 中的 `plugins` 文件夹下
3. 然后在 `element.js` 中引入 `index.css`

```js
import "./index.css";
```

如果放在 `assets` 文件夹中不会被打包编译，默认是啥就是啥，放在除了` assets` 文件夹外就会被打包编译。

#### 聊聊 Element 的安装使用

讲完 `vue-router` 路由插件，就顺着往下讲 `element` 插件，这是最最最常用的。别人做好的东西我们去拿来用就行了

```json
 "dependencies": {
    "core-js": "^3.6.5",
    "vue": "^2.6.11",
    "vue-router": "^3.2.0"
  }
```

`vue/cli` 官方提供的脚手架,解析 `vue created vue-demo`

我们主打的是 `pc` 端
用的组件库有(复制粘贴就可以直接用)

- `element ui` 组件库
- `swiper` 使用轮播图
- `Bootstrap` 按钮

如果不到万不得已就不要用之前的 `jq` 和 `dom` 操作，因为他们都是真实操作 `dom`。

#### 快速上手

**第一种:(全局)完整引入**

1. 使用 命令行工具 输入 `npm i element-ui -S`
2. 在 `main.js` 中写入以下内容：
   `vue` 里面有插件的知识，就是把 `element` 组件注册成全局的,想在哪用都行。

```js
// main.js 中
import Vue from "vue";
import ElementUI from "element-ui";
import "element-ui/lib/theme-chalk/index.css";
import App from "./App.vue";

Vue.use(ElementUI); //全局使用 Element 库里的各种效果
new Vue({
  el: "#app",
  render: (h) => h(App),
});
```

##### 使用

直接去官方的文档复制就可以了

```html
<el-button type="success" disabled>成功按钮</el-button>
```

**第二种:按需引入**

- 在图形化界面安装

  1. 在插件中安装 `element` (版本大概是 1.0.1 25k 左右)
  2. 点击安装后会出现图形化界面让你选择 --- 是否按需安装 ---
  3. 然后在 `plugins` 文件夹下的 `element.js` 中添加一下代码

```js
import Vue from "vue";
import { Button } from "element-ui";
// 将element 相关的代码f全部写到了 plugins/element.js 内，其实这就是代码分割。
// plugins 是插件的意思，以后想要的插件都可以放到这个文件夹中，方便管理和归类。
import { Message, InfiniteScroll, Tree } from "element-ui";
Vue.use(InfiniteScroll);
// 因为我们使用的是 element 的按需加载，所以不管是组件还是方法都得使用 use 或者 prototype 设置成全局的。
// 组件用 Vue.use()
// 方法用 Vue.prototype.$xxx = xxx
// 改了配置的话的重启才生效
Vue.prototype.$message = Message;
Vue.use(Button);
Vue.use(Tree);
```
