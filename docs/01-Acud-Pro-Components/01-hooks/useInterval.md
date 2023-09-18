---
title: useInterval
---

用于定时执行回调的 hooks。`useInterval` 无视 hook 刷新，当 hook 组件存在时会一直有效。默认是 hook 生成之后就生效，可以设置 abort 参数来手动开始。

## 引入

```js
import {useInterval} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [abort, setAbort] = useState(true);
    useInterval(() => console.log('handle Interval:', new Date()), 1000, abort);

    return (
        <Button onClick={() => setAbort(false)}>
            点击开始
        </Button>
    );
}
```

## API

```ts
useInterval((...args: any) => any, interval?: number, abort?: boolean)
```
