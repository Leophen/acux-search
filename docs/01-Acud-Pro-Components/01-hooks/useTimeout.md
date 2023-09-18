---
title: useTimeout
---

用于设置过多少毫秒执行指定方法的 hooks。

:::caution 注意

- 不会导致 reRender 组件；
- 如果第一次不想直接发起，可以通过设置 useTimeout 第二个参数“延迟毫秒数”为负数来实现，否则在进入组件时会直接发起一次 timeout；
- 当延时时长改变时自动重置 timeout；
- 可以通过调用暴露的 clear 方法随时取消 timeout；
- 可以通过调用暴露的 set 方法来发起一个新的 timeout；
- useTimeout 第一个参数“方法”的改变并不会重置 timeout，除非调用 set 方法。

:::

## 引入

```js
import {useTimeout} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [timeoutDelay, setTimeoutDelay] = useState(-1);
    function fn() {
        console.log(`called at ${Date.now()}`);
    }

    // 如果第一次不需要发起 timeout
    // 第二个参数通过设置负数来实现，否则直接传值即可
    const {set, clear} = useTimeout(fn, timeoutDelay);

    const startTimeout = useCallback(() => {
        setTimeoutDelay(3000);
        set();
    }, [timeoutDelay]);

    return (
        <div className="acux-demo-row">
            <Button onClick={startTimeout}>发起 setTimeout</Button>
            <Button onClick={clear}>取消 setTimeout</Button>
        </div>
    );
}
```

## API

```typescript static
const {
    set: () => void,
    clear: () => void
} = useTimeout(callback: () => void, ms: number = 0);
```

- `callback`: `Function` - 要被延迟执行的方法;
- `ms`: `number` - 延迟毫秒数;
- `clear`: `() => void` - 取消 timeout
- `set`: `() => void` - 重置 timeout
