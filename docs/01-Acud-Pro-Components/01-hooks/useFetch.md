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
import {request, useFetch} from '@baidu/acud-pro-components';
```

## action 为普通函数

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

## 经过 bindActionCreators 处理

action 经过了 `bindActionCreators` 处理：

```js
const action = () => {
    return async dispatch => {
        const result = await request.post(url);
        dispatch({
            type: 'LIST',
            result
        });
        return result;
    };
};

const mapDispatchToProps = dispatch => ({
    action: bindActionCreators(action, dispatch)
});
```

**示例：**

- 引入

```js
import React from 'react';
import thunk from 'redux-thunk';
import {Table} from 'acud';
import {connect, Provider, useSelector} from 'react-redux';
import {createStore, bindActionCreators, compose, applyMiddleware} from 'redux';
import {request, useFetch} from '@baidu/acud-pro-components';
```

- 使用

```jsx live fff
function App() {
    const reducer = (state = [], action) => {
        switch (action.type) {
            case 'LIST':
                return action.result;
            default:
                return state;
        }
    };

    const store = createStore(reducer, compose(applyMiddleware(thunk)));

    const url = 'https://yapi.baidu-int.com/mock/23714/api/list';

    const action = () => {
        return async dispatch => {
            const result = await request.post(url);
            dispatch({
                type: 'LIST',
                result
            });
            return result;
        };
    };

    const mapStateToProps = (state, ownProps) => ownProps;

    const mapDispatchToProps = dispatch => ({
        action: bindActionCreators(action, dispatch)
    });

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

    const FetchDemo = connect(mapStateToProps, mapDispatchToProps)(props => {

        const {action} = props;
        const state = useSelector(state => state);

        const {loading} = useFetch(action);
        const {result, pageNo, pageSize, totalCount} = state || {};

        return (
            <Table
                rowKey="id"
                loading={loading}
                dataSource={result}
                columns={columns}
                pagination={{current: pageNo, total: totalCount}}
            />
        );
    });

    return (
        <Provider store={store}>
            <FetchDemo />
        </Provider>
    );
}
```

## 未经过 bindActionCreators 处理

action 未经过 `bindActionCreators` 处理，但使用了 `dispatch` (该场景其实不合理，但为了兼容旧代码)

```js
const action = () => {
    return async dispatch => {
        const result = await request.post(url);
        dispatch({
            type: 'LIST',
            result
        });
        return result;
    };
};
```

**示例：**

- 引入

```js
import React from 'react';
import axios from 'axios';
import thunk from 'redux-thunk';
import {Table} from 'acud';
import {connect, Provider, useSelector} from 'react-redux';
import {createStore, compose, applyMiddleware} from 'redux';
import {request, useFetch} from '@baidu/acud-pro-components';
```

- 使用

```jsx live fff
function App() {
    const reducer = (state = [], action) => {
        switch (action.type) {
            case 'LIST':
                return action.result;
            default:
                return state;
        }
    };

    const store = createStore(reducer, compose(applyMiddleware(thunk)));

    const url = 'https://yapi.baidu-int.com/mock/23714/api/list';

    const action = () => {
        return async dispatch => {
            const result = await request.post(url);
            dispatch({
                type: 'LIST',
                result
            });
            return result;
        };
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

    const FetchDemo = props => {

        const state = useSelector(state => state);

        const {loading} = useFetch(action);
        const {result, pageNo, pageSize, totalCount} = state || {};

        return (
            <Table
                rowKey="id"
                loading={loading}
                dataSource={result}
                columns={columns}
                pagination={{current: pageNo, total: totalCount}}
            />
        );
    };

    return (
        <Provider store={store}>
            <FetchDemo />
        </Provider>
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
