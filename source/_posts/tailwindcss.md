---
title: 在 vue/react 项目中如何使用 tailwindcss
date: 2021-02-26 17:10:17
updated: 2021-02-26 17:13:34
cover: /img/tailwindcss.jpeg
---

Tailwind CSS，是一个CSS库，它为我们提供了构建定制设计而无需使用自定义样式所需的所有构建块。可以以直接添加类名的方式构建页面布局。简化样式，更少地编写自定义的 CSS。

[中文官网 : https://www.tailwindcss.cn/](https://www.tailwindcss.cn/)

[英文官网 : https://tailwindcss.com/](https://tailwindcss.com/)

下面是介绍如何在前端开发中 （ vue/react ）使用 Tailwind CSS

# 1，创建项目

这里创建项目是以 vite 为例子，所以 vue 和 react 中使用 Tailwind CSS 方法是一样的

```bash
# vue
pnpm create vite tailwindcss-vue --template vue  
# react
pnpm create vite tailwindcss-react --template react  
```

然后进入到创建好的项目目录中下载依赖

## 2，在 项目 中下载tailwindcss依赖

在 vue/react 项目中使用 tailwindcss 需要依赖于 postcss autoprefixer 两个插件，这里一起下载就可以

```bash
pnpm i -D tailwindcss postcss autoprefixer 
```

# 3，创建配置文件

```bash
npx tailwindcss init -p
```

使用命令执行后 会生成两个文件 postcss.config.js 和 tailwind.config.js 两个配置文件，更改配置如下

```js
// postcss.config.js
import tailwindcss from 'tailwindcss'
import autoprefixer from 'autoprefixer'
export default {
  plugins: [tailwindcss, autoprefixer]
}

//  tailwind.config.js
/** @type {import('tailwindcss').Config} */
export default {
  // react
  content: ['./index.html', './src/**/*.{js,jsx,ts,tsx}'],  
  // vue
  // content: ['./index.html', './src/**/*.vue'],  
  darkMode: false,
  theme: {
    extend: {}
  },
  plugins: []
}
```

# 4，新建一个tailwind.css文件

**使用 @tailwind 指令注入 Tailwind 的基础 (base)，组件 (components) 和功能 (utilities) 样式**

在src文件夹下 创建一个tailwind.css文件，并在文件中写入如下代码

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

⚠️：这里vscode 可能会有提示标黄

解决办法：在跟路径下创建一个 .vscode文件夹, 文件夹内创建 settings.json 

```json
{
    "css.lint.unknownAtRules": "ignore"
}
```

这样vscode就不会标黄了

# 5，将tailwind.css文件引入到main.js文件中

```js
import './tailwind.css'
```

# 6，在组件中使用，启动项目

### **react**
```jsx
export default function App() {
  return (
    <div className="text-3xl font-bold bg-red-500 w-56">
      hello word!
    </div>
  )
}
```
### **vue**
```html
<template>
  <div className="text-3xl font-bold bg-red-500 w-56">
    hello word!
  </div>
</template>
```
## 演示效果
![image](http://lc-u11PV6WA.cn-n1.lcfile.com/UPmCV1w7jVlnwr9GLecREnx5FxnpYwxl/tailwindcss.jpg)