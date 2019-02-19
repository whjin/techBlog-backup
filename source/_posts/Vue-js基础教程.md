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

```
<input type="text" v-model.trim="name" value="name">
```

## 懒加载`.lazy` ##

在离开`input`时才更新输入的内容，在`v-model`后加上`.lazy`即可。

## 限定输入数字`.number` ##

在`v-model`后加上`.number`即可。

## 遍历`v-for` ##

遍历有一个基本的模板：

```
<div id="app">
    <ul v-for="(item,index) in member" :key="index">
        <li>{{item}}</li>
    </ul>
</div>
```