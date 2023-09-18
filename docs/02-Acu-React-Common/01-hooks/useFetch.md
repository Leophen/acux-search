---
title: useFetch
---

用于请求获取数据的 hooks。

:::note 说明

发送请求获取数据，当 hook 组件存在时会一直有效。

默认是 hook 生成之后就生效，可以设置 abort 参数来手动开始发送请求。

:::

## 引入

```js
import {request, useFetch} from 'baidu-acu-react-common';
```

## 基本用法

```jsx live fff
function App() {
    const url = 'https://yapi.baidu-int.com/mock/23714/api/list';

    const action = () => {
        return request.post(url);
    };

    const columns = [
        {
            key: 'id',
            title: 'ID',
            dataIndex: 'id'
        },
        {
            key: 'name',
            title: '名称',
            dataIndex: 'name'
        }
    ];

    const FetchDemo = () => {
        const {data, loading} = useFetch(action);
        const {result, pageNo, pageSize, totalCount} = data || {};

        return (
            <Table
                rowKey="id"
                loading={loading}
                dataSource={result}
                columns={columns}
                pagination={{current: pageNo, total: totalCount}}
            />
        );
    }

    return (
        <FetchDemo />
    );
}
```

## API

```js
useFetch(
    action: (params?: any) => Promise<TData>,
    params?: TParam,
    $onRequest?: (payload?: any) => any,
    $onResponse?: (result?: any) => any,
    $onError?: (ex: any) => void,
    abort?: boolean
)
```

## 参考文档

<https://react-app-common.now.baidu-int.com/#/hooks/UseFetch>
