---
title: useFetchPolling
---

基于 [useFetch](./useFetch) 实现轮询请求的 hooks。

## 引入

```js
import {useFetchPolling} from 'baidu-acu-react-hooks';
```

## 基本用法

`useFetchPolling`  在除了 [useFetch](./useFetch) 的六个参数后，传入第七个参数 interval，单位为 ms，在上一个请求返回后，间隔 n（ms）后，再次发起请求。

如果 interval 不传，则会在请求返回后，立即发出再一次的请求。如果上一次的请求失败，轮询请求则停止。

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

    const Demo = props => {
        const [abort, setAbort] = useState(true);

        const action = useCallback(() => (
            new Promise(resolve => setTimeout(() => resolve({}), 500))
        ), []);

        useFetchPolling(
            action,
            {},
            payload => console.log('请求参数', payload),
            res => console.log('请求成功', res),
            error => console.log('请求失败', error),
            abort,
            1000
        );
        return (
            <div className="acux-demo-row">
                <Button onClick={() => setAbort(false)}>发送请求</Button>
                <Button onClick={() => setAbort(true)}>停止请求</Button>
            </div>
        );
    };

    return (
        <Provider store={store}>
            <Demo />
        </Provider>
    );
}
```

## API

```js
useFetchPolling(
    action: (params?: any) => Promise<TData>,
    params?: TParam,
    $onRequest?: (payload?: any) => any,
    $onResponse?: (result?: any) => any,
    $onError?: (ex: any) => void,
    abort?: boolean,
    interval?: number
) : {loading: boolean, data: any, error: any, reload: () => void, latestPayload: object}
```
