---
title: async/await 异常捕获 代替 try--catch
date: 2021-03-15 10:13:23
updated: 2021-03-15 10:14:05
cover: /img/async:await.jpeg
---

看到捕获异常，一想到的就是 try--catch 可能单看try--catch 是没什么问题，但是对于我这种有点强迫症的来说，感觉不美观，而已感觉逻辑上像是，中间给截掉了一样，而且代码量也会变多，如果每个请求的地方都添加 try-catch，可想而之

如何让代码变得更优雅，这里分享我一直都在使用的一个方法 await-to-js

# await-to-js 

使用方法非常简单，就是代替了 try--catch 去处理异常，抛出异常

## 1，下载 await-to-js 

```bash
# use npm
npm i await-to-js --save

# use yarn
yarn add await-to-js --save
```

## 2，项目中使用

```js
import to from 'await-to-js'

(async () => {
  const [err, data] = await to(axios.get('填写你的接口地址')
  // err 是拿到的 错误信息，data 是请求成功的数据
  // 当请求成功的使用 err 为 null
  if(!err) return
})()
```

这样一看代码就很简洁了，强迫症专用
