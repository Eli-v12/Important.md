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

### vue 的常用的 ui 库 element-ui

#### 完整引入

1. 第一步用 `npm` 的方式安装，它能更好地和 `webpack` 打包工具配合使用。
   - 在项目下的命令行工具中输入 `npm i element-ui -S` 下载。
2. 在 `main.js` 中写入以下内容.(`vue` 里面有插件的知识，就是把 `element` 组件注册成全局的,想在哪用都行。)

```js
// main.js 中
import Vue from "vue";
import ElementUI from "element-ui";
import "element-ui/lib/theme-chalk/index.css";
import App from "./App.vue";

// 现在有了这句话无需在我的组件内引入了，可以直接使用了。
Vue.use(ElementUI); //全局使用 Element 库里的各种效果
new Vue({
  el: "#app",
  render: (h) => h(App),
});
```

3. 现在可以直接使用了，直接去官方的文档复制就可以了

```html
<el-button type="success" disabled>成功按钮</el-button>
```

#### 按需引入

借助 `babel-plugin-component`，我们可以只引入需要的组件，以达到减小项目体积的目的。

1. 首先，安装 `babel-plugin-component`：
   - 在 vue-ui-demos 包中的命令行输入

```js
npm install babel-plugin-component -D
```

2. (官方说的)然后，将 `.babelrc `修改为：

```js
{
  "presets": [["es2015", { "modules": false }]],
  "plugins": [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```

3. 但是我们只有 `babel.config.js`

```js
module.exports = {
  presets: ["@vue/cli-plugin-babel/preset"],
};
```

4. 把 `"plugins"` 粘过去就行了。

```js
module.exports = {
  presets: ["@vue/cli-plugin-babel/preset"],
  plugins: [
    [
      "component",
      {
        libraryName: "element-ui",
        styleLibraryName: "theme-chalk",
      },
    ],
  ],
};
```

5. `main.js` 中修改

```js
import Vue from "vue";
import App from "./App.vue";

import ElementUI from "element-ui";
import "element-ui/lib/theme-chalk/index.css";
Vue.use(ElementUI);

// import { Button,Switch} from 'element-ui';
// Vue.use(Button)
// Vue.use(Switch)

// 将 Message 方法添加到整个 Vue 的原型对象内，也就是整个项目内都可以使用 this.$message 访问
// Vue.prototype.$message = Message
Vue.config.productionTip = false;
new Vue({
  render: (h) => h(App),
}).$mount("#app");
```

6. 因为我们修改了 `babel.config.js` ，这个属于配置文件，配置文件需要重启服务器。
   - 就是把界面的 `serve` 停止，再重新开一下。

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

### Message 消息提示

##### 单一导入 && 全局导入

```js
// main.js
import { Button, Switch, Link, Message } from "element-ui";
Vue.prototype.$message = Message;
// 将 Message 方法添加到整个 Vue 的原型对象内，也就是整个项目内都可以使用 this.$message 访问，把 Message 当成 Vue 的一个公共方法，用 this.$message 进行访问。
// 特别特别的注意 是不加 Vue.use(Message) 的
// Vue.use(Message);
```

```html
<div>
  <el-button :plain="true" @click="success">成功</el-button>
  <el-button :plain="true">警告</el-button>
  <el-button :plain="true">消息</el-button>
  <el-button :plain="true">错误</el-button>
</div>
```

```js
import {Message} from 'element-ui'
// 此时导入的是一个 Message 函数
success() {
  // Message({
  //   message: "恭喜你，这是一条成功消息",
  //   type: "success",
  // });
  this.$message({
    message: "恭喜你，这是一条成功的消息",
    type: "success",
    duration: 1000,
  });
}
```
