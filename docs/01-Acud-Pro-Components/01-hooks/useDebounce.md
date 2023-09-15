---
title: useDebounce
---

用于设置防抖值的 hooks。

## 引入

```js
import {useDebounce} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [value, setValue] = useState();
    const debounceValue = useDebounce(value, {wait: 1000});

    return (
        <>
            <Input value={value} onChange={e => setValue(e.target.value)} />
            <p>DebouncedValue: {debounceValue}</p>
        </>
    );
}
```

## API

| 参数    | 说明           | 类型      | 默认值 |
| ------- | -------------- | --------- | ------ |
| value   | 需要防抖的值   | `any`     | `--`   |
| options | 配置防抖的行为 | `Options` | `--`   |

## Options

| 参数     | 说明                     | 类型      | 默认值  |
| -------- | ------------------------ | --------- | ------- |
| wait     | 超时时间，单位为毫秒     | `number`  | `1000`  |
| leading  | 是否在延迟开始前调用函数 | `boolean` | `false` |
| trailing | 是否在延迟开始后调用函数 | `boolean` | `true`  |
| maxWait  | 最大等待时间，单位为毫秒 | `number`  | `--`    |
