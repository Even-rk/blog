---
title: js数字精度问题的处理
date: 2020-09-17 14:14:37
updated: 2020-09-17 19:20:47
cover: /img/number.jpg
---
在JavaScript中，计算两个十进制的和，它是把十进制转换成二进制来进行运算的，运算的结果在转换为十进制，对于整数来说可以很轻易转化成十进制或者二进制。但是对于一个浮点数来说，因为小数点的存在，小数点的位置不是固定的。这个时候就会出现精度丢失的问题

## 场景复现

我们在计算 0.1 + 0.1 的到的结果是 0.2，但是计算 0.1 + 0.2 的结果并不是0.3，而是0.30000000000000004

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/vr9H1NqIpnc0CpmINSeTr7JOycCRbdLe/number.jpg)

你可能会期望输出结果为0.3，但实际上由于浮点数表示的限制，结果会有微小的误差。

## 解决办法

### 1 : parentFloat(xxx.toPrecision(xx))

我们可以使用 js 内置的方法 `toPrecision` 凑整后再使用`parentFloat`

```js
const parse = parseFloat(0.30000000000000004.toPrecision(12))
consloe.log(parse)  // 0.3
```

可以单封封装一个函数用于复用

```js

function precision(num, parse) {
  return parseFloat(num.toPrecision(parse));
}

precision(1.6385000000000001, 1) // 2
precision(1.6385000000000001, 2) // 1.6
precision(1.6385000000000001, 3) // 1.64
```

### 2 : toFixed()

toFixed() 方法使用定点数表示法来格式化一个数字，返回值为String类型。

以下是一个使用`toFixed()`函数解决精度丢失问题的示例:

```js
const num = 0.1 + 0.2;
const parse = num.toFixed(1);
console.log(parse); // 输出结果为 "0.3"
```

### 3 : 第三方数字运算库(推荐)

[bignumber.js](https://github.com/MikeMcl/bignumber.js)，[decimal.js](https://github.com/MikeMcl/decimal.js)，以及[big.js](https://github.com/MikeMcl/big.js)等 



## 在JavaScript中，精度问题是无法完全避免的，但可以通过上述方法来尽可能地减少误差。



