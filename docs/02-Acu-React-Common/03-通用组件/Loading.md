---
title: Loading
---

Loading 组件，用于页面局部处于等待时缓解用户焦虑。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const Loading = components.Loading;
```

## 基本用法

```jsx live fff unfold
<Loading />
```

## 自定义提示文字

```jsx live fff unfold
<Loading text="读取中" />
```

## API

| 参数 | 说明     | 类型     | 默认值            |
| ---- | -------- | -------- | ----------------- |
| text | 配置文案 | `string` | `'玩命加载中...'` |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/Loading>
