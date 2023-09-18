---
title: useThrottle
---

用于设置节流值的 hooks。

## 引入

```js
import {useThrottle} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [value, setValue] = useState();
    const throttleValue = useThrottle(value, {wait: 1000});

    return (
        <>
            <Input value={value} onChange={e => setValue(e.target.value)} />
            <p>ThrottledValue: {throttleValue}</p>
        </>
    );
}
```

## API

```typescript static
const throttledValue = useThrottle(
    value: any,
    options?: Options
);
```

### Params

| 参数    | 说明           | 类型      | 默认值 |
| ------- | -------------- | --------- | ------ |
| value   | 需要节流的值   | `any`     | `--`   |
| options | 配置节流的行为 | `Options` | `--`   |

### Options

| 参数     | 说明                     | 类型      | 默认值  |
| -------- | ------------------------ | --------- | ------- |
| wait     | 等待时间，单位为毫秒     | `number`  | `1000`  |
| leading  | 是否在延迟开始前调用函数 | `boolean` | `false` |
| trailing | 是否在延迟开始后调用函数 | `boolean` | `true`  |
