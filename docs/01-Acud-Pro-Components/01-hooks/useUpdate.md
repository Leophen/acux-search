---
title: useUpdate
---

用于主动使组件重新渲染的 hooks。

## 引入

```js
import {useUpdate} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const update = useUpdate();
    const renderCount = React.useRef(0);
    renderCount.current += 1;

    return (
        <>
            <div>renderCount: {renderCount.current}</div>
            <Button onClick={update}>update</Button>
        </>
    );
}
```

## API

```typescript static
type useUpdate = () => () => void
```

| 参数   | 说明               | 类型         | 默认值 |
| ------ | ------------------ | ------------ | ------ |
| update | 用来强制更新的函数 | `() => void` | `--`   |
