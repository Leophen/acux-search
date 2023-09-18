---
title: TagSelect
---

标签选择组件。

- 支持选择多个标签
- 支持展开收起
- 支持全选功能

## 引入

```js
import {components} from 'baidu-acu-react-common';

const TagSelect = components.TagSelect;
```

## 基本用法

```jsx live fff
function App() {
    const TYPE_DATASOURCE = [
        {value: 'cat1', text: '类目一'},
        {value: 'cat2', text: '类目二'},
        {value: 'cat3', text: '类目三'},
        {value: 'cat4', text: '类目四'},
        {value: 'cat5', text: '类目五'},
        {value: 'cat6', text: '类目六'},
        {value: 'cat7', text: '类目七'},
        {value: 'cat8', text: '类目八'},
        {value: 'cat9', text: '类目九'},
        {value: 'cat10', text: '类目十'},
        {value: 'cat11', text: '类目十一'},
        {value: 'cat12', text: '类目十二'},
        {value: 'cat13', text: '类目十三'},
        {value: 'cat14', text: '类目十四'}
    ];

    return (
        <TagSelect value={['cat1', 'cat3']}>
            {TYPE_DATASOURCE.map(type => (
                <TagSelect.Option value={type.value}>{type.text}</TagSelect.Option>
            ))}
        </TagSelect>
    );
}
```

## 支持打开收起

```jsx live fff
function App() {
    const TYPE_DATASOURCE = [
        {value: 'cat1', text: '类目一'},
        {value: 'cat2', text: '类目二'},
        {value: 'cat3', text: '类目三'},
        {value: 'cat4', text: '类目四'},
        {value: 'cat5', text: '类目五'},
        {value: 'cat6', text: '类目六'},
        {value: 'cat7', text: '类目七'},
        {value: 'cat8', text: '类目八'},
        {value: 'cat9', text: '类目九'},
        {value: 'cat10', text: '类目十'},
        {value: 'cat11', text: '类目十一'},
        {value: 'cat12', text: '类目十二'},
        {value: 'cat13', text: '类目十三'},
        {value: 'cat14', text: '类目十四'}
    ];

    return (
        <TagSelect expandable>
            {TYPE_DATASOURCE.map(type => (
                <TagSelect.Option value={type.value}>{type.text}</TagSelect.Option>
            ))}
        </TagSelect>
    );
}
```

## 单选模式

```jsx live fff
function App() {
    const TYPE_DATASOURCE = [
        {value: 'cat1', text: '类目一'},
        {value: 'cat2', text: '类目二'},
        {value: 'cat3', text: '类目三'},
        {value: 'cat4', text: '类目四'},
        {value: 'cat5', text: '类目五'},
        {value: 'cat6', text: '类目六'},
        {value: 'cat7', text: '类目七'},
        {value: 'cat8', text: '类目八'},
        {value: 'cat9', text: '类目九'},
        {value: 'cat10', text: '类目十'},
        {value: 'cat11', text: '类目十一'},
        {value: 'cat12', text: '类目十二'},
        {value: 'cat13', text: '类目十三'},
        {value: 'cat14', text: '类目十四'}
    ];

    return (
        <TagSelect mode="single" expandable>
            {TYPE_DATASOURCE.map(type => (
                <TagSelect.Option value={type.value}>{type.text}</TagSelect.Option>
            ))}
        </TagSelect>
    );
}
```

## onChange 事件

```jsx live fff
function App() {
    const TYPE_DATASOURCE = [
        {value: 'cat1', text: '类目一'},
        {value: 'cat2', text: '类目二'},
        {value: 'cat3', text: '类目三'},
        {value: 'cat4', text: '类目四'},
        {value: 'cat5', text: '类目五'},
        {value: 'cat6', text: '类目六'},
        {value: 'cat7', text: '类目七'},
        {value: 'cat8', text: '类目八'},
        {value: 'cat9', text: '类目九'},
        {value: 'cat10', text: '类目十'},
        {value: 'cat11', text: '类目十一'},
        {value: 'cat12', text: '类目十二'},
        {value: 'cat13', text: '类目十三'},
        {value: 'cat14', text: '类目十四'}
    ];

    function handleTagChange(value) {
        console.log(value);
    }

    return (
        <TagSelect onChange={handleTagChange} expandable>
            {TYPE_DATASOURCE.map(type => (
                <TagSelect.Option value={type.value}>{type.text}</TagSelect.Option>
            ))}
        </TagSelect>
    );
}
```

## API

| 参数         | 说明                 | 类型                  | 默认值                   |
| ------------ | -------------------- | --------------------- | ------------------------ |
| mode         | 模式                 | `multiple`〡`single`  | `multiple`               |
| hideCheckAll | 是否隐藏全选按钮     | `boolean`             | `false`                  |
| expandable   | 是否支持展开收起功能 | `boolean`             | `false`                  |
| defaultValue | 默认数据             | `any[]`               | `--`                     |
| value        | 默认数据             | `any[]`               | `--`                     |
| className    | 样式名               | `string`              | `--`                     |
| style        | 内联样式             | `React.CSSProperties` | `--`                     |
| children     | 子节点               | `any`                 | `--`                     |
| onChange     | 数据修改后事件       | `function`            | `(value: any[]) => void` |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/TagSelect>
