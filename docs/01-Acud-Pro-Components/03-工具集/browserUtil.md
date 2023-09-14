---
title: browserUtil
---

浏览器相关工具。

## 引入

```js
import {browserUtil} from '@baidu/acud-pro-components';

const {isBrowser, isAbsolutePath, isScrollBottom} = utils.browserUtil;
```

## 是否是浏览器环境

`isBrowser` 用于判断当前是否为浏览器环境。

```js
isBrowser()
```

## 是否是 http 绝对地址

`isAbsolutePath` 用于判断指定字符是否是 http 绝对地址。

```js
isAbsolutePath('https://www.baidu.com/') // true
isAbsolutePath('/a/b/c') // false
```

## 页面是否滚到底部

`isScrollBottom` 用于判断页面是否滚到底部。

```js
if (isScrollBottom()) {
    console.log('到达底部了');
}
```
