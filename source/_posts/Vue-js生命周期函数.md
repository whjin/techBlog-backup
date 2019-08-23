---
title: Vue.js生命周期函数
date: 2019-08-23 10:14:50
category: ["Vue.js"]
tags: ["Vue.js","生命周期函数"]
comments: true
---


# 生命周期函数表 #

|生命周期函数|含义|
|---|---|
|`beforeCreate`（创建前）|组件实例刚被创建，组件属性计算之前，比如`data`属性等|
|`created`（创建后）|组件实例刚创建完成，属性已经绑定，此时`DOM`还未完成，`$el`属性还不存在|
|`beforeMount`（载入前）|模板编译、挂载之前|
|`mounted`（载入后）|模板编译、挂载之后|
|`beforeUpdate`（更新前）|组件更新之前|
|`updated`（更新后）|组件更新之后|
|`beforeDestroy`（销毁前）|组件销毁前调用|
|`destroyed`（销毁后）|组件销毁后调用|

<!--more-->