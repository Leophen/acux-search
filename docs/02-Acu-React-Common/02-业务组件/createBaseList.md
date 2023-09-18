---
title: createBaseList
---

通过配置，结合 redux 用来快速生成一张列表页的高阶组件。

列表页是网站开发中的最常见形式之一，为了提高开发效率，避免大量逻辑类似的代码，将列表通用的行为抽取出来，通过本 HOC 来扩展。

具体做法如下，createBaseList 采取继承的方式创建一个原始 List 的子类，注入列表相关的基础功能，返回增强后的 List。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const createBaseList = components.createBaseList;
```

## 功能说明

- 支持通过配置生成操作区，操作区支持的动作有打开新页、批量发起 ajax 请求、打开弹框等。也可以自定义操作区。
- 支持通过配置生成筛选区，当前支持筛选项有输入框、下拉框和时间选择框。支持实时更新查询数据、同时也支持自定义筛选区。
- 表格区域支持使用默认的 antd table 组件，也支持自定义卡片组件来展现数据。

## demo

<img className="bottom16" src="https://react-app-common.now.baidu-int.com/image/listDemo1.png" width="1200" referrerPolicy="no-referrer" />

<img className="" src="https://react-app-common.now.baidu-int.com/image/listDemo2.png" width="1200" referrerPolicy="no-referrer" />

## 使用方法

```js
import {components} from 'baidu-acu-react-common';

const createBaseList = components.createBaseList;

const options = {}; // 配置项，具体如下配置说明

@createBaseList(options)
class List extends React.Component {
}
export default List;
```

## 配置方法

要生成上图所示的列表页只需要进行一些配置就可以完成，包括基本配置，批量操作区配置、筛选区配置、表格区配置、表格事件配置。

### 基本配置

```js
// 基本配置
{
    className: 'demo-list',  // 样式类名
    title: '通过配置生成的列表', // 标题
    fetchListAction: 'getDemoList', // 如果用redux则填action的方法名，如果不是，则填形如'/api/demo/list'的后端接口地址
    rowKey: 'id', // 表格数据主键
    pageSize: 10, // 默认pageSize
    pageSizeOptions: ['10', '20', '50', '100'], // 分页下拉框中的页数配置
    select: 'multi' | 'single' | 'none', // 注：如果不设置则默认为'multi'
    loadMore: false | true , // 是否采用“加载更多”方式展现数据，默认为false
    interval: 60000, // 每多少毫秒重复请求列表数据
    $onRequest(payload) {
        payload.aaa = 1;
    }, // 发起请求之前
    $onResponse(page) {}, // 成功之后
    $onError(error) {}, // 错误之后
}
```

### 批量操作区域配置

操作区可以支持配置bulkConfig，也可以支持自定义组件bulkComp，下面先说明配置

```js
// 操作区基本配置
{
    id: 'create', // id
    text: '创建', // 按钮文案
    icon: 'reload', // antd icon 可选
    skin: 'primary', // primary dashed danger 不填为默认样式
    disabled: true, // 是否可点击
    actionType: 'link', // 按钮操作类型 link ajax dialog custom drawer
    select: true, // 是否可表格中选择项相关
}

// 以下是4种常见操作类型的额外配置内容
// 2.1 actionType='link'
{
    actionType: 'link',
    link: '/home/demo/form'
}

// 2.2 actionType='ajax'
{
    actionType: 'ajax',
    ajax: {
        apiAction: 'deleteUser', // 如果用redux，填action方法名，如果不是，则填形如'/api/demo/delete'的后端接口地址
        $toastMessage: '删除成功', // 成功后提示
        confirmTitle: '确认删除提示', // confirmTitle
        confirmText: '确定要删除所选择的数据吗?', // confirmText
        $onRequest(requestPayload) {}, // 勾子函数：请求发起之前
        $onResponse(response, requestPayload) {}, 勾子函数：成功返回之后
        $onError(error) {} // 勾子函数：错误获取后
    }
}

// 2.3 actionType='dialog'
{
    actionType: 'dialog',
    dialog: {
        className: 'my-dialog',
        maskClosable: false, // 是否点击空白处关闭弹框
        title: '弹框',
        width: 500,
        foot: false, // 一般不需要配置，只有当不需要foot时，才配置foot=false
        body: {
            type: 'commom', // common-常见于内套form组件 alert-只可接收string、plain-纯展示内容，可接受组件和string
            content: ExampleComponent // 对于alert只接收字符串，其他的可接受组件
        }
   }
}

// 2.4 actionType='drawer'
{
    actionType: 'drawer',
    dialog: {
        className: 'my-drawer',
        maskClosable: false, // 是否点击空白处关闭弹框
        title: '弹框',
        width: 500,
        foot: false, // 一般不需要配置，只有当不需要foot时，才配置foot=false
        body: {
            content: ExampleComponent // 对于alert只接收字符串，其他的可接受组件
            $onBeforeOpen(request) {},
            $extraPayload: {
                a: 1
            }
        }
   }
}

