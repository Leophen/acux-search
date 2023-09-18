---
title: useLatest
---

用于获取当前最新值的 hooks。

## 引入

```js
import {useLatest} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [count1, setCount1] = useState(0);
    const [count2, setCount2] = useState(0);
    const latestCountRef = useLatest(count2);

    useEffect(() => {
        const interval = setInterval(() => {
            setCount1(count1 + 1);
            setCount2(latestCountRef.current + 1);
        }, 1000);

        return () => clearInterval(interval);
    }, []);


   return (
        <>
            <p>非最新 count: {count1}</p>
            <p>最新 count: {count2}</p>
        </>
    );
}
```

## API

```ts
const latestValueRef = useLatest<T>(value: T): MutableRefObject<T>;
```
