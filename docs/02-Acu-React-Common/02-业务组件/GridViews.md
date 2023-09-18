---
title: GridViews
---

用于展示详情页的信息的布局组件，支持分块展示和指定列数展示。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const {GridViews} = components;
```

## 基本用法

```jsx live fff
function App() {
    const contents = [
        {
            key: 'basic',
            title: '基本信息',
            items: [
                {key: 'contractNo', label: '提交编号', content: '2018100800003'},
                {key: 'name', label: '合同名称', content: '合同计收测试'},
                {key: 'type', label: '合同类型', content: '战略/框架合作协议'},
                {key: 'nature', label: '合同性质', content: '非范本合同'}
            ]
        }
    ];

    return (
        <div>
            <div>详情页</div><br />
            <GridViews contents={contents} />
        </div>
    );
}
```

## 分块展示

```jsx live fff
function App() {
    const items = [
        {key: 'contractNo', label: '提交编号', content: '2018100800003'},
        {key: 'name', label: '合同名称', content: '合同计收测试'},
        {key: 'type', label: '合同类型', content: '战略/框架合作协议'},
        {key: 'nature', label: '合同性质', content: '非范本合同'},
        {key: 'contractModelName', label: '范本名称', content: '范本内容'},
        {key: 'status', label: '合同状态', content: '待提交终审正本'}
    ];

    const contents = [
        {key: 'basic', title: '基本信息', items},
        {key: 'advanced', title: '高级信息', items}
    ];

    return (
        <div>
            <div>分块展示详情页</div><br />
            <GridViews contents={contents} />
        </div>
    );
}
```

## 指定列数

```jsx live fff
function App() {
    const items = [
        {key: 'contractNo', label: '提交编号', content: '2018100800003'},
        {key: 'name', label: '合同名称', content: '合同计收测试'},
        {key: 'type', label: '合同类型', content: '战略/框架合作协议'},
        {key: 'nature', label: '合同性质', content: '非范本合同'},
        {key: 'contractModelName', label: '范本名称', content: '范本内容'},
        {key: 'status', label: '合同状态', content: '待提交终审正本'}
    ];

    const contents = [
        {key: 'basic', title: '基本信息', items},
        {key: 'advanced', title: '高级信息', items}
    ];

    return (
        <div>
            <div>指定列数</div><br />
            <GridViews contents={contents} colCount={3} />
        </div>
    );
}
```

## API

| 参数       | 说明         | 类型      | 默认值 |
| ---------- | ------------ | --------- | ------ |
| labelWidth | 标签宽度     | `number`  | `--`   |
| colCount   | 单列个数     | `number`  | `--`   |
| withColon  | 是否显示冒号 | `boolean` | `--`   |
| contents   | 展示项       | `Items[]` | `--`   |

## Items API

| 参数    | 说明       | 类型        | 默认值 |
| ------- | ---------- | ----------- | ------ |
| key     | 展示项key  | `string`    | `--`   |
| label   | 展示项标签 | `string`    | `--`   |
| content | 展示项内容 | `ReactNode` | `--`   |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E4%B8%9A%E5%8A%A1%E7%BB%84%E4%BB%B6/GridViews>