// 2.5 actionType='custom' 自定义动作
{
   actionType: 'custom',
   action: 'stopService' // 自定义方法名，是类里面的方法名！
}
```

除了配置生成操作区，也可以自定义一个操作区组件，具体见下图代码示例：

```js
// 引入方式
{
    bulkPosition: 'left',
    bulkComp: Bulk,
}
```

<img className="" src="https://react-app-common.now.baidu-int.com/image/bulk.png" width="1200" referrerPolicy="no-referrer" />

### 筛选区域配置

筛选区同样可以支持配置 filterConfig，也可以支持自定义组件 filterComp，下面先说明配置，当前 filter 筛选配置只支持 textbox, select,  rangecalendar。注：当前还不支持筛选项间的联动。

```js
filterConfig: {
    position: 'tb', // 筛选位置，如果postion等于'tb'，则和操作区同行，不设置则另起一行
    controls: [
        {
            type: 'textbox', // 类型为输入框
            name: 'name',
            label: 'Name：' // label
        },
        {
            type: 'select', // 下拉框
            name: 'age',
            value: '29', // 初始化的值
            label: '年龄：',
            // multi: true // 是否多选
            options: [
                {value: '', text: '全部'},
                {value: '29', text: '29'},
                {value: '30', text: '30'}
            ]
        },
        {
            type: 'rangecalendar', // 时间段选择框
            name: 'time',
            time: true,
            label: '时间：',
            value: {
                begin: moment().subtract(1, 'months').utc().format('YYYY-MM-DDTHH:mm:ss') + 'Z',
                end: moment().utc().format('YYYY-MM-DDTHH:mm:ss') + 'Z'
            },
            range: {
                begin: new Date(2018, 7, 2),
                end: new Date()
            }
        }
    ],
    submitText: '查询' // 查询按钮text, 如果不设置则实时改变就发起查询。
}

// 有一种场景需要请求后端数据来更新下拉框的options选项，只需要更新state的filterConfig内容
const filterConfigControls = this.state.filterConfig.controls;

itemIndex = filterConfigControls.findIndex(item => item.name === 'age');
if (itemIndex > -1) {
    const newOptions = [
        {value: '29', text: '29'},
        {value: '31', text: '31'}
    ];
    this.setState({
        filterConfig: Object.assign({}, this.state.filterConfig, {
            controls: [
                ...filterConfigControls.slice(0, itemIndex),
                Object.assign({}, filterConfigControls[itemIndex], {options: newOptions}),
                ...filterConfigControls.slice(itemIndex + 1)
            ]
        })
    });
}
```

同样的，开发者也可以自定义筛选区组件来完成筛选操作：

```js
// 引入方式
filterConfig: {
    position: 'tb' // 筛选位置，如果postion等于'tb'，则和操作区同行，不设置则另起一行
},
filtetComp: Filter // 自定义组件Filter
```

一个简单的筛选组件如下图所示，通过调用 props.handleFilter 方法发起查询。

<img className="" src="https://react-app-common.now.baidu-int.com/image/Filter.png" width="1200" referrerPolicy="no-referrer" />

表格区域一般配置和 antd table 配置一致，如不清楚参考 [antdTable](https://ant.design/components/table-cn/)，
这里主要说明下操作列的配置，操作动作配置是 commands, 和上面 bulk 配置选项基本一致，具体如下：

其中 handleTableCommand 是组件已经封装操作方法，用户不需要自定义，只需要配置 commands，如果操作比较复杂，则可以自定义方法，例如 viewDetail 方法，
此时在List组件中实现即可。

```js
tableConfig() { // 注意：这里一定是方法
    return {
        columns: [
            {
                title: 'Name',
                dataIndex: 'name'
            },
            {
                title: '操作',
                render: record => {
                    return (
                        <span>
                            <a onClick={() => this.handleTableCommand('VIEW', record)} className="action">去新页面</a>
                            <a onClick={() => this.handleTableCommand('DELETE', record)} className="action">删除</a>
                            <a onClick={() => this.handleTableCommand('UPDATE', record)} className="action">编辑</a>
                            <a onClick={() => this.viewDetail(record)} className="action">自定义详情</a>
                        </span>
                    );
                }
            }
        ]
    };
},
commands: {
    VIEW: {
        actionType: 'link',
        link: '/home/demo/form',
        $payloadFields: ['id']
    },
    DELETE: {
        actionType: 'ajax',
        ajax: {
            apiAction: 'deleteUser',
            $toastMessage: '删除成功',
            confirmTitle: '确认删除提示',
            confirmText: '确定要删除所选择的数据吗?',
            // $onRequest(requestPayload) {},
            // $onError(error) {},
            $payloadFields: ['id'],
            $extraPayload: {
                a: 1
            }
        }
    },
    UPDATE: {
        actionType: 'dialog',
        dialog: {
            title: '依赖模块',
            width: 700,
            body: {
                type: 'common',
                content: DemoForm
            }
        }
    }
}
```

表格区域也可以自定义，比如需要的是卡片式表格样式，只需要定一个card组件就可以，具体可见[demo](http://106.12.154.36/project/list/card)和[源码](http://icode.baidu.com/repos/baidu/acu-ai-fe/react-app-starter/blob/master:src/modules/demo/Cards.js)

对于更加特殊的类型自定义tableComp组件来实现

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E4%B8%9A%E5%8A%A1%E7%BB%84%E4%BB%B6/CreateBaseList>
