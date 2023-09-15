---
title: useDeepCompareEffect
---

深拷贝比较判断依赖是否变化执行 useEffect， 变量中不可有方法，或者方法为外部引用，否则该变量将被判断为变化。

## 引入

```js
import {useDeepCompareEffect} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [time, setTime] = useState(0);
    const [deepTime, setDeepTime] = useState(0);
    const object = {
        number: 100
    };

    useEffect(() => {
        if (time < object.number) {
            setTime(prevTime => prevTime + 1);
        }
    }, [object]);

    useDeepCompareEffect(() => {
        if (deepTime < object.number) {
            setDeepTime(prevTime => prevTime + 1);
        }
    }, [object]);

    return (
        <>
            <p>useEffect: {time}</p>
            <p>useDeepCompareEffect: {deepTime}</p>
        </>
    );
}
```

## API

```js
useDeepCompareEffect(effect: React.EffectCallback, dep?: React.DependencyList | undefined);
```
