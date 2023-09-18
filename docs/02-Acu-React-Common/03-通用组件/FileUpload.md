---
title: FileUpload
---

配合 form 使用的文件上传组件。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const FileUpload = components.FileUpload;
```

## 基本用法

```jsx live fff
<FileUpload action="/upload"/>
```

## 设置默认值

```jsx live fff
<FileUpload
    action="/upload"
    value={[{uid: 1, name: 'test.txt', status: 'done', url: '/test.txt'}]}
/>
```

## API

| 参数         | 说明                         | 类型                                      | 默认值                                             |
| ------------ | ---------------------------- | ----------------------------------------- | -------------------------------------------------- |
| action       | 上传的地址                   | `string`                                  | `/file/upload`                                     |
| value        | 默认文件                     | `object[]`                                | `无`                                               |
| tipText      | 提示文字                     | `string`                                  | `'注意：请调整文件名后再上传，以便其他人可以识别'` |
| onChange     | 文件上传成功或被移除时的回调 | `Function`                                | `无`                                               |
| beforeUpload | 上传文件之前的钩子           | `(file: any, fileList: any[]) => boolean` | `无`                                               |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/FileUpload>
