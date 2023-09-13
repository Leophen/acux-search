---
title: useTable
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

基于 Table 进行扩展的渲染业务列表 hooks，包括以下功能：

- **列表数据请求相关：**
  - 首次请求
  - 定时/手动刷新请求
  - 翻页请求
  - 搜索请求
  - 排序请求
  - 过滤请求
- **列表操作相关：**
  - 新建按钮
  - 批量操作按钮
  - 表格单项操作

## 引入

```js
import {request, useTable, HooksTable} from '@baidu/acud-pro-components';
```

## test

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = props => {
        const {bulkComp, filterComp} = props;
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            bulkComp,
            filterComp,
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '角色名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '角色描述',
                        dataIndex: 'creator'
                    },
                    {
                        key: 'user',
                        title: '已授权用户数',
                        dataIndex: 'user'
                    },
                    {
                        key: 'handle',
                        title: '操作',
                        dataIndex: 'handle'
                    }
                ]
            }
        };
    };

    const bulkComp = () => (
        <div className="acud-hooks-table-toolbar-filter">
            <Search
                placeholder="请输入项目名称"
                onSearch={nameFilter => console.log(nameFilter, 'search')}
            />
            <Button onClick={() => console.log('create')}>
                角色管理
            </Button>
        </div>
    );

    const filterComp = () => (
        <div className="acud-hooks-table-toolbar-filter">
            <Button
                icon={<OutlinedRefresh />}
                onClick={() => console.log('refresh')}
            />
        </div>
    );

    const List = props => {
        const listProps = useTable(options, {...props, bulkComp, filterComp});
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 基本用法

```mdx-code-block
<Tabs>
<TabItem value="useTable 的参数">
```

1. `options`：可以接收三个参数的方法，用于动态配置组件所需配置项；
2. `props`：options 方法中需要用到的一些参数；
3. `customFunctions`：options 方法中需要用到的一些方法。

```mdx-code-block
</TabItem>
<TabItem value="useTable 的返回值">
```

`useTable` 返回以下数据结构，传入 `HooksTable`，即可渲染列表：

```js
{
    /**
     * 类名
     */
    className,
    /**
     * 标题
     */
    title,
    /**
     * 表格上方区域相关配置
     */
    toolbarProps,
    /**
     * 表格区域相关配置
     */
    tableProps: {
        /**
         * 行标识符
         */
        rowKey,
        /**
         * 加载状态
         */
        loading,
        /**
         * 表格数据
         */
        dataSource,
        /**
         * 表格行选择配置
         */
        rowSelection,
        /**
         * 表格分页配置
         */
        pagination,
        /**
         * 表格分页、过滤、排序等操作触发的 change
         */
        onChange
    },
    /**
     * 对话框/抽屉相关配置
     */
    dialogProps,
    /**
     * 表格中的一些方法
     * 包括内置方法（loadList、loadFirstPage、setListParams、handleFilterChange）+ useTable 调用时传入的 customFunctions
     */
    tableActions,
    /**
     * 筛选数据
     * 通过 handleFilterChange 方法调用后进行保存的筛选数据，
     * 初始化值依靠 filterConfig 中配置的 name、defaultValue、defaultChecked 进行提取
     */
    filterData,
    /**
     * 请求数据，但是是 $onRequest 处理之前的
     */
    listParams,
    /**
     * http 状态码，若为 403、404、500，可以展示表格对应的空状态
     */
    httpStatusCode,
    /**
     * 更新请求数据，触发请求更新
     */
    setListParams,
    /**
     * 传入 command 配置内容，触发对应操作
     */
    handleCommand,
    /**
     * 传入 options 中配置的 commands 操作名，触发对应操作
     */
    handleTableCommand,
    /**
     * 传入筛选数据项，触发请求更新
     */
    handleFilterChange
}
```

```mdx-code-block
</TabItem>
<TabItem value="option 的参数">
```

1. `props`：useTable 调用时传入的 props；
2. `handleTableCommand`：用于调用 options 的 command 操作；
3. `customFunctions`：内置方法（loadList、loadFirstPage、setListParams、handleFilterChange）+ useTable 调用时传入的  customFunctions。

```mdx-code-block
</TabItem>
</Tabs>
```

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = () => {
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '创建人',
                        dataIndex: 'creator'
                    }
                ]
            }
        };
    };

    const List = props => {
        const listProps = useTable(options, props);
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 不可选择

配置 `options > select` 为 `none` 可以关闭表格的默认可选状态。

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = () => {
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            select: 'none',
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '创建人',
                        dataIndex: 'creator'
                    }
                ]
            }
        };
    };

    const List = props => {
        const listProps = useTable(options, props);
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 表格操作

配置 `options > tableConfig > columns > render` 自定义表格操作。

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = (props, handleTableCommand) => {
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            select: 'none',
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '创建人',
                        dataIndex: 'creator'
                    },
                    {
                        title: '操作',
                        key: 'action',
                        width: 210,
                        render: payload => (
                            <>
                                <a className="table-action" onClick={() => handleTableCommand('LINK', payload)}>详情</a>
                                <a className="table-action" onClick={() => handleTableCommand('DIALOG', payload)}>编辑</a>
                                <a className="table-action" onClick={() => handleTableCommand('DIALOG', payload)}>对话框</a>
                                <a className="table-action" onClick={() => handleTableCommand('DRAWER', payload)}>抽屉</a>
                                <a className="table-action" disabled>删除</a>
                            </>
                        )
                    }
                ]
            }
        };
    };

    const List = props => {
        const listProps = useTable(options, props);
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 排序和筛选

- 配置 `options > tableConfig > columns > sorter` 可以对表格进行排序；
- 配置 `options > tableConfig > columns > filters` 可以对表格进行筛选，`filters` 是一个数组，包含要筛选的信息。

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = () => {
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '创建人',
                        dataIndex: 'creator'
                    },
                    {
                        key: 'createTime',
                        title: '创建时间',
                        dataIndex: 'createTime',
                        sorter: true,
                        render: createTime => {
                            return timeUtil.toTime(createTime, '-');
                        }
                    },
                    {
                        key: 'departmentIDs',
                        title: '部门',
                        dataIndex: 'departmentName',
                        filters: [
                            {text: '部门1', value: 'department1'},
                            {text: '部门2', value: 'department2'}
                        ]
                    },
                ]
            }
        };
    };

    const List = props => {
        const listProps = useTable(options, props);
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 配置操作区

配置 `options > bulkConfig` 属性来开启操作区，具体可配置项见 [API - IBulkItemConfig](./useTable#ibulkitemconfig)

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = () => {
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            bulkConfig: [
                {
                    id: 'createProject',
                    skin: 'primary',
                    icon: <OutlinedPlus />,
                    text: '创建项目',
                    actionType: 'link',
                    link: '/project/create'
                }
            ],
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '创建人',
                        dataIndex: 'creator'
                    }
                ]
            }
        };
    };

    const List = props => {
        const listProps = useTable(options, props);
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 自定义操作区

配置 `options > bulkComp` 属性来自定义操作区，优先级高于上面的 `bulkConfig`。

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = props => {
        const {bulkComp} = props;
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            bulkComp,
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '创建人',
                        dataIndex: 'creator'
                    }
                ]
            }
        };
    };

    const bulkComp = () => (
        <Button
            type="primary"
            icon={<OutlinedPlus />}
            onClick={() => console.log('create')}
        >
            创建项目
        </Button>
    );

    const List = props => {
        const listProps = useTable(options, {...props, bulkComp});
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 配置筛选区

配置 `options > filterConfig` 属性来开启筛选区，具体可配置项见 [API - IFilterConfig](./useTable#ifilterconfig)

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = (props, handleTableCommand, customFunctions) => {
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            filterConfig: {
                controls: [
                    {
                        name: 'keyword',
                        control: Search,
                        controlProps: {
                            allowClear: true,
                            placeholder: '请输入项目名称搜索',
                            onSearch: keyword => customFunction.handleFilterChange({keyword})
                        }
                    },
                    {
                        id: 'refresh',
                        icon: <OutlinedRefresh />,
                        actionType: 'custom',
                        action: 'loadList',
                        position: 'right'
                    }
                ]
            },
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '创建人',
                        dataIndex: 'creator'
                    }
                ]
            }
        };
    };

    const customFunction = {
        handleFilterChange: key => console.log(key, 'search')
    };

    const List = () => {
        const listProps = useTable(options, {}, customFunction);
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 自定义筛选区

配置 `options > filterComp` 属性来自定义筛选区，优先级高于上面的 `filterConfig`。

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const options = props => {
        const {filterComp} = props;
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            filterComp,
            tableConfig: {
                columns: [
                    {
                        key: 'name',
                        title: '名称',
                        dataIndex: 'name'
                    },
                    {
                        key: 'creator',
                        title: '创建人',
                        dataIndex: 'creator'
                    }
                ]
            }
        };
    };

    const filterComp = () => (
        <div className="acud-hooks-table-toolbar-filter">
            <Search
                placeholder="请输入项目名称"
                onSearch={nameFilter => console.log(nameFilter, 'search')}
            />
            <Button
                icon={<OutlinedRefresh />}
                onClick={() => console.log('refresh')}
            />
        </div>
    );

    const List = props => {
        const listProps = useTable(options, {...props, filterComp});
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## 卡片式列表

配置 `options > card` 属性来展示卡片式列表。

```jsx live fff
function App(props) {
    const listUrl = 'https://yapi.baidu-int.com/mock/23714/api/list';
    const fetchListAction = params => {
        return request.post(listUrl, params);
    };

    const CardContent = props => {
        const {item} = props;
        return (
            <Card
                title={`项目名称：${item.name}`}
                style={{width: 300, margin: '0 20px 20px 0'}}
            >
                创建者：{item.creator}
            </Card>
        );
    };

    const options = () => {
        return {
            rowKey: 'id',
            title: '项目列表',
            fetchListAction,
            card: CardContent
        };
    };

    const List = props => {
        const listProps = useTable(options, props);
        return <HooksTable {...listProps} />;
    };

    return <List />;
}
```

## API

### ITableOptions

Options 配置项：

| 配置项          | 说明                                     | 类型                                            | 默认值                      |
| --------------- | ---------------------------------------- | ----------------------------------------------- | --------------------------- |
| title           | 页面标题                                 | `ReactNode`                                     | `--`                        |
| className       | 列表类名                                 | `string`                                        | `--`                        |
| fetchListAction | 请求的 action 名称或方法                 | `string〡Function`                              | `--`                        |
| abort           | 是否禁止发这次请求                       | `boolean`                                       | `--`                        |
| interval        | 轮询间隔（ms）                           | `number`                                        | `--`                        |
| $onRequest      | 请求发出前钩子函数                       | `(payload: any) => any`                         | `--`                        |
| $onResponse     | 请求返回成功后钩子函数                   | `(response: any, payload?: any) => any`         | `--`                        |
| $onError        | 请求失败时钩子函数                       | `(error: any) => void`                          | `--`                        |
| bulkConfig      | 操作区配置                               | [IBulkItemConfig](./useTable#ibulkitemconfig)[] | `--`                        |
| bulkComp        | 自定义操作区组件                         | `React.ComponentType<any>`                      | `--`                        |
| filterConfig    | 筛选区配置                               | [IFilterConfig](./useTable#ifilterconfig)       | `--`                        |
| filterComp      | 自定义筛选区组件                         | `React.ComponentType<any>`                      | `--`                        |
| rowKey          | 表格行 key 的取值                        | `string`                                        | `--`                        |
| select          | 表格行是否可选择及可选类型（多选、单选） | `multi`〡`single`〡`none`                       | `--`                        |
| pageSize        | 每页默认展示条数                         | `number`                                        | 10                          |
| pageSizeOptions | 每页展示条数的可选值                     | `string[]`                                      | `['10', '20', '50', '100']` |
| tableConfig     | 表格区域配置，同 acud Table              | `Table`                                         | `--`                        |
| tableComp       | 自定义表格区域组件                       | `React.ComponentType<any>`                      | `--`                        |
| card            | 表格区域以卡片组件的形式展示             | `React.ComponentType<any>`                      | `--`                        |
| commands        | 操作相关配置                             | `ICommand`                                      | `--`                        |

### IBulkItemConfig

操作区配置项：

| 配置项        | 说明                                                                       | 类型                                                           | 默认值    |
| ------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------- | --------- |
| id            | 按钮 ID                                                                    | `string`                                                       | `--`      |
| text          | 按钮文本                                                                   | `ReactNode`                                                    | `--`      |
| skin          | 按钮主题                                                                   | `primary`〡`text`〡`highlight`〡`enhance`〡`default`〡`danger` | `--`      |
| block         | 按钮宽度是否为父级宽度                                                     | `boolean`                                                      | `false`   |
| disabled      | 按钮失效状态                                                               | `boolean`                                                      | `false`   |
| href          | 按钮点击跳转地址                                                           | `string`                                                       | `--`      |
| htmlType      | 按钮原生类型                                                               | `string`                                                       | `button`  |
| icon          | 按钮图标组件                                                               | `ReactNode`                                                    | `--`      |
| loading       | 按钮载入状态                                                               | `boolean`〡`{ delay: number }`                                 | `false`   |
| size          | 按钮大小                                                                   | `large〡middle〡small`                                         | `middle`  |
| target        | 按钮 target 属性                                                           | `string`                                                       | `--`      |
| type          | 按钮类型                                                                   | `primary`〡`text`〡`highlight`〡`enhance`〡`default`           | `default` |
| select        | 未选中时是否可操作                                                         | `boolean`                                                      | `true`    |
| actionType    | 操作类型                                                                   | `link`〡`ajax`〡`dialog`〡`drawer`〡`custom`                   | `--`      |
| link          | actionType 为 link 时的链接配置                                            | `string`                                                       | `--`      |
| ajax          | actionType 为 ajax 时的 ajax 配置                                          | [IAjaxOption](./useTable#iajaxoption)                          | `--`      |
| dialog        | actionType 为 dialog 时的 dialog 配置                                      | [IDialogOption](./useTable#idialogoption)                      | `--`      |
| drawer        | actionType 为 dialog 时的 drawer 配置                                      | [IDrawerOption](./useTable#idraweroption)                      | `--`      |
| action        | actionType 为 custom 的用户自定义方法名                                    | `string`                                                       | `--`      |
| $extraPayload | payload 项，select 为 true 时将被覆盖为 `{selectedItems, selectedRowKeys}` | `object`                                                       | `--`      |

### IAjaxOption

### IDialogOption

### IDrawerOption

### IFilterConfig

筛选区配置项：

| 配置项   | 说明       | 类型                                          | 默认值 |
| -------- | ---------- | --------------------------------------------- | ------ |
| controls | 筛选项配置 | [IFilterControl](./useTable#ifiltercontrol)[] | `--`   |

### IFilterControl

```ts
export interface IFilterControl extends IBulkItemConfig {
    /**
     * 筛选项名称
     */
    name?: string;
    /**
     * 筛选控件前的标签名
     */
    label?: React.ReactNode;
    /**
     * 筛选控件
     */
    control?: React.ComponentType<any>;
    /**
     * 筛选控件的参数
     * 如控件有默认值（defaultValue、defaultChecked）
     * 则需要通过这种方式传入，不然会影响 filterData 的初始化
     */
    controlProps?: any;
}
```