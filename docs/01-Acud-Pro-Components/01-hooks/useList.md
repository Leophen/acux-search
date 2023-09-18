---
title: useList
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

用于配置化+自定义实现各种列表页面的 hooks。

:::note 说明

列表页是开发中遇到最常见的页面，如下图所示，一张典型的列表页会包括“列表主区域”、“操作区”和“筛选区”。

为了提高开发效率，避免大量重复的基础代码(比如请求数据，打开弹框等)，将列表通用的行为都抽取出来，用户只需要通过简单的配置就能实现大多数场景的列表页面，一些特殊的场景可以通过自定义组件和方法来实现。

<img src="https://acud-pro.now.baidu-int.com/image/useListFeatures.png" referrerPolicy="no-referrer" />

:::

- 列表主区域支持表格，卡片风格及其他自定义形式的列表。
- 操作区和表格区支持常用的 5 种操作方式：
  - 页面跳转
  - 弹框
  - 抽屉
  - Ajax 请求
  - 自定义方法
- 操作区支持配置及自定义，能与主区域选中的数据进行交互。自定义操作组件可以调用底层的 `handleAction` 方法迅速实现 5 种常用操作。
- 筛选区支持配置及自定义，筛选区的数据可从后端接口中获取，随时可改，支持联动。
- 支持在业务端 自己定义方法，或实现自己的逻辑。

:::note 与 [useTable](./useTable) 的区别

- **更灵活的配置项**：[useTable](./useTable) 比 useList 支持更多基础组件参数的传入
- **更统一的配置项**：[useTable](./useTable) 统一了 command 部分不同 actionType 下参数配置结构
- **更精简的代码**：[useTable](./useTable) 精简了代码文件结构（useList 由于 createBaseList 的原因，文件引用复杂）

:::

## 引入

```js
import {useList, HooksList} from '@baidu/acud-pro-components';
```

### 使用方法

```tsx
import {useList, HooksList} from '@baidu/acud-pro-components';

// 配置信息
const options = (props, handleTableCommand, customFunctions) => ({
    // ...
});

export default props => {
    // 自定义方法
    const customOpt = () => {
        // ...
    };

    // 自定义方法集合
    const customFunctions = {customOpt};
    const [bizData, setBizData] = useState({});
    const {listProps} = useList(options, {...props, ...bizData}, customFunctions);

    return <HooksList {...listProps} />;
};
```

1、 首先定义配置项信息 options，它必须是一个方法，有三个参数 prop、handleTableCommand 和 customFunctions，分别代表组件属性，表格事件处理函数，和业务代码中自定义的方法集合。更多详细的配置项下面详细介绍。

2、 核心：在组件中使用 useList 这个 hooks，它的三个参数是 options、props 和 customFunctions，返回一个对象如下说明：

- dataSource: 当前列表中展现的数据集合
- options: 当前所有配置项
- setOptions: 更新配置项的方法
- setSelectedRowKeys: 设置选中的方法
- handleAction: 5 种常见操作方法
- listProps: 列表渲染的所有属性

3、 最后返回 HooksList 组件

## 配置项

### 基础配置

| 配置项           | 说明                                           | 类型                      | 默认值                      |
| ---------------- | ---------------------------------------------- | ------------------------- | --------------------------- |
| *fetchListAction | 请求方法，可以是 actions 方法名或接口          | `string`                  | `--`                        |
| *rowKey          | 返回数据的主键字段名                           | `string`                  | `--`                        |
| title            | 页面标题                                       | `string`〡`ReactNode`     | `--`                        |
| className        | 列表 className                                 | `string`                  | `--`                        |
| pageSize         | 每页条数                                       | `number`                  | `10`                        |
| pageSizeOptions  | 指定每页可以显示多少条                         | `string[]`                | `['10', '20', '50', '100']` |
| select           | 选择类型                                       | `multi`〡`single`〡`none` | `multi`                     |
| interval         | 轮询间隔（ms）                                 | `number`                  | `--`                        |
| emptyText        | 无返回数据时的文案提示                         | `string`                  | `--`                        |
| bulkPosition     | 操作区位置                                     | `left`〡`right`           | `left`                      |
| bulkConfig       | 操作区配置，详见“操作区配置”                   | `BulkItem[]`              | `--`                        |
| bulkComp         | 自定义操作区组件，优先级优于 bulkConfig        | `ReactNode`               | `--`                        |
| bulkConfig       | 筛选区配置，详见“筛选区配置”                   | `FilterConfig`            | `--`                        |
| filterComp       | 自定义筛选区组件，优先级优于 filterConfig      | `ReactNode`               | `--`                        |
| tableConfig      | 列表主区域配置，详见“列表主区域配置”           | `object`                  | `--`                        |
| tableComp        | 自定义列表主区域区组件，优先级优于 tableConfig | `ReactNode`               | `--`                        |
| card             | 卡片组件，当展现形式为卡片列表时配置           | `ReactNode`               | `--`                        |
| commands         | 事件实现配置，详见“事件实现配置”               | `object`                  | `--`                        |
| requestAbort     | 是否中断请求发起                               | `boolean`                 | `false`                     |
| $onRequest       | 列表请求发出前钩子函数                         | `(payload: any) => any`   | `--`                        |
| $onResponse      | 列表请求返回成功后钩子函数                     | `(page: any) => any`      | `--`                        |
| $onError         | 列表请求失败时钩子函数                         | `(error: any) => void`    | `--`                        |

