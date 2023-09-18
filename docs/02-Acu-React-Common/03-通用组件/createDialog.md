---
title: createDialog
---

创建弹框的高阶组件。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const {createDialog} = components;
```

## 基本用法

```jsx
import {Button} from 'antd';
import {useState} from 'react';

const WrappedComponent = () => (
    <div>弹框中的组件</div>
);

let Dialog = null;

const DialogDemo = () => {
    const [dialogOptions, setDialogOptions] = useState();
    const [dialogOpen, setDialogOpen] = useState(false);

    const showDialog = () => {
        const options = {
            dialogType: 'common',
            className: 'my-dialog',
            title: '我的弹框',
            width: 600,
            maskClosable: false, // 点击旁边弹框是否可关闭，默认为true
            foot: true, // 是否需要弹框底部，默认为true
            payload: {
                aa: 1
            } // 传到wappedComponent中的参数
        };
        setDialogOptions(options);
        setDialogOpen(true);
    };

    const handleDialogCancel = () => {
        Dialog = null;
        setDialogOptions(null);
    };
    const handleDialogSuccess = () => {
        console.log('handleDialogSuccess');
    };

    if (!Dialog && dialogOptions) {
        Dialog = CreateDialog(dialogOptions)(WrappedComponent);
    }

    return (
        <div>
            <Button type="primary" icon="plus" onClick={showDialog}>显示弹框</Button>
            {Dialog && (
                <Dialog
                    open={dialogOpen}
                    onCancel={handleDialogCancel}
                    onSuccess={handleDialogSuccess}
                />
            )}
        </div>
    );
};

<DialogDemo />
```

## API

### options

| 参数         | 说明                                          | 类型    | 默认值 |
| ------------ | --------------------------------------------- | ------- | ------ |
| dialogType   | 弹框类型, plain为纯展示类型，common一般有交互 | string  | common |
| className    | 样式名                                        | string  |        |
| title        | 弹框头部title                                 | string  |        |
| width        | 弹框宽度                                      | number  |        |
| maskClosable | 是否点击外面可以关闭弹框                      | boolean | true   |
| foot         | 是否需要弹框底部                              | boolean |        |
| payload      | 传入的数据                                    | object  |        |
| message      | 显示的信息                                    | string  |        |

### 弹框 Props

| 参数      | 说明                 | 类型     | 默认值 |
| --------- | -------------------- | -------- | ------ |
| open      | 是否打开弹框         | boolean  | false  |
| onSuccess | 成功时激活的方法     | function |        |
| onCancel  | 关闭弹框后激活的方法 | function |        |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/CreateDialog>
