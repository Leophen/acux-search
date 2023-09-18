---
title: Enum
---

通用枚举类工具。

## 初始化

```js
import {Enum} from 'baidu-acu-react-common';

const statusEnum = new Enum(
    {alias: 'NORMAL', text: '正常', value: 'normal'},
    {alias: 'DISABLED', text: '禁用', value: 'disabled'},
    {alias: 'DELETED', text: '已删除', value: 'deleted'}
);

const normalStatus = {alias: 'NORMAL', text: '正常', value: 'normal'};
```

## alias 和 value 相互映射

```js
statusEnum.NORMAL; // 'normal'
statusEnum.normal // 'NORMAL'
```

## fromValue()

```js
statusEnum.fromValue('normal');
// {alias: 'NORMAL', text: '正常', value: 'normal'}
```

## fromAlias()

```js
statusEnum.fromAlias('NORMAL');
// {alias: 'NORMAL', text: '正常', value: 'normal'}
```

## fromText()

```js
statusEnum.fromText('正常');
// {alias: 'NORMAL', text: '正常', value: 'normal'}
```

## getTextFromValue()

```js
statusEnum.getTextFromValue('disabled');
// '禁用'
```

## getTextFromAlias()

```js
statusEnum.getTextFromAlias('NORMAL');
// '正常'
```

## getValueFromAlias()

```js
statusEnum.getValueFromAlias('NORMAL');
// 'normal'
```

## getValueFromText()

```js
statusEnum.getValueFromText('正常');
// 'normal'
```

## getAliasFromValue()

```js
statusEnum.getValueFromText('normal');
// 'NORMAL'
```

## getAliasFromText()

```js
statusEnum.getAliasFromText('正常');
// 'NORMAL'
```

## toJson()

```js
statusEnum.toJson();
// {
//     normal: '正常',
//     disabled: '禁用',
//     deleted: '已删除'
// };
```

## toArray()

```js
statusEnum.toArray();
// const statusArray = [
//     {alias: 'NORMAL', text: '正常', value: 'normal', label: '正常'},
//     {alias: 'DISABLED', text: '禁用', value: 'disabled', label: '禁用'},
//     {alias: 'DELETED', text: '已删除', value: 'deleted', label: '已删除'}
// ];
```
