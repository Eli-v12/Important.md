##### scss 安装使用

1. `Vue` 的单文件组件里的样式设置是非常灵活的。通过 `vue-loader`，你可以使用任意预处理器、后处理器，甚至深度集成 `CSS Modules` ——全部都在 `<style>` 标签内。
2. 使用工具包 sass-loader 把 scss 扩展语言编译成 css 语言。

- `Vue` 的单文件组件里的样式设置是非常灵活的。通过 `vue-loader`，你可以使用任意预处理器、后处理器，甚至深度集成 `CSS Modules`——全部都在 `<style>` 标签内。
- `scss` 语法就是 `css` 的扩展语法
- 默认我们先安装的 vue 环境是不支持 `scss` 语法的，需要安装工具
- 需要安装 `node.sass` 以及 `sass-loader` 不需要配置的东西，`使用依赖--> 开发依赖`
- 安装好了工具包之后就可以在组件内使用 `scss` 语法了

- 使用

```html
<div class="scss-demo">
  <h3>在 vue 中使用 scss 语法样式</h3>
  <h4>测试插值语句</h4>
</div>
```

```scss
// 整个项目的公共样式变量   public.scss
$border:1px solid #ccc;
<style lang="scss" scoped>

1. 样式嵌套  &  代表的是当前的标签名   样式表生成也是我们之前的 css 语法。
2. 设置变量  $color:teal;
3. 运算
4. @if 或者 for
5. 样式的导入 @import   assets 创建 public.scss @import '../assets/public.scss'
6. 插值语句 定义 $xxx:H3  使用 #{$xxx}

@import "../assets/public.scss";
$color: teal;
$height: 50px;
$nameH3: H3;
$nameH4: H4;
.scss-demo {
  #{$nameH3} {
    color: #000;
    border: $border;
    height: $height + 20px;
  }
  #{$nameH4} {
    color: blue;
    border: $border;
  }
  &:hover h3 {
    @if 5 < 3 {color: red}
    @if 1 + 1 == 2 {color: $color}
  }
}
</style>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201015210426442.png#pic_center)

#### less 安装使用

- 需要安装 less-loader 以及 less.scss 基础用法和 scss 一样没区别。

```html
<div class="less-demo"><h3>在 vue 中使用 less 语法写样式</h3></div>
```

```css
@color: #770fff;
.less-demo {
  h3 {
    color: @color;
  }
}
```

#### stylus 安装并使用

1. 原先在图形化界面中安装的 `stylus` 以及 `stylus-loader` 的 `4.1.1` 最新版本的，`Vue` 还未更新。
2. 所以必须使用命令行工具安装 `npm i stylus@3 -D` 安装之前的 3 版本。
3. 需要安装 `stylus` `stylus-loader` 注意 s`tylus-loader` 最近更新了 `4` 版本但是 `VueCli4` 能使用 `3` 版本，所以安装 `stylus` 的 `3` 版本才可以。
4. `vscode` 安装了 `vetur` 那么 `vue` 组件内的 `style` 写 `stylus` 样式的时候会自动补齐，不想自动补齐， 文件>首选项>设置>搜索` stylus>none` 关闭格式化
5. 在 `<sttle lang='stylus'>` 里面保存会自动的格式化。
   - 文件>首选项>设置>搜索 `fromat` 或者 `vetur` 再或者 `stylus `下 `Default Formatter:` 选中` none` 。

```css
<style lang="stylus">
.stylus
  h3
   color #ffff00
   font-size 20px
</style>
```

#### Flex 布局方式给页面排版布局

1. 哪都能用，不需要下载任何包，跟 `float` 一样,只是兼容性不好，只支持高版本的浏览器。
2. `Flex` 在 `Vue` 中随便用，注意，设为 `Flex` 布局以后，子元素的` float、clear` 和 `vertical-align` 属性将失效。
3. 不要混合式布局

**简介**

- `flex` 是一种弹性盒子布局方式
- 抛弃原来的 float 布局方式
- 设为 `Flex` 布局以后，子元素的 `float、clear 和 vertical-align` 属性将失效。
- `flex` 核心 学之前就要搞懂
- 容器：设置了 `display:flex;` 的元素就是容器
- 容器的轴线:分横向和纵向，默认主轴线是横向
- 项目: `display:flex;` 的子元素就是项目，项目并不会超出盒子，而且项目按照容器的主轴线排列，项目会自动转化为块元素，项目如果没有设置高度默认和容器的过渡一致，想竖排的就给容器修改轴线 `flex-direction:column`

```html
<div class="wrap">
  <div class="a"></div>
  <div class="b"></div>
