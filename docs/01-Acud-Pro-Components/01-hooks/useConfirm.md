---
title: useConfirm
---

用于打开弹框和抽屉的 hooks。

## 引入

```js
import {useConfirm} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    const {Confirm, setConfirmOptions} = useConfirm();

    const showConfirm = () => {
        const confirmOptions = {
            title: '确认',
            content: '内容',
            onOk: () => {console.log(123)}
        };
        setConfirmOptions(confirmOptions);
    };

    return (
        <>
            <Button onClick={showConfirm}>显示确认框</Button>
            {Confirm}
        </>
    );
}
```

## 不同类型

通过 `type` 属性控制弹框类型。

```jsx live fff
function App() {
    const {Confirm, setConfirmOptions} = useConfirm();

    const showConfirm = type => {
        const confirmOptions = {
            type,
            title: '确认',
            content: '内容',
            onOk: () => {
                console.log(123);
            }
        };
        setConfirmOptions(confirmOptions);
    };

    return (
        <>
            <div className="acux-demo-row">
                <Button onClick={() => showConfirm('warning')}>warning</Button>
                <Button onClick={() => showConfirm('info')}>info</Button>
                <Button onClick={() => showConfirm('error')}>error</Button>
            </div>
            {Confirm}
        </>
    );
}
```

## 隐藏遮罩

通过 `mask` 属性控制弹框类型。

```jsx live fff
function App() {
    const {Confirm, setConfirmOptions} = useConfirm();

    const showConfirm = () => {
        const confirmOptions = {
            title: '确认',
            content: '内容',
            mask: false,
            onOk: () => {console.log(123)}
        };
        setConfirmOptions(confirmOptions);
    };

    return (
        <>
            <Button onClick={showConfirm}>显示确认框-隐藏遮罩</Button>
            {Confirm}
        </>
    );
}
```

## API

| 参数       | 说明         | 类型                                         | 默认值    |
| ---------- | ------------ | -------------------------------------------- | --------- |
| type       | 弹框类型     | `warning`〡`success`〡`info`〡`error`        | `warning` |
| title      | 弹框标题     | `string`                                     | `--`      |
| content    | 弹框内容     | `ReactNode`                                  | `--`      |
| visible    | 是否显示     | `boolean`                                    | `--`      |
| footer     | 弹框底部     | `ReactNode`                                  | `--`      |
| okText     | 确认文本     | `string`                                     | `确定`    |
| cancelText | 取消文本     | `string`                                     | `取消`    |
| mask       | 是否显示遮罩 | `boolean`                                    | `true`    |
| onOk       | 确认回调     | `(e: React.MouseEvent<HTMLElement>) => void` | `--`      |
| onCancel   | 取消回调     | `(e: React.MouseEvent<HTMLElement>) => void` | `--`      |