### 列表主区域配置 (tableConfig)

如果配置了 tableConfig，则会使用 [acud table](../../03-Acud/05-数据展示/Table)展示表格，所以配置项可以使用 Acud table 的配置项，组件会进行透传，下面就几个常用的配置项做说明。

| 配置项            | 说明                 | 类型                                                    | 默认值 |
| ----------------- | -------------------- | ------------------------------------------------------- | ------ |
| *columns          | 表格列的配置描述     | [ColumnProps[]](../../03-Acud/05-数据展示/Table#column) | `--`   |
| *getCheckboxProps | 选择框的默认属性配置 | `Function(record)`                                      | `--`   |

### columns 操作区指南

先看一个例子代码

```tsx
const options = (props, handleTableCommand, customFunctions) => ({
    tableConfig: {
        columns: [
            ...(props.match.params.withName ? [{
                    title: '名称',
                    dataIndex: 'name'
            }] : []),
            {
                title: '操作',
                key: 'action',
                render: item => (
                    <span>
                        <a onClick={() => handleTableCommand('VIEW_DETAIL', item)}>新页查看详情</a>
                        <a onClick={() => handleTableCommand('VIEW_DIALOG_DETAIL', item)}>弹框查看详情</a>
                        <a onClick={() => handleTableCommand('DELETE', item)}>删除</a>
                        <a onClick={() => handleTableCommand('UPDATE', item)}>编辑</a>
                        <a onClick={() => customFunctions.customOpt(item)}>自定义方法</a>
                    </span>
                )
            }
        ]
    },
    commands: {
        VIEW_DETAIL: {
            actionType: 'link',
            link: '/home/detail/basicdetail',
            $payloadFields: ['id']
        },
        VIEW_DIALOG_DETAIL: {
            actionType: 'dialog',
            dialog: {
                title: 'Demo详情',
                width: 700,
                body: {
                    type: 'plain',
                    content: DialogDetail
                }
            }
        },
        DELETE: {
            actionType: 'ajax',
            ajax: {
                apiAction: 'deleteDemo',
                $toastMessage: '删除成功',
                confirmTitle: '确认删除提示',
                confirmText: '确定要删除所选择的数据吗?',
                confirmType: 'error',
                $payloadFields: ['id'],
                $extraPayload: {
                    a: 1
                }
            }
        },
        UPDATE: {
            actionType: 'dialog',
            dialog: {
                title: '编辑Demo',
                width: 700,
                body: {
                    type: 'common',
                    content: DialogForm
                }
            }
        }
    }
});
```

上面代码块有两个小技巧

- columns 有些列可以根据 url 参数或者 props 中某个属性而显示隐藏。比如上面 name 列就由 url 中 withName 参数来控制展现与否。
- 表格中的操作有两种方式：

1. 通过配置
2. 自定义方法，自定义方法需要在业务代码中自己实现，并放到 customFunctions 集合中，通过配置 commands 字段就可以快速实现 5 种常见的操作，key 对应 handleTableCommand 方法的第一个参数，value 对象配置项详见下面【事件配置】

### 事件配置

| 配置项      | 说明                                           | 类型                                     | 默认值 |
| ----------- | ---------------------------------------------- | ---------------------------------------- | ------ |
| *actionType | 操作类型                                       | `link`/`ajax`/`dialog`/`drawer`/`custom` | `--`   |
| link        | 当 actionType 为 `link` 时<br/>要跳转的链接    | `string`                                 | `--`   |
| action      | 当 actionType 为 `custom` 时<br/>自定义方法名  | `string`                                 | `--`   |
| ajax        | 当 actionType 为 `ajax` 时<br/>Ajax 配置项     | `AjaxOption`                             | `--`   |
| dialog      | 当 actionType 为 `dialog` 时<br/>dialog 配置项 | `DialogOption`                           | `--`   |
| drawer      | 当 actionType 为 `drawer` 时<br/>drawer 配置项 | `DrawerOption`                           | `--`   |

三种配置项 AjaxOption、DialogOption 和 DrawerOption 分别用 TS 类型定义来说明如下：

```mdx-code-block
<Tabs>
<TabItem value="AjaxOption">
```

```ts
export type ConfirmType = 'warning' | 'info' | 'error' | 'sucess';

export interface AjaxOption {
    apiAction: string; // actions方法名
    $toastMessage?: string; // 成功之后提示
    confirmTitle?: string; // 确认提示title
    cancelText?: string;
    okText?: string;
    confirmText?: string; // 确认提示文案
    confirmType?: ConfirmType | 'error'; // 确认按钮的类别
    $payloadFields?: string[]; // 需要传给后端的表格字段
    $extraPayload?: any; // 额外的请求参数
    $onRequest?: (requestPayload: any) => any; // 发起ajax请求前的勾子函数
    $onResponse?: (response: any, requestPayload: any) => any; // ajax请求成功后的勾子函数
    $onError?: (error: any, requestPayload: any) => void; // ajax请求失败时的勾子函数
}
```

```mdx-code-block
</TabItem>
<TabItem value="DialogOption">
```

```ts
export interface DialogOptionBody {
    type: 'alert' | 'plain' | 'common'; // 弹框类型
    content: any; // 弹框中的内容，可以是string、可以是组件
    $payloadFields?: any; // 需要传给弹框的数据字段
    $extraPayload?: any; // 额外参数
    $onBeforeDialogOpen?: (payload: any) => any; // 弹框打开之前的钩子函数
}
export interface DialogOption {
    body: DialogOptionBody; // 弹框主体区域配置，见DialogOptionBody
    className?: string; // 弹框 className
    title?: string; // 弹框标题
    width?: number; // 弹框宽度
    maskClosable?: boolean; // 点击蒙层是否允许关闭
    foot?: boolean; // 是否需要底部
    okText?: string; // 确认按钮文字
    cancelText?: string; // 取消按钮文字
    cancelWithSuccess?: boolean; // 取消时是否刷新列表
    mask?: boolean // 是否显示遮罩
}
```

```mdx-code-block
</TabItem>
<TabItem value="DrawerOption">
```

```ts
export interface DrawerOptionBody {
    content: any; // 内容，可以是string、可以是组件
    $payloadFields?: any; // 需要传给弹框的数据字段
    $extraPayload?: any; // 额外参数
    $onBeforeOpen?: (payload: any) => any; // 抽屉打开之前的钩子函数
}
export interface DrawerOption {
    body: DrawerOptionBody; // 抽屉主体区域配置，见DrawerOptionBody
    className?: string; // 抽屉 className
    title?: string; // 抽屉标题
    width?: number; // 抽屉宽度
    maskClosable?: boolean; // 点击蒙层是否允许关闭
    foot?: boolean; // 是否需要底部
    okText?: string; // 确认按钮文字
    cancelText?: string; // 取消按钮文字
    cancelWithSuccess?: boolean; // 取消时是否刷新列表
    mask?: boolean; // 是否显示遮罩
}
```

```mdx-code-block
</TabItem>
</Tabs>
```

### 操作区配置 (bulkConfig)

bulkConfig: BulkItem[];  BulkItem 配置项如下表所示：

| 配置项      | 说明                                                       | 类型                                         | 默认值   |
| ----------- | ---------------------------------------------------------- | -------------------------------------------- | -------- |
| *id         | 按钮 ID                                                    | `string`                                     | `--`     |
| *text       | 按钮文案                                                   | `string`                                     | `--`     |
| position    | 按钮位置                                                   | `left`〡`right`                              | `left`   |
| type        | 类型                                                       | `button`〡`checkbox`                         | `button` |
| icon        | 按钮 icon                                                  | `string`                                     | `--`     |
| skin        | 按钮皮肤，不填为默认样式                                   | `primary`〡`dashed`〡`danger`                | `--`     |
| select      | 是否和选择关联，如果关联，当没有选择数据的时候，按钮不可点 | `boolean`                                    | `false`  |
| disabled    | 是否禁用                                                   | `boolean`                                    | `false`  |
| *actionType | 操作类型                                                   | `link`〡`ajax`〡`dialog`〡`drawer`〡`custom` | `--`     |
| link        | 当 actionType 为 `link` 时，要跳转的链接                   | `string`                                     | `--`     |
| action      | 当 actionType 为 `custom` 时，自定义方法名                 | `string`                                     | `--`     |
| ajax        | 当 actionType 为 `ajax` 时，Ajax 配置项                    | `AjaxOption`                                 | `--`     |
| dialog      | 当 actionType 为 `dialog` 时，dialog 配置项                | `DialogOption`                               | `--`     |
| drawer      | 当 actionType 为 `drawer` 时，drawer 配置项                | `DrawerOption`                               | `--`     |

上表中 AjaxOption、DialogOption 和 DrawerOption 见上面【事件配置】章节。

### 筛选区配置 (filterConfig)

| 配置项     | 说明                                                                               | 类型              | 默认值 |
| ---------- | ---------------------------------------------------------------------------------- | ----------------- | ------ |
| *controls  | 筛选配置项                                                                         | `FilterControl[]` | `--`   |
| position   | 筛选区位置，`left` 与操作区一行居左 `right` 与操作区一行居右，不设置则在操作区下面 | `string`          | `--`   |
| submitText | 查询按钮文案，如果不设置则实时改变就发起查询                                       | `string`          | `--`   |

FilterControl:

| 配置项       | 说明                                            | 类型                                                                 | 默认值  |
| ------------ | ----------------------------------------------- | -------------------------------------------------------------------- | ------- |
| *type        | 筛选类型                                        | `textbox`〡`search`〡`select`〡`rangecalendar`〡`tagselect`〡`radio` | `--`    |
| *name        | 筛选项名称                                      | `string`                                                             | `--`    |
| width        | 筛选项宽度                                      | `number`                                                             | `--`    |
| defaultValue | 默认值                                          | `any`                                                                | `--`    |
| value        | 数值                                            | `any`                                                                | `--`    |
| label        | 标签                                            | `string`                                                             | `--`    |
| multi        | 是否多选，应用 type 为 'select' 情况            | `boolean`                                                            | `false` |
| options      | 选项，select、tagselect 和 radio 类型时需要配置 | `any[]`                                                              | `--`    |
| time         | type === 'rangecalendar' 时是否是时间           | `boolean`                                                            | `true`  |
| range        | type === 'rangecalendar' 时日期选择框的范围     | `any`                                                                | `--`    |
| acudProps    | 其他 acud 支持的属性                            | `any`                                                                | `--`    |

### 其他使用技巧

1、页面中渲染切换

我们业务中有很多这种场景，比如某个按钮置灰与否、列展示、请求地址都会根据 props 中某个值变化而切换。

实现方式：通过修改 options 方法第一个参数 props 来实现所有类似这些变化。

```tsx
export default props => {
    const customFunctions = {};

    // 业务端维护用来修改渲染的数据，通过setBizData来用数据出发渲染的改变
    const [bizData, setBizData] = useState({});
    const {listProps} = useList(options, {...props, ...bizData}, customFunctions);

    // 更新原始配置的方法
    const updateFilterControl = () => {
        setBizData({
            ...bizData,
            type2Options: [
                {value: 'cat1', text: '类目1'},
                {value: 'cat2', text: '类目2'}
            ]
        });
    };

    useEffect(() => {
        // 更新一个筛选项方法
        updateFilterControl();
    }, []);

    return (
        <HooksList
            {...listProps}
        />
    );
};
```

2、卡片形式列表的全选功能

功能示例: [demo](http://106.12.154.36/hooks/list/cardlist)。

实现方式：只需要在 bulkConfig 中新增一个 checkbox 配置项，如下面代码所示

```typescript static
bulkConfig: [
    {
        id: 'checkAll',
        type: 'checkbox',
        text: '全选',
        actionType: 'custom',
        action: 'checkAll' // 底层useList中已实现，业务代码中不需要写
    },
    ...
]
```

3、业务中自定义的渲染

需求场景：有些列表页 title 上面需要放一些提示，或者表格上面放一些统计信息等，这种情况就需要业务代码进行一些渲染。HooksList 有一个 customRender 属性，当前有 title 和 toolbar 两个位置的渲染输入，具体可见下面代码。

```tsx
export default props => {
 
    // 业务端支持自定义做一些页面渲染
    const customRender = {
        title: <div>业务端title</div>,
        toolbar: <div>业务端toolbar</div>
    };
    return (
        <HooksList
            {...listProps}
            customRender={customRender}
        />
    );
};
```
