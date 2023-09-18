---
title: useToggle
---

用于控制在两个状态值间切换的 hooks。

## 引入

```js
import {useToggle} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [state, {toggle}] = useToggle();

    return (
        <>
            <p>ToggleState: {`${state}`}</p>
            <div>
                <Button onClick={toggle}>切换 toggle 值</Button>
            </div>
        </>
    );
}
```

## API

```typescript static
type useToggle = <T, U>(defaultValue: T = false, reverseValue?: U) =>
    [state: T | U, {toggle: () => void}]
```

### Params

| 参数         | 说明                     | 类型 | 默认值  |
| ------------ | ------------------------ | ---- | ------- |
| defaultValue | 可选项，传入默认的状态值 | `--` | `false` |
| reverseValue | 可选项，传入取反的状态值 | `--` | `--`    |

### Result

| 参数    | 说明           | 类型      | 默认值 |
| ------- | -------------- | --------- | ------ |
| state   | 对应当前状态值 | `--`      | `--`   |
| actions | 操作集合       | `Actions` | `--`   |

### Actions

| 参数   | 说明       | 类型         | 默认值 |
| ------ | ---------- | ------------ | ------ |
| toggle | 切换 state | `() => void` | `--`   |
