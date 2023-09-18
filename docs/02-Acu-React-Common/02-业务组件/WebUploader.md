---
title: WebUploader
---

WebUploader 分片上传组件

- 支持多个文件上传；
- 支持文件分片上传；
- 支持文件图片和文件预览功能，及查看上传进度；
- 支持文件大小、文件数量和文件类型限制；
- 支持与 `createBaseForm` 共同使用。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const {WebUploader} = components;
```

## 基本用法

```jsx
function App() {
    // 取消上传
    function handleCancelUpload() {
    }

    // 所有文件上传完成
    function handleUploadFinished(totalResult) {
    }

    function handleFilesChange(files) {
    }

    return (
        <WebUploader
            label="选择文件"
            accept="png,jpg"
            beforeSendFileUrl="/api/file/upload/init"
            url="/api/file/upload/upload"
            afterSendFileUrl="/api/file/upload/complete"
            multiple
            hideStartBtn
            autoStart
            maxFileSize={5 * 1024 * 1024 * 1024}
            maxFileCount={300}
            fileNamePattern={/^[\u4e00-\u9fa5_a-zA-Z0-9.-]+$/}
            onUploadFinished={handleUploadFinished}
            onCancelUpload={handleCancelUpload}
            onChange={handleFilesChange}
        />
    );
}
```

## API

| 参数              | 说明                                  | 类型     | 默认值     |
| ----------------- | ------------------------------------- | -------- | ---------- |
| label             | 按钮文案 选填                         | string   | '选择文件' |
| url               | 上传接口地址 必填                     | string   | 无         |
| beforeSendFileUrl | 上传前的接口，主要用来分片上传 选填   | string   | 无         |
| afterSendFileUrl  | 上传之后的接口，主要用来分片上传 选填 | string   | 无         |
| disabled          | 是否禁用                              | bool     | false      |
| autoStart         | 是否自动发起上传                      | bool     | false      |
| hideStartBtn      | 是否隐藏发起上传按钮                  | bool     | false      |
| multiple          | 是否多文件上传                        | bool     | false      |
| maxFileCount      | 文件上传数量限制                      | number   | -1 不限制  |
| maxFileSize       | 单个文件上传大小限制                  | number   | -1 不限制  |
| accept            | 支持上传文件的后缀                    | string   | ''         |
| fileNamePattern   | 文件名要求正则 选填                   | string   | ''         |
| payload           | 其他上传输入参数 选填                 | object   | {}         |
| uploaderOptions   | webuploader底层其他配置项 选填        | object   | {}         |
| onChange          | 文件上传状态修改时的事件              | function |            |
| onUploadCompleted | 上传完成后的事件                      | function |            |
| onCancelUpload    | 取消上传后的事件                      | function |            |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E4%B8%9A%E5%8A%A1%E7%BB%84%E4%BB%B6/WebUploader>
