---
title: usePrevious
---

用于设定保存上一次渲染状态的 hooks。

## 引入

```js
import {usePrevious} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [count, setCount] = useState(0);
    const previous = usePrevious(count);

    return (
        <>
            <p>currentValue: {count}</p>
            <p>previousValue: {previous}</p>
            <Button onClick={() => setCount(c => c + 1)}>
                add
            </Button>
        </>
    );
}
```

## API

```typescript static
const previous: T | undefined = usePrevious<T>(state: T);
```

### Result

| 参数     | 说明                 | 类型 | 默认值 |
| -------- | -------------------- | ---- | ------ |
| previous | 被记录状态的上次的值 | `T`  | `--`   |

### Params

| 参数  | 说明                 | 类型 | 默认值 |
| ----- | -------------------- | ---- | ------ |
| state | 需要记录变化的状态值 | `T`  | `--`   |
