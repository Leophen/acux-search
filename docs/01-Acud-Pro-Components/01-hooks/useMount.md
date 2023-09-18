---
title: useMount
---

用于设定在组件挂载时执行的 hooks。

## 引入

```js
import {useMount} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const MountComp = () => {
        useMount(() => {
            message.success('mount');
        });
        return <p>mountComp</p>;
    };

    const [state, {toggle}] = useToggle();

    return (
        <>
            <Button onClick={toggle}>切换 mount 值</Button>
            {state && <MountComp />}
        </>
    );
}
```

## API

```typescript static
type useMount = (fn: () => void) => void;
```

### Params

| 参数 | 说明                 | 类型         | 默认值 |
| ---- | -------------------- | ------------ | ------ |
| fn   | 组件挂载时执行的函数 | `() => void` | `--`   |
