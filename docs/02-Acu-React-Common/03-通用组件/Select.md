---
title: Select
---

标签选择组件。

- 支持选择多个标签
- 支持展开收起
- 支持全选功能

## 引入

```js
import {components} from 'baidu-acu-react-common';

const Select = components.Select;
```

## 基本用法

```jsx live fff
function App() {
    function handleChange(value) {
        console.log(`selected ${value}`);
    }

    return (
        <Select onChange={handleChange}>
            <Option value="data1">data1</Option>
            <Option value="data2">data2</Option>
            <Option value="data3">data3</Option>
        </Select>
    );
}
```

## 列表写法

传入 `options` 的写法：

```jsx live fff
function App() {
    function handleChange(value) {
        console.log(`selected ${value}`);
    }

    const optionsDemo = [
        {value: 'data1', label: 'data1'},
        {value: 'data2', label: 'data2'}
    ];

    return (
        <Select options={optionsDemo} onChange={handleChange} />
    );
}
```

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/Select>
