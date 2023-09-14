---
title: EmptyStatus
---

业务空状态组件。

## 引入

```js
import {EmptyStatus} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
<EmptyStatus />
```

## 暂无数据

```jsx live fff
<EmptyStatus status="NO_DATA" />
```

## 没有访问权限

```jsx live fff
<EmptyStatus status="NO_AUTH" />
```

## 无法找到页面

```jsx live fff
<EmptyStatus status="NO_PAGE" />
```

## 服务器错误

```jsx live fff
<EmptyStatus status="SERVER_ERROR" />
```

## API

| 属性   | 说明       | 类型                                            | 默认值 |
| ------ | ---------- | ----------------------------------------------- | ------ |
| status | 空状态类型 | `NO_DATA`〡`NO_AUTH`〡`NO_PAGE`〡`SERVER_ERROR` | `--`   |
