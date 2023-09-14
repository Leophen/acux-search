---
title: useDialog
---

触发对话框或抽屉组件的 hooks

## 引入

```js
import { hooks } from 'baidu-acu-react-common';

const { useDialog } = hooks;
```

## 触发对话框

对话框可通过将 `Dialog`、`dialogOpen`、`setDialogOptions`、`handleDialogCancel` 解构出来使用，其中对话框内容组件支持点击确认按钮调用内部的 `doSubmit` 方法。$$

```jsx live fff
function App() {
    const { Dialog, dialogOpen, setDialogOptions, handleDialogCancel } = useDialog();

    const DialogContent = React.forwardRef((props, ref) => {
        const { onSuccess } = props;

        const doSubmit = () => Promise.resolve().then(() => onSuccess());

        // 关联 doSubmit 到 ref 上
        useImperativeHandle(
            ref,
            () => ({ doSubmit })
        );

        return (
            <div>对话框内容</div>
        );
    });

    const handleShowDialog = () => {
        const dialogOptions = {
            dialogType: 'common',
            className: 'aibp-bml-description-modal',
            title: '对话框标题',
            width: 500,
            maskClosable: true,
            wrappedComponent: DialogContent,
            payload: {}
        };
        setDialogOptions(dialogOptions);
    }

    const handleDialogSuccess = () => {
        message.success('success message!');
    };

    return (
        <>
            <Button onClick={handleShowDialog}>打开对话框</Button>
            {Dialog && (
                <Dialog
                    open={dialogOpen}
                    onCancel={handleDialogCancel}
                    onSuccess={handleDialogSuccess}
                />
            )}
        </>
    );
}
```

## 触发抽屉

抽屉使用方法与对话框同理，区别在于 `setDialogOptions` 的参数中控制 `type` 字段为 `drawer`。

```jsx live fff
function App() {
    const { Dialog, dialogOpen, setDialogOptions, handleDialogCancel } = useDialog();

    const DialogContent = React.forwardRef((props, ref) => {
        const { onSuccess } = props;

        const doSubmit = () => Promise.resolve().then(() => onSuccess());

        // 关联 doSubmit 到 ref 上
        useImperativeHandle(
            ref,
            () => ({ doSubmit })
        );

        return (
            <div>抽屉内容</div>
        );
    });

    const handleShowDialog = () => {
        const dialogOptions = {
            type: 'drawer',
            dialogType: 'common',
            className: 'aibp-bml-description-modal',
            title: '抽屉标题',
            width: 500,
            maskClosable: true,
            wrappedComponent: DialogContent,
            payload: {}
        };
        setDialogOptions(dialogOptions);
    }

    const handleDialogSuccess = () => {
        message.success('success message!');
    };

    return (
        <>
            <Button onClick={handleShowDialog}>打开抽屉</Button>
            {Dialog && (
                <Dialog
                    open={dialogOpen}
                    onCancel={handleDialogCancel}
                    onSuccess={handleDialogSuccess}
                />
            )}
        </>
    );
}
```

## 配合 HooksForm 使用

`DialogOptions` 的 `wrappedComponent` 一般为 `<HooksForm />` 组件，使用如下：

```jsx live fff
function App() {
    return (
        <>
            TODO...
        </>
    );
}
```

## UseDialogType

```ts
interface UseDialogType {
    Dialog: React.ReactNode;
    dialogOpen: boolean;
    showDialog: () => void;
    hideDialog: () => void;
    dialogOptions: object;
    setDialogOptions: () => void;
    handleDialogCancel: () => void;
}
```

## DialogOptions API

| 属性              | 说明                                       | 类型                                | 默认值   |
| ----------------- | ------------------------------------------ | ----------------------------------- | -------- |
| antdProps         | Antd 属性传入（可选）                      | `Object`                            | `--`     |
| cancelText        | 取消文本（可选）                           | `string`                            | `取消`   |
| cancelWithSuccess | 设置可以支持关闭弹框，同时刷新页面（可选） | `boolean`                           | `false`  |
| className         | 弹窗类名（可选）                           | `string`                            | `--`     |
| dialogType        | 弹框类型（可选）                           | `plain（纯展示）〡common（有交互）` | `common` |
| foot              | 是否需要底部（可选）                       | `boolean`                           | `true`   |
| mask              | 是否显示遮罩（可选）                       | `boolean`                           | `true`   |
| maskClosable      | 遮罩是否可点击关闭（可选）                 | `boolean`                           | `false`  |
| okText            | 确认文本（可选）                           | `string`                            | `确定`   |
| payload           | 传入的数据（可选）                         | `Object`                            | `--`     |
| type              | 弹窗类型（可选）                           | `dialog〡drawer`                    | `dialog` |
| title             | 弹窗标题（可选）                           | `string`                            | `--`     |
| width             | 弹窗高度（可选）                           | `number`                            | `378`    |
| wrappedComponent  | 弹窗内容组件                               | `ReactNode`                         | `--`     |
