---
title: fileUtil
---

文件相关工具。

## 引入

```js
import {fileUtil} from 'baidu-acu-react-common';

const {filesize, getSuffixByName} = fileUtil;
```

## 转换文件大小

`filesize` 用于转换文件大小。

- `kilo`：量级（默认是 1024）
- `decimals`：小数位数
- `decPoint`：小数点
- `thousandsSep`： 千位分割符
- `suffixSep`：suffixSep

```js
// 转换成 Mb, Gb 等格式的文件大小
filesize(1024, {decimals: 4, thousandsSep: ','})
```

## 获取文件后缀

```js
getSuffixByName('https://aaa.com/a.mp4') // mp4
isAbsolutePath('/a/b/c/b.doc') // doc
```
