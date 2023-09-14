---
title: cookieUtil
---

cookie 相关工具。

## 引入

```js
import {cookieUtil} from '@baidu/acud-pro-components';

const {getCookie, setCookie, removeCookie} = cookieUtil;
```

## 获取 Cookie

`getCookie` 用于获取 Cookie。

```js
getCookie('aa');
```

## 设置 Cookie

`setCookie` 用于设置 Cookie。

```js
setCookie('aa', 'bbb');
```

## 删除 Cookie

`removeCookie` 用于删除 Cookie。

```js
removeCookie('aa');
```
