---
title: request
---

基于 axios 的 http 请求类，针对 acu 的接口格式进行了封装。支持 GET、POST、PUT 操作。

## 引入

```js
import {utils} from 'baidu-acu-react-common';

const request = utils.request;
```

## 基本用法

```js
import {utils} from 'baidu-acu-react-common';

const request = utils.request;

const demoDetail = await request.post('/api/demo/detail', {id});
request.get('/api/demo/list').then(result => console.log(result));
```
