---
title: Vue.js基础教程
date: 2019-02-18 23:34:23
category: ["前端"]
tags: ["Vue.js"]
---

开发工具准备：

1. 根据个人喜欢选择`IDE`，我使用的是`WebStorm`，推荐使用`Atom`和`VSCode`；
2. 安装`git base`和`node.js`；
3. 安装`vue-cli`，命令`npm i -g @vue/cli`；
4. 新建`vue-cli`项目：
    1. 方法一：通过图形界面进行安装`vue ui`；
    2. 方法二：通过命令行安装`vue create project-name`
5. 运行项目`npm run serve`，端口`8080`。

<!--more-->

## 双向绑定v-model ##

双向绑定大多用于表单事件，通过监听使用者输入的事件来更新内容。

现阶段大部分工作在`App.vue`上，`template`与普通写法一致，`js`写法：

```javascript
export default {
    name: 'app',
    data() {
        return {
            title: 'vue.js',
            myname: '请输入名字'
        }
    }
}
```

## 去掉空白符`.trim` ##

直接在`v-model`后加上`.trim`即可。

```html
<input type="text" v-model.trim="name" value="name">
```

## 懒加载`.lazy` ##

在离开`input`时才更新输入的内容，在`v-model`后加上`.lazy`即可。

## 限定输入数字`.number` ##

在`v-model`后加上`.number`即可。

## 遍历`v-for` ##

遍历有一个基本的模板：

```html
<div id="app">
    <ul v-for="(item,index) in member" :key="index">
        <li>{{item}}</li>
    </ul>
</div>
```

## 组件`component` ##

在`App.vue`中引入`components`中的组件：

```javascript
<template>
  <div id="app">
    <Card />
  </div>
</template>

<script>
  import Card from './components/Card'
  
  export default {
    components: {
      Card
    }
  }
</script>
```

## 数据传递`props` ##

```html
<template>
    <div id="app">
        <Card :cardData="cardData"/>
    </div>
</template>
```

其中`:cardData="cardData"`是这个组件的核心，用于绑定属性`cardData`。其他数据展示工作放在`Card.vue`组件中进行。

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js" data-user="whjin" data-slug-hash="darQdg" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="props接收数据">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/darQdg/">
  props接收数据</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

这里解析一下`<div class="card_wall"></div>`包裹`<div class="card"></div>`主要是方便后期应用扩展，以及让应用整体更稳定。

## 生命周期 ##

我不喜欢用官网的生命流程图来讲解这个内容，使用文字表达更加让思维清晰。

1. **初始化**：设置数据监听，编译模板，挂载到`DOM`并在数据变化时更新`DOM`等；
2. 生命周期钩子：其实就是一个过程处理，类似于服务站。

**生命周期钩子简介**

1. `beforeCreate`：实例初始化
2. `created`：实例建立完成（可以取得`$data`）
3. `beforeMount`：模板挂载之前（还没有生成`html`）
4. `mounted`：模板挂载完成
5. `beforeUpdate`：如果`data`发生变化，触发组件更新，重新渲染
6. `updated`：更新完成
7. `beforeDestroy`：实例销毁之前（实例还可以使用）
8. `destroyed`：实例已销毁（所有绑定被解除、所有事件监听器被移除、所有子实例被移除）

生命周期钩子用得最多的是`mounted`，主要用在调用属性、方法的时候，

## 指令 ##

### `v-once`指令 ###

