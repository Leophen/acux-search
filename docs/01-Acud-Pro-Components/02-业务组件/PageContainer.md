---
title: PageContainer
---

页面容器组件。

## 引入

```js
import {PageContainer} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
>
    内容
</PageContainer>
```

## 副标题

通过 `custom` 属性添加副标题。

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
    custom={<span>这是自定义内容</span>}
>
    内容
</PageContainer>
```

## 页面描述

通过 `description` 属性添加页面描述。

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
    description="页面描述"
>
    内容
</PageContainer>
```

## 返回文本

通过 `backText` 属性自定义返回文本。

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
    backText="后退"
>
    内容
</PageContainer>
```

## 扩展信息

通过 `extra` 属性添加扩展信息。

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
    extra={<span>扩展信息</span>}
>
    内容
</PageContainer>
```

## 按钮配置

通过 `extra` 属性添加扩展信息。

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
    btnConfig={[
        {
            id: 'base-custom-btn-id',
            text: '按钮1',
            btnAction: () => console.log('click btn1')
        },
        {
            text: '按钮2',
            disabled: true,
            tooltip: {
                title: '提示信息'
            },
            btnAction: () => console.log('click btn2')
        }
    ]}
>
    内容
</PageContainer>
```

## 卡片模式

通过 `mode` 属性设为 `card` 切换成卡片模式。

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
    mode="card"
>
    <Card style={{marginBottom: '20px'}}>内容1</Card>
    <Card>内容2</Card>
</PageContainer>
```

## 标签页模式

通过 `mode` 属性设为 `tabs` 切换成标签页模式。

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
    mode="tabs"
>
    <Tabs>
        <Tabs.TabPane tab="组织概览" key="overview">
            组织概览
        </Tabs.TabPane>
        <Tabs.TabPane tab="项目列表" key="list">
            项目列表
        </Tabs.TabPane>
    </Tabs>
</PageContainer>
```

## 卡片标签模式

通过 `mode` 属性设为 `tabs-card` 切换成卡片 + 标签页的混合模式。

```jsx live fff
<PageContainer
    backUrl='/'
    title="详情页"
    mode="tabs-card"
>
    <Tabs>
        <Tabs.TabPane tab="组织概览" key="overview">
            <Card style={{marginBottom: '20px'}}>内容1</Card>
            <Card>内容2</Card>
        </Tabs.TabPane>
        <Tabs.TabPane tab="项目列表" key="list">
            <Card style={{marginBottom: '20px'}}>内容3</Card>
            <Card>内容4</Card>
        </Tabs.TabPane>
    </Tabs>
</PageContainer>
```

## 单个标题组件

通过 `PageContainer.PageTitle` 可单独使用 PageTitle 组件。

```jsx live fff
<PageContainer.PageTitle
    backText="返回"
    backUrl='/'
    title="标题"
    custom={<span>这是自定义内容</span>}
    description="页面描述"
    extra={<span>扩展信息</span>}
    btnConfig={[
        {
            id: 'base-custom-btn-id',
            text: '按钮1',
            btnAction: () => console.log('click btn1')
        },
        {
            text: '按钮2',
            disabled: true,
            tooltip: {
                title: '提示信息'
            },
            btnAction: () => console.log('click btn2')
        }
    ]}
/>
```

## 单个列表组件

通过 `PageContainer.List` 可单独使用 List 组件。

```jsx live fff
function App() {
    const data = [
        {
            key: '1',
            name: 'John Brown',
            age: 32,
            address: 'New York No. 1 Lake Park'
        },
        {
            key: '2',
            name: 'Jim Green',
            age: 42,
            address: 'London No. 1 Lake Park'
        },
        {
            key: '3',
            name: 'Joe Black',
            age: 32,
            address: 'Sidney No. 1 Lake Park'
        }
    ];

    const columns = [
        {
            title: 'Name',
            dataIndex: 'name',
            key: 'name',
            render: text => <a>{text}</a>
        },
        {
            title: 'Age',
            dataIndex: 'age',
            key: 'age'
        },
        {
            title: 'Address',
            dataIndex: 'address',
            key: 'address'
        }
    ];

    const tabList = [
        {
            tab: '任务详情',
            key: 'base',
            content: <Table columns={columns} dataSource={data} />,
            description: '任务详情的描述信息，这是任务详情的描述信息'
        },
        {
            tab: '评估报告',
            key: 'report',
            content: <Table columns={columns} dataSource={data} />,
            description: '评估报告的描述信息，这是评估报告的描述信息'
        }
    ];

    return (
        <div className="acux-demo-container acux-demo-layout-background">
            <PageContainer.List
                title="可视化建模"
                description="通过拖拉拽和拼接组件的⽅式，形成建模流程。⽤户配置组件参数后，即可训练模型。"
                descLink={'/assistance/doc?path=/bml/可视化建模/概述'}
                tabList={tabList}
                tabInfo={{
                    defaultActiveKey: 'base'
                }}
            >
                <Table columns={columns} dataSource={data} />
            </PageContainer.List>
        </div>
    );
}
```

## 单个详情组件

通过 `PageContainer.Detail` 可单独使用 Detail 组件。

```jsx live fff
function App() {
    const tabList = [
        {
            tab: '任务信息',
            key: 'baseInfo',
            content: '测试内容1',
            description: '任务详情的描述信息，这是任务详情的描述信息'
        },
        {
            tab: '训练过程',
            key: 'training-process',
            content: '测试内容2',
            description: '评估报告的描述信息，这是评估报告的描述信息'
        }
    ];

    const btnConfig = [
        {
            text: '复制',
            btnAction: () => history.push('/admin/abc')
        }
    ];

    return (
        <div className="acux-demo-container acux-demo-layout-background">
            <PageContainer.Detail
                title="数据详情"
                backUrl="/"
                btnConfig={btnConfig}
                tabList={tabList}
                tabInfo={{
                    defaultActiveKey: 'base'
                }}
            />
        </div>
    );
}
```

## API

| 参数          | 说明                 | 类型                        | 默认值 |
| ------------- | -------------------- | --------------------------- | ------ |
| showPageTitle | 是否显示 header 部分 | `boolean`                   | `--`   |
| mode          | 布局模式类型         | `card`〡`tabs`〡`tabs-card` | `--`   |

## PageTitle API

| 参数      | 说明       | 类型         | 默认值 |
| --------- | ---------- | ------------ | ------ |
| id        | ID         | `string`     | `--`   |
| disabled  | 不可点击   | `boolean`    | `--`   |
| text      | 按钮文本   | `ReactNode`  | `--`   |
| tooltip   | hover 提示 | `any`        | `--`   |
| className | 类名       | `string`     | `--`   |
| btnAction | 操作方法   | `() => void` | `--`   |

PageTitle 组件的定义：

```ts
export interface PageTitleProps {
    title?: ReactNode; // 标题
    backText?: string; // 返回的文本
    backUrl?: string | object & {pathname: string}; // 返回的 url
    defaultBackUrl?: string;
    backParams?: any; // 返回的参数
    className?: string; // class 名称
    custom?: ReactNode; // 自定义 title 位置的文本
    extra?: ReactNode; // title 右侧扩展信息
    btnConfig?: PageTitleBtnProps[] // 按钮配置
    description?: ReactNode; // 换行的描述信息
}
```
