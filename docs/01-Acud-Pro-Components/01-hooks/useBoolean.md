---
title: useBoolean
---

用于控制 boolean 值切换的 hooks。

## 引入

```js
import {useBoolean} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const [visible, show, hide] = useBoolean(false);

    return (
        <>
            <div className="acux-demo-row">
                <Button onClick={() => show()}>显示</Button>
                <Button onClick={() => hide()}>隐藏</Button>
            </div>
            {visible && (<p>要显示的内容</p>)}
        </>
    );
}
```

## API

```ts
type useBoolean = (initialValue: boolean = false) => [boolean, () => void, () => void]
```
