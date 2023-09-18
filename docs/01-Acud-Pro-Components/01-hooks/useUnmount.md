---
title: useUnmount
---

用于设定在组件卸载时执行的 hooks。

## 引入

```js
import {useUnmount} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [state, {toggle}] = useToggle();

    const UnmountComp = () => {
        useUnmount(() => {
            message.success('unmount');
        });
        return <p>unmountComp</p>;
    };

    return (
        <>
            <Button onClick={toggle}>切换 unmount 值</Button>
            {state && <UnmountComp />}
        </>
    );
}
```

## API

```typescript static
type useUnmount = (fn: () => void) => void;
```

| 参数 | 说明                 | 类型         | 默认值 |
| ---- | -------------------- | ------------ | ------ |
| fn   | 组件卸载时执行的函数 | `() => void` | `--`   |
