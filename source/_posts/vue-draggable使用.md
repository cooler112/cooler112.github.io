---
title: vue-draggable使用
date: 2021-01-16 11:23:12
tags: vue
categories: 前端开发
---

在Vue业务开发中，会用到功能菜单的位置变换，比如支付宝的菜单换行， 是怎么实现的呢？

可以直接使用Vue的draggable组件

安装方式：

```
npm i vuedraggable
```

页面引用

```
import vuedraggable from 'vuedraggable'
......
  components: {
    vuedraggable
  },
```

直接使用,可以在内部添加简单动画

```
 <vuedraggable 
 	v-model="menus" 
 	dragable="true" 
  @change="change"
  @start="start"
  @end="end"
  :move="move"
  :disabled="isEdit">
    <transition-group class="my-func-group">
      <div
      class="menu-item menu-item-drag"
      v-for="item in menus"
      :key="item.bh"
      >
        <div class="func-icon-wrapper" @click.stop="fnClick(item)">
        <img class="func-icon" :src="item.realUrl" />
      </div>
      	<div class="menu-text">{{ item.mc }}</div>
      </div>
    </transition-group>
  </vuedraggable>
```

另外切换的元素本身是可以点击的，需要添加@click.stop禁止点击元素向上传递事件

