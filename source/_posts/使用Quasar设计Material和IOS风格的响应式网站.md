---
title: 使用Quasar设计Material和IOS风格的响应式网站
date: 2019-02-23 18:37:28
category: ["前端"]
tags: ["Vue.js","Quasar","Material","IOS","响应式","网站"]
comments:
---

# Quasar #

`Quasar`是一款基于`Vue.js`开发的`UI`框架，可以让你轻松构建网站简洁明快的界面，更重要的是它还能让你轻松做好`RWD`（响应式网站设计），除此之外还能帮助你加上`PWA`，使你的网页变成手机上的`App`。

<!--more-->

以下内容来自官网[Quasar Framework](http://www.quasarchs.com/)，概括了`Quasar`的主要特点。

`Quasar`是`MIT`许可的开源框架（基于[Vue](https://cn.vuejs.org/)），可帮助`Web`开发人员创建：

- 响应式网站
- `PWA`
- 通过`Apache Cordova`构建移动`App`
- 多平台桌面应用程序（使用`Electron`）

## 选择Quasar的5个理由 ##

1. 内建了`Material`及`IOS`两种主题
2. 组件均内建`RWD`快速响应
3. 多样的基础`UI`组件库
4. 自带了`Vuex`、`VueRouter`、`Vuei18n`（多国语系）
5. 强大的部署工具

## 安装指南 ##

首先安装`Node.js`和`vue-cli`，具体安装方法查看官网资料。

然后安装`Quasar`，`npm install -g quasar-cli`。

最后搭建项目：`quasar init <folder name>`

取代`main.js`的`quasar.config.js`设置文件：

- 引用Quasar内建的组件，可以不用在每个地方`import components`
- `i18n`设置多国语系
- `icons`移除注释即可使用
- `开发模式`下的HTTPS以及`port`设置
- `CSS`动画设置
- 其他外部插件的设置
- `PWA`、`manifest`等设置

### `quasar.config.js` ###

- `plugins`

以前在`Vue`安装其他的`plugin`会在`main.js`里引入，而在`Quasar`就会取代`main.js`成为全部配置文件。

- `css`

CSS的引入都会放在这个文件，预设的位置`/src/css`，所需的CSS库已经准备好，可以直接使用。

- `extra`

这里是设置是否引入[quasar-extras](https://github.com/quasarframework/quasar-extras)的内容。

|Package|name|说明|
|-------|----|----|
|Roboto Font|`roboto-font`|Material主题的建议字体|
|Roboto Font Latin Extended|`roboto-font-latin-ext`|Material主题的建议字体|
|[Material Icons](https://material.io/tools/icons/?style=baseline)|`material-icons`|Material风格的`icon`|
|MDI (Material Design Icons)|`mdi`|Material风格的`icon`扩展|
|Font Awesome|`fontawesome`|自由选择`icon`|
|[Ionicons](https://ionicons.com/)|`ionicons`|`ionicons`的`icon`|
|Animate.css|`animations`|网页组件动画|

- `scopeHoiting`

预设`true`，用来提升`webpack`运行时的性能

- `VueRouterMode`

设置`Vue Router`的模式，有`history`、`hash`两种值。

- `vueCompiler`

包含两种Vue的编译模式`vue runtime`+`compiler`，预设只有`runtime-only`运行时编译

- `gzip`

使网站支持`gzip`的格式。

- `analyze`

在`build`时会运行`webpack-bundle-analyzer`工具。

![](https://d1dwq032kyr03c.cloudfront.net/upload/images/20181017/20111805z6Qs0mgwUv.png)

- `extractCSS`

提取CSS到文件中。[VueLoader](https://vue-loader-v14.vuejs.org/zh-cn/configurations/extract-css.html)

- `extendWebpack`

在`dev`模式中服务器的设置。


- `https`

- `port`

设置成指定的`port`，当quasar在运行`dev`模式时，遇到相同的`port`时会自己再`+1`。

- `open`

是否在`dev`指令执行完成后，自动开启此网站的分页在浏览器上。

### Layout ###

`quasar dev`打开初始页面，页面的`header`和`drawer`都是在`layout/MyLayout.vue`里。

![](https://ithelp.ithome.com.tw/upload/images/20181018/20111805omoWvkNkQj.png)

一些常用的属性：

|属性|取值|说明|
|---|---|----|
|`side`|`String`|有两个值`left`，`right`，决定要出现在左边还是右边|
|`overlay`|`Boolean`|设置侧边栏弹出时是挤压`q-page-container`还是直接盖在上面|
|`content-style`|`Object`|设置侧边栏的CSS|
|`content-class`|`String/Object/Array`|设置侧边栏的`class`|
|`mini`|`Boolean`|把侧边栏缩小到只有`icon`|

> 这里的CSS要用`Object`的方式传入。

```html
:content-style="{color: 'red'}"
```

## 旅游网站-Header ##

**演示项目：**

- Toolbar
- ToolbarTitle
- Button

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html" data-user="whjin" data-slug-hash="MLNxZN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="旅游网站-Header">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/MLNxZN/">
  旅游网站-Header</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### Toolbar ###

- `color`

Quasar内建色：[color-palette](http://www.quasarchs.com/components/color-palette.html)

在`/src/css/themes/common.variables.styl`里面增加调色板的颜色。

- `inverted`

让**背景色**变成**白色**，然后使原来白色的文字变成设置的**背景色**。

- `glossy`

加上玻璃效果

### QToolbarTitle ###

- `gt-xs`

用来设置显示像素高于`576px`的页面样式。

- `q-mr-md`

`mr`等于`margin-right`
`sm`就是`size`的值为`small`

![](https://ithelp.ithome.com.tw/upload/images/20181019/20111805O7e642RHjY.png)

**其他非外观的功能属性：**

- `disable`，`:disable="true"`时按钮禁用
- `label`设置按钮的文字
- `type`可以是`button`、`submit`、`reset`其中一种
- `loading`，值为`true`显示读取中
- `percentage`显示读取的圆圈，要跟`loading`一起使用
- `dark-percentage`用在亮色系的按钮上

### List&ListItem ###

**修改Drawer**

- `v-model="rightDrawerOpen"`控制弹出侧边栏的位置
- `content-class="bg-grey-10"`背景色
- `side="right"`按钮设置在多边

设置了`rightDrawerOpen`需要加到`data`里。

```javascript
export default {
  name: 'MyLayout',
  data () {
    return {
      rightDrawerOpen: false
    }
  }
}
```

### 手机端按钮 ###

控制显示的`class`用`lt-sm`只要像素小于`sm(768px)`就会显示该区域。

### 设置List和`ListItem` ###

**使用Dark属性使得组件内容在暗色背景下更好显示**

List中可用组件，这些组件需要自己去配置文件中自行引入。

- `QListHeader`List上的标题
- `QItemSeparator`分割线
- `QItem`
- `QItemSide`可分成左右两侧的区块
- `QItemMain`中间的区块
- `QItemTitle`区块中的标题

## 旅游网站-Carousel(页面轮播) ##

### 建立新的首页 ###

在`src/pages/`下新建`Index`文件夹，并在此文件夹下新建`Index.vue`作为首页，删除原来的`Index.vue`文件。

### 修改Vue Router ###

在`src/router/routers.js`修改`Index.vue`的路径。

### 建立轮播的区块 ###

在`src/pages/Index`下新建`SectionCarousel.vue`，并在`Index.vue`中引入。

然后再`template`下的`q-page`中加入`section-carousel`

```html
<template>
  <q-page>
    <section-carousel></section-carousel>
  </q-page>
</template>
```

### 开始写轮播 ###

[官方Carousel](http://www.quasarchs.com/components/carousel.html)

在设置文件`quasa.config.js`中引入：

```javascript
framework: {
  components: [
    'QCarousel',
    'QCarouselSlide',
    'QCarouselControl'
    ...
  ],
}
```

### 加入轮播的图片/页面 ###

```html
<template>
  <q-carousel
    color="white"
    infinite
    arrows
    autoplay
    height="400px"
  >
    <q-carousel-slide img-src="statics/images/papercut1.jpg"/>
    <q-carousel-slide img-src="statics/images/papercut2.jpg"/>
  </q-carousel>
</template>
```

### 加入文字区块 ###

Quasar在`carousel`中有个子组件`QCarouselControl`用来自定义按钮在页面上。

根据官方文档的范例，`QCarouselControl`要放在`QCarousel`的最后面，也就是`QCarouselSlide`的后面。

```html
<q-carousel-control
  position="center"
  slot="control-nav"
  slot-scope="carousel"
  class="carouselInput">
</q-carousel-control>
```

在`q-carousel-control`中加入内容：

```html
<div class="main">
  <h6 class="title">新锐旅游网站</h6>
  <p class="subtitle">您身边的好玩专家</p>
  <p>发现周边好玩的地方，玩得快乐，玩得精彩。</p>
</div>
```

### 加上CSS ###

```css
<style lang="stylus" scoped>
  .carouselInput {
    width: 90%
  }

  .carouselInput .main {
    text-align center
    color: #f50057
  }

  .carouselInput .title {
    font-size 48px
  }

  .carouselInput .subtitle {
    font-size 24px
  }
</style>
```

### 调整手机版CSS ###

```css
@media (min-width: 768px) {
  .carouselInput .title {
    font-size 48px
  }

  .carouselInput .subtitle {
    font-size 24px
  }
}

@media (max-width: 768px) {
  .carouselInput .title {
    font-size 24px
  }

  .carouselInput .subtitle {
    font-size 16px
  }
}
```

## 旅游网站-搜索框 ##

### 加入搜索框 ###

**`input`**

首先到`quasar.config.js`中引入`QInput`

```javascript
framework: {
  components: ['QInput']
}
```

在`<div class="main">`后面加入`q-input`内容：

```html
<q-input
  inverted-light
  color="white"
  placeholder="输入城市/景点 或是想去的地方"
  :after="[{icon:'fas fa-search-location'}]"
  v-model="search">
</q-input>
```

- `inverted`显示**背景**
- `color`主题颜色
- `after`用来显示输入框前后`icon`

最后绑定`v-model="search"`，此时需要在`data`中添加`value`值，否则会报错。

```javascript
  data() {
    return {
      search: ''
    }
  }
```

### 调整排版 ###

> 使用[Flex CSS](http://www.quasarchs.com/components/flex-css.html)调整组件长度。

```html
<div class="row">
  <div class="col-md-2 col-xs-1"></div>
  <div class="col-md-8 col-xs-10">
    <q-input ...></q-input>
  </div>
  <div class="col-md-2 col-xs-1"></div>
</div>
```

### 自动填入`autocomplete` ###

引入`QAutocomplete`组件：

```javascript
framework: {
  components: ['QAutocomplete']
}
```

加入`q-autocomplete`：

```html
<q-input ...>
  <q-autocomplete :static-data="{field: 'label', list: countries}"/>
</q-input>
```

- `static-data`
    - `field`用于搜索数据的栏位
    - `list`搜索的数据来源

### 设置静态数据 ###

```javascript
countries: [
  {label: '广州市', icon: 'fas fa-map-marker-alt'},
  {label: '深圳市', icon: 'fas fa-map-marker-alt'},
  {label: '珠海市', icon: 'fas fa-map-marker-alt'},
  {label: '[网美景点]香山公园，秋季赏枫胜地', stamp: '北京市'},
  {label: '珠海长隆[海豚剧场]精彩不容错过！精彩变身演出抢先看', stamp: '珠海，长隆', rightTextColor: 'pink-13'}
]
```






