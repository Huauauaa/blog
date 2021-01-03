---
title: Vue Packaging Optimization
date: '2021-01-03'
description: 'something about vue build'
---

关于 vue 打包的一些方法

### 懒加载

```js
const HelloWorld = () => import('../components/HelloWorld.vue');
```

### CDN

一些 [CDN](https://developer.mozilla.org/zh-CN/docs/Glossary/CDN) 网站

[<img src="https://www.jsdelivr.com/img/icon_256x256.png" height="30px">](https://www.jsdelivr.com/)
[<img src="https://www.bootcdn.cn/assets/ico/favicon.ico" height="30px">](https://www.bootcdn.cn/)
[<img src="https://unpkg.com/favicon.ico" height="30px">](https://unpkg.com/)
[<img src="http://www.staticfile.org/assets/images/logo.png" height="30px">](http://www.staticfile.org/)

`vue.config.js` 中添加 [externals](https://webpack.js.org/configuration/externals/)

> key 为包名, value 为 cdn 文件中暴露的变量

```js
configureWebpack: config => {
  if (process.env.NODE_ENV === 'production') {
    config.externals = {
      vue: 'Vue',
      'vue-router': 'VueRouter',
      'element-ui': 'ELEMENT',
    };
  } else {
    // 为开发环境修改配置...
  }
},
```

`public/index.html`

```html
<head>
  <% if(process.env.NODE_ENV === 'production') { %>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12" rel="prefetch"></script>
  <% } %>
</head>
```

### 按需引入

例: element-ui

全部引入

```js
import ElementUI from 'element-ui';
import Vue from 'vue';
Vue.use(ElementUI);
```

部分引入

```js
import { Input, Button } from 'element-ui';
```

### 使用小体积版本

例: lodash-es 替换 lodash

```bash
npm i lodash-es
```
