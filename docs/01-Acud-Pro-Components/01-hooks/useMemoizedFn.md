---
title: useMemoizedFn
---

用于来持久化函数的 hooks，主要用来解决 useCallback 本身声明依赖后带来的隐式重渲染问题和闭包陷阱。

## 引入

```js
import {useMemoizedFn} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const ReRenderCountComp = React.memo(({fn}) => {
        const renderCountRef = useRef(0);
        renderCountRef.current += 1;
        return (
            <div>
                <p>ReRender Count: {renderCountRef.current}</p>
                <Button onClick={fn}>
                    showParentCount
                </Button>
            </div>
        );
    });

    const [count, setCount] = useState(0);

    const notifyCountFn = useMemoizedFn(() => {
        message.success(`count: ${count}`);
    });

    const normalCallback = useCallback(() => {
        message.success(`count: ${count}`);
    }, [count]);

    const noDepCallback = useCallback(() => {
        message.success(`count: ${count}`);
    }, []);

    return (
        <div className="acux-demo-column">
            <div>
                <p>count: {count}</p>
                <Button onClick={() => setCount(count + 1)}>
                    setCount
                </Button>
            </div>

            <ReRenderCountComp fn={notifyCountFn} />
            <ReRenderCountComp fn={normalCallback} />
            <ReRenderCountComp fn={noDepCallback} />
        </div>
    );
}
```

## API

```typescript static
type useMemoizedFn = <T extends (...args: any[] => any)>(fn: T) => T
```

### Params

| 参数 | 说明               | 类型                      | 默认值 |
| ---- | ------------------ | ------------------------- | ------ |
| fn   | 需要被持久化的函数 | `(...args: any[]) => any` | `--`   |

### Result

| 参数 | 说明           | 类型                      | 默认值 |
| ---- | -------------- | ------------------------- | ------ |
| fn   | 被持久化的函数 | `(...args: any[]) => any` | `--`   |