</div>
```

```css
<style>
/* 如果 .wrap  没有高的话是撑不起来的，如果加了 flex布局的话这些问题就迎刃而解，不会超出，还会等比的缩小放大*/
.wrap {
  width: 200px;
  height: 200px;
  border: 2px solid blue;
  display: flex; /* 定义容器 */
  flex-direction: column;  /* 修改竖轴线 */
}
/* .a,
.b {
  height: 200px;
} */
.a {
  /* width: 80%; */
  height: 80%;
  background-color: #770fff;
}
.b {
  /* width: 40%; */
  height: 40%;
  background-color: #ffff00;
}
</style>
```
## 1015 Flex 布局样式

###### 主要讲

1. 看 `VueCli` 官方文档版本的信息,在 `npm` 查看 `stylus` 的版本资料
2. 面试官问你：对一个数组你怎么处理呀。你一脸蒙 B 了。
3. 以后还要讲 `webpack`
4. 讲上节课遗留的 `stylus` 问题,命令行安装 `npm i stylus@3 -D`,还有代码补全设置。
5. stylus 语法高亮
6. 昨天讲了 `Flex` 的三大核心。
7. 在 `Vue` 中使用原生的插件 `Swiper`
8. `FlexDemo1` 测试小例子
9. `Flex` 实现响应式布局

###### 应用 Flex 去做页面排版布局

1. `flex` 是一种弹性盒子布局方式
2. 抛弃原来的 `float` 布局方式
3. 设为 `Flex` 布局以后，子元素的 `float、clear 和 vertical-align` 属性将失效。
4. `flex` 核心 学之前就要搞懂了
5. 容器：设置了 `display:flex;` 的元素就是容器
6. 容器的属性: `felx-direction`(换方向) `flex-wrap`(换行) `flex-flow` (前面两者的简写) `justify-content`(规定项目主轴的排列顺序) `align-items`(规定项目在副轴的对齐顺序 `align-content`(多轴线，规定在副轴线的对齐方式)
7. 容器的轴线:分横向和纵向，默认主轴线是横向
8. 项目: `display:flex;` 的子元素就是项目，项目并不会超出盒子，而且项目按照容器的主轴线排列，项目会自动转化为块元素，项目如果没有设置高度默认和容器的过渡一致，想竖排的话容器 修改轴线 `flex-direction:column`
9. `order`(排列顺序) `flex-grow`(是否占满剩余空间) `flex-shrink`(是否缩小空间) `flex-basis` `flex`(前面三个的简写) `align-self`(单个的排列顺序)
10. `align-items`属性 是控制项目在副轴的排列顺序。如果项目没有设置副轴方向上的大小原本是和容器副轴大小一致，设置了 `align-items` 项目的大小就是项目本身内容的大小。

**四 项目的属性**

1. ` order` 属性定义项目的排列顺序。数值越小，排列越靠前，默认为 0。
2. `flex-grow`属性定义项目的放大比例，默认为 0，即如果存在剩余空间，也不放大，一个定义了之后，单单哪一个就全部占满了剩下的空间，如果是两个，那就是两个平分剩下的空间，三个也是平分剩下的空间，以此类推。
3. 如果所有项目的`flex-grow`属性都为 1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为 2，其他项目都为 1，则前者占据的剩余空间将比其他项多一倍。
4. 剩下 300px 一个设置为 1 一个设置为 2 那么就平分三份 `100px 200px` 总的来说就是设置了他们就占满剩余的空间
5. `flex-shrink`属性定义了项目的缩小比例，默认为 1，即如果空间不足，该项目将缩小。
6. 如果所有项目的`flex-shrink`属性都为 1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为 0，其他项目都为 1，则空间不足时，前者不缩小。 7.` align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为 auto，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch。`

7. 京东移动端
   - flex-direction:column
   - justify-content:space-between
   - justify-content:space-around
   - 垂直居中:align-items:center
   - 上中下占全屏居中。
8. 掘金左固定 200px 右侧随意放大缩小
   - 第一种掘金方案(建议使用)
   - 右侧 flex-grow:1 (放大)
   - 左侧 flex-shrink:0; (不缩小)
   - 第二种解决方案
   - 右侧的大小直接用 100%-200px
9. 网易云注册的字体对齐