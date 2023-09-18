---
title: BOSUploader
---

BOS 上传通用组件。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const {BOSUploader} = components;
```

## 基本用法

```jsx live fff
function App() {
    function onUploadCompleted() {}

    return (
        <BOSUploader
            label="选择文件"
            bosEndpoint="https://xxx.bj.bcebos.com/"
            uptokenUrl="/api/demo/upload_auth"
            path="a/b/c"
            multiple={true}
            autoStart={false}
            hideStartBtn={false}
            maxFileSize="10Mb"
            maxFileCount={5}
            onUploadCompleted={onUploadCompleted}
        />
    );
}
```

## API

| 参数              | 说明                           | 类型       | 默认值        |
| ----------------- | ------------------------------ | ---------- | ------------- |
| bosEndpoint       | BOS服务器的地址 必填项         | `string`   | `--`          |
| uptokenUrl        | 用来算签名的后端api地址 必填项 | `string`   | `--`          |
| path              | bos路径                        | `string`   | `--`          |
| label             | 按钮文案                       | `string`   | `选择文件`    |
| btnId             | 按钮id                         | `string`   | `bosUploader` |
| disabled          | 是否禁用                       | `boolean`  | `false`       |
| autoStart         | 是否自动发起上传               | `boolean`  | `false`       |
| hideStartBtn      | 是否隐藏发起上传按钮           | `boolean`  | `false`       |
| multiple          | 是否多文件上传                 | `boolean`  | `false`       |
| maxFileCount      | 文件上传数量限制               | `number`   | `不限制`      |
| maxFileSize       | 单个文件上传大小限制           | `string`   | `50Gb`        |
| accept            | 支持上传文件的后缀             | `string`   | `--`          |
| onUploadCompleted | 上传完成后的事件               | `function` | `--`          |
| startUpload       | 开始上传方法                   | `function` | `--`          |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E4%B8%9A%E5%8A%A1%E7%BB%84%E4%BB%B6/BOSUploader>
