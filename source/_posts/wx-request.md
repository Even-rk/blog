---
title: Promise 对 we.request 的封装，请求拦截器，响应拦截器
date: 2023-05-20 12:05:14
updated: 2023-05-20 12:06:23
cover: /img/wechat-http.jpeg
---

首先为什么需要封装，因为在开发中常常遇到，请求中需要携带 token 请求头，还有就是其他的一些逻辑，或者对响应数据的处理，根据接口响应过来的数据做判断，实现一些功能，但是原生小程序的请求中 wx.request 并没有这一项功能，而且也不支持promise，这个时候就需要自己封装一下，进行一个处理

我这里是封装的简易版的，能满足日常需求，直接上代码。

# 主要代码

```js
async function http(config) {
  // 请求函数开始执行的时候，运行加载中动画
  wx.showLoading({
    title: '加载中',
  })
  // 请求基地址，这里是演示默认地址
  const baseUrl = 'https://mock.boxuegu.com/mock/3293'
  // 这里是配置的请求拦截器，进入的时候，先走请求拦截器
  const options = await requestInterceptor({
    ...config,
    url: baseUrl + config.url,
  })
  return new Promise((resolve, reject) => {
    wx.request({
      ...options,
      success(response) {
        // 请求成功后，走响应拦截器
        resolve(responseInterceptor(response))
      },
      fail(error) {
        // 请求失败后，走响应拦截器
        reject(responseInterceptor(error))
      },
      complete() {
        // 请求完成，关闭 loading 动画
        wx.hideLoading()
      },
    })
  })
}
```

# 简易版请求

```js
// get 请求
http.get = (url, data) => {
  return http({ url, data, method: 'GET' })
}
// post 请求
http.post = (url, data) => {
  return http({ url, data, method: 'POST' })
}
// put 请求
http.put = (url, data) => {
  return http({ url, data, method: 'PUT' })
}
// delete 请求
http.delete = (url, data) => {
  return http({ url, data, method: 'DELETE' })
}
```

如果还有其他的 像put请求等，可以直接加
```js
// put 请求
http.put = (url, data) => {
  return http({ url, data, method: 'PUT' })
}
```



# 请求拦截器和响应拦截器

请求拦截器和响应拦截器就相对简单很多了

```js
// 请求拦截器
function requestInterceptor(options) {
  // 在发送请求之前做些什么
  return new Promise((resolve) => resolve(options))
}
// 响应拦截器
function responseInterceptor(response) {
  // 对响应数据做点什么
  return response.data
}
```

# 导出

```js
export default http
```

# 使用

以get请求为例

```js
import http from '../../utils/http' // 导入
Page({
  async getStudentList() {
    const res = await http.get('/students')
    console.log(res)
  },
  onLoad() {
    this.getStudentList()
  },
})
```

