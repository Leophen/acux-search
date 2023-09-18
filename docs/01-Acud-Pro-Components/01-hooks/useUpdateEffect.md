---
title: useUpdateEffect
---

用于忽略首次执行仅在依赖项更新时执行的等效 useEffect 的 hooks。

## 引入

```js
import {useUpdateEffect} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [count, setCount] = React.useState(0);
    const [effectCount, setEffectCount] = useState(0);
    const [updateEffectCount, setUpdateEffectCount] = useState(0);

    useEffect(() => {
        setEffectCount(effectCount + 1);
    }, [count]);

    useUpdateEffect(() => {
        setUpdateEffectCount(updateEffectCount + 1);
    }, [count]);

    return (
        <>
            <p>count: {count}</p>
            <p>effectCount: {effectCount}</p>
            <p>updateEffectCount: {updateEffectCount}</p>
            <Button onClick={() => setCount(count + 1)}>
                count++
            </Button>
        </>
    );
}
```
