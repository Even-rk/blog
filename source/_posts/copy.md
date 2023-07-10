---
title: 项目中的（剪切板）vue/react
date: 2023-01-12 09:44:15
updated: 2023-01-12 09:50:36
cover: /img/copy.jpeg
---

在开发项目的时候，往往有个别项目需求，一段内容需要当点复制的时候，可以复制这段内容，直接到自己手机或者电脑的剪切板，可以方便的实现复制，而不是，需要拖拽选中的实现 cv ，实现复制，可以使用一些第三方的插件来实现。

下面分别是vue2，vue3 和react的实现方法

# Vue2

#### 1：安装 vue-clipboard2

```bash
# npm
npm install vue-clipboard2
# yarn
yarn add vue-clipboard2
# pnpm 
pnpm install vue-clipboard2
```

#### 2：在main.js中注册

```js
import Vue from "vue";
import App from "./App.vue";
import VueClipboard from "vue-clipboard2";

Vue.config.productionTip = false;

Vue.use(VueClipboard);

new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

#### 3：组件中使用

在组件中使用有两种方法

- 直接将变量内容复制至剪切板

```html
<template>
  <div>
    <!-- v-clipboard:copy 绑定需要被复制的内容 -->
    <!-- v-clipboard:success 绑定成功的回调 -->
    <!-- v-clipboard:error 绑定失败的回调 -->
    <button
      type="button"
      v-clipboard:copy="msg"
      v-clipboard:success="success"
      v-clipboard:error="error"
    >
      复制
    </button>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Copy These Text'
    }
  },
  methods: {
    // 复制成功的函数
    success(e) {
      alert('复制成功', e.text)
    },
    // 复制失败的函数
    error() {
      alert('复制失败')
    }
  }
}
</script>
```

- VUE响应函数方式

```html
<template>
  <div>
    <button type="button" @click="onCopy">复制</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Copy These Text'
    }
  },
  methods: {
    async onCopy () {
      try {
        const copyRes = await this.$copyText(this.msg)
        alert('复制成功', copyRes.text)
      } catch (error) {
        alert('复制失败', error)
      }
    }
  }
}
</script>
```

# Vue3

vue3中的相对vue2就简单了很多

#### 1：安装 vue-clipboard2

```bash
# npm
npm install vue-clipboard3
# yarn
yarn add vue-clipboard3
# pnpm 
pnpm install vue-clipboard3
```

#### 2：直接在组件中使用

示例代码

```html
<template>
  <button @click="Copy">复制链接</button>
</template>

<script setup>  // 这是使用了setup语法糖
import useClipboard from 'vue-clipboard3'

const Copy = () => {
  copy('拷贝内容')
}

const { toClipboard } = useClipboard()
// meg接收到的就是需要拷贝的内容
const copy = async (msg) => {
  try {
    await toClipboard(msg)
    alert('拷贝成功')
  } catch (error) {
    alert('复制失败', error)
  }
}
</script>
```

# React

#### 1：安装 react-copy-to-clipboard

```bash
# npm
npm install react-copy-to-clipboard
# yarn
yarn add react-copy-to-clipboard
# pnpm 
pnpm install react-copy-to-clipboard
```

#### 2：直接在组件中使用

```jsx
import { CopyToClipboard } from 'react-copy-to-clipboard'

export default function App() {
  return (
    <div>
      <CopyToClipboard
        text={'需要复制的内容'}
        onCopy={() => {
          alert('复制成功')
        }}
      >
        <button>复制</button>
      </CopyToClipboard>
    </div>
  )
}
```

