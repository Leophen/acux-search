---
title: Status
---

状态组件。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const {Status} = components;
```

## 基本用法

```jsx live fff
<Status />
```

## 不同状态

通过 `type` 属性控制不同类型的状态。

```jsx live fff
<div className="acux-demo-row">
    <Status type="success" text="运行成功" />
    <Status type="error" text="运行错误" />
    <Status type="warning" text="请注意" />
    <Status type="unavailable" text="等待中..." />
    <Status type="pending" text="运行中" />
</div>
```

## API

| 参数 | 说明     | 类型                                                    | 默认值 |
| ---- | -------- | ------------------------------------------------------- | ------ |
| type | 状态类型 | `success`〡`error`〡`warning`〡`unavailable`〡`pending` | `--`   |
| text | 状态文本 | `string`                                                | `--`   |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E4%B8%9A%E5%8A%A1%E7%BB%84%E4%BB%B6/Status>
