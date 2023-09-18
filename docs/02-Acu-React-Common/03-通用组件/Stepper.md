---
title: Stepper
---

步进器组件。

- 同 InputNumber 组件

## 引入

```js
import {components} from 'baidu-acu-react-common';

const Stepper = components.Stepper;
```

## 基本用法

```jsx live fff
<Stepper min={1} max={60} defaultValue={3} />
```

## 不同尺寸

```jsx live fff
<div className="acux-demo-column">
    <Stepper size="small" />
    <Stepper size="large" />
</div>
```

## 禁用模式

```jsx live fff
<Stepper disabled />
```

## API

参考 [InputNumber](https://ant.design/components/input-number-cn/)

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/Stepper>
