---
title: useLabelBox
---

支持图像标注展示 & 在线标注；标注类型包括图像分类、目标检测、图像分割等标注形式；

1. 标注展示
2. 在线标注（图像分类、目标检测、图像分割）
3. 标注缩略图（2种展示形式：图像缩略图、宫格缩略图）
4. 自定义标注展示样式

## 引入

```js
import {useDebounce} from 'baidu-acu-react-common';
```

## 使用方法

1、以下代码展示标注展示、在线标注、options 参数配置、onChange 事件；

```js static
import _ from 'lodash';
import {useCallback, useState, useMemo, useEffect} from 'react';
import {hooks, components} from 'baidu-acu-react-common';

// 相关hooks引入
const {useLabelBox} = hooks;
const {HooksLabelBox} = components;

// 图像信息
const defaultImage = {
    url: 'http://img2.imgtn.bdimg.com/it/u=1962045236,1139336730&fm=26&gp=0.jpg',
    width: 500,
    height: 334,
    grid: {
        rowCount: 5,
        columnCount: 5,
        color: 'blue'
    }
};

// 标签名&标注框样式声明
const labelNameStyle = {fontColor: '#FFFFFF', fontSize: 12, bgColor: '#1890FF'};
const labelTextStyle = {fontColor: '#000', fontSize: 12, bgColor: '#FFFFFF'};
const labelFeatureStyle = {strokeColor: '#0000FF', fillColor: '#FF0000', opacity: 0.5};
const labelDrawStyle = {strokeColor: '#0000FF'};
// 标注集合
const defaultLabels = [
    {
        key: '110', // [必传] 暂做必传处理，避免引发不可预知错误
        select: false, // 当前标注对象是否呈现选中态[目前由于底层限制，控制每次至多有一个select：true, 即每次最多只能编辑一个标注对象]
        label: { // 标签名配置
            name: '中国', // 标签名称
            style: labelNameStyle // 标签样式
        },
        type: 'rect', // 矩形，支持'rect'， 'polygon'
        texts: [{ // 该标注对象关联的文本集合，一般业务不需要
            position: {x: 20, y: 20},
            offset: {x: 0, y: 0},
            maxWidth: 100,
            text: '中国北京',
            style: labelTextStyle
        }],
        markers: [{ // 该标注对象关联的标记集合，一般业务不需要
            position: {x: 150, y: 100},
            offset: {x: 0, y: 0},
            events: {click: (p1, p2) => {
                console.log('p1, p2', p1, p2);
            }}
        }],
        points: [ // 该标注对象坐标信息【相对于图像左上角的坐标值】
            {x: 100, y: 50},
            {x: 200, y: 50},
            {x: 200, y: 150},
            {x: 100, y: 150}
        ],
        style: labelFeatureStyle // 标注框展示样式
    }
];

// useLabelBox:options配置
const options = props => ({
    id: 'map-container-id', // [必传] 标注区域的dom-id，此处设置唯一值即可
    wrapClassName: 'map-container-class', // [可选] 标注区域的dom-class，可根据业务需求自行决定是否添加
    container: { //[必传] 标注区域的dom-size，设置标注区域大小，支持相对单位
        width: '100%',
        height: 400
    },
    image: props.bizImage, //[必传] 图像信息
    labels: props.bizLabels, // [必传] 标注框信息
    mode: props.bizMode, // [必传] 当前标注模式【'pan'、‘drawRect’、‘drawPolygon’】，开发人员可自行决定切换模式
    deleteIcon: '', // [可选] 删除按钮icon[此处建议默认即可，即不传或者设置为空即可，建议设置此字段]
    drawStyle: labelDrawStyle, // [可选] 绘制过程样式
    filter: true // [可选] 是否触发默认内在过滤，默认false【内在过滤仅会对标注框是否超出图像区域进行过滤】
    clip: true // [可选] 是否需要进行内置图片内裁剪【默认不裁剪】，只针对绘制add情况
});

export default props => {
    // 业务变量声明
    const [bizLabels, setBizLabels] = useState(initLabels);
    const [bizImage] = useState(image);
    const [bizMode, setBizMode] = useState('pan');

    // labels数据change
    const handleLabelChange = useCallback((operateType, label, evt, wxy) => {
        // 有些中间状态是不需要进行label重设
        if (_.includes(['updating', 'boundsChanged', 'updateReset', 'hover'], operateType)) {
            return;
        }
        // 需要进行labels变化时，才进行setBizLabels，否则中间态持续执行，如果不停的setBizLabels会造成死循环
        setBizLabels(preLabels => {
            let newLabels = _.cloneDeep(preLabels);
            // label添加
            if (operateType === 'add') {
                newLabels.push({
                    key: `model-label-${_.uniqueId()}`,
                    label: {
                        name: '测试',
                        style: labelNameStyle
                    },
                    ...label,
                    style: labelFeatureStyle
                });
            }
            // label删除/更新/选中
            else if (_.includes(['delete', 'update', 'select'], operateType)) {
                const findIndex = _.findIndex(newLabels, {key: label.key});
                if (findIndex >= 0) {
                    newLabels.splice(findIndex, 1);
                    operateType === 'update' && newLabels.push(label);
                    operateType === 'select' && newLabels.push({...label, select: true});
                }
            }
            // 【【特别注意：特别注意：特别注意】】：reset 这一步目前必须，需要将label进行直接覆盖即可【作用：所有select: false】
            else if (operateType === 'reset') {
                const formatLabels = _.map(newLabels, label => ({...label, select: false}));
                newLabels = formatLabels;
            }
            return newLabels;
        });
    }, []);

    const {
        labelProps,
        gMap,
        initZoom
    } = useLabelBox(
        options,
        {bizLabels, bizImage, bizMode},
        handleLabelChange
    );

    // 模式切换事件
    const handleModeChange = useCallback(mode => {
        if (_.includes(['pan', 'drawRect'], mode)) {
            setBizMode(mode);
        }
        else if (mode === 'zoomIn' && gMap) {
            gMap.zoomIn();
        }
        else if (mode === 'zoomOut' && gMap) {
            gMap.zoomOut();
        }
        else if (mode === 'reset' && gMap && initZoom) {
            gMap.centerAndZoom({x: 0, y: 0}, initZoom);
        }
    }, [gMap, initZoom]);

    return (<HooksLabelBox {...labelProps} />);
};

```

2、 核心：在组件中使用 useLabelBox，它的三个参数是 options、props 和 onChange，返回一个对象如下说明：

- labelProps: 当前列表中展现的数据集合
- gMap: 标注主实例对象【关键对象】
- initZoom: 当前图像最佳展示zoom值，能够保证全图展示在标注容器中【复位可能使用】
- tools: {worldToScreen} 对外暴露方法

## 配置项

### useLabelBox 参数

| 参数     | 说明                                         | 类型              | 默认值 |
| -------- | -------------------------------------------- | ----------------- | ------ |
| options  | 配置数据                                     | `props => object` | `--`   |
| props    | options 配置方法接收参数                     | `any`             | `--`   |
| onChange | 监听事件: 具体说明参考下方 onChange 参数说明 | `args => void`    | `--`   |

```js static
// example: 
const {...} = useLabelBox(
    options,
    props,
    onChange
);
```

### options配置参数

| 参数          | 说明                                                                                  | 类型       | 默认值 |
| ------------- | ------------------------------------------------------------------------------------- | ---------- | ------ |
| id            | 标注区域的 dom-id，此处设置唯一值即可                                                 | `string`   | `--`   |
| wrapClassName | 标注区域的 dom-class                                                                  | `string`   | `--`   |
| container     | 标注区域的 dom-size，设置标注区域大小，支持相对单位                                   | `object`   | `--`   |
| image         | 图像信息，具体参看下方说明                                                            | `Image`    | `--`   |
| labels        | 标注集合                                                                              | `Label:[]` | `--`   |
| mode          | 当前标注模式【'pan'、‘drawRect’、‘drawPolygon’】                                      | `string`   | `--`   |
| deleteIcon    | 删除按钮 icon                                                                         | `string`   | `--`   |
| drawStyle     | 绘制过程样式，使用参考上方使用代码                                                    | `object`   | `--`   |
| filter        | 是否触发默认内在过滤，默认 false<br/>【内在过滤仅会对标注框是否超出图像区域进行过滤】 | `boolean`  | `--`   |
| clip          | 是否触发默认内在裁剪，默认 false                                                      | `boolean`  | `--`   |

```js static
// example: 
const options = props => ({
    id: 'map-container-id',
    wrapClassName: 'map-container-class',
    container: {
        width: '100%',
        height: 400
    },
    image: props.bizImage,
    labels: props.bizLabels,
    mode: props.bizMode,
    deleteIcon: '',
    drawStyle: labelDrawStyle,
    filter: true
});
```

### Image配置参数

| 参数             | 说明                    | 类型                               | 默认值 |
| ---------------- | ----------------------- | ---------------------------------- | ------ |
| url              | 标注图像的url           | `string`                           | `--`   |
| width            | 标注图像宽度:原始图宽度 | `string、number`                   | `--`   |
| height           | 标注图像高度:原始图高度 | `string、number`                   | `--`   |
| grid             | 图像辅助网格信息        | `object`                           | `--`   |
| grid.rowCount    | 辅助网格行数            | `number`                           | `--`   |
| grid.columnCount | 辅助网格列数            | `number`                           | `--`   |
| grid.color       | 辅助网格颜色            | `string`: 目前仅支持十六进制颜色值 | `--`   |

```js static
// example: 
const defaultImage = {
    url: 'http://img2.imgtn.bdimg.com/it/u=1962045236,1139336730&fm=26&gp=0.jpg',
    width: 500,
    height: 334,
    grid: {
        rowCount: 5,
        columnCount: 5,
        color: 'blue'
    }
};
```

### Label配置参数

| 参数        | 说明                                                                 | 类型        | 默认值 |
| ----------- | -------------------------------------------------------------------- | ----------- | ------ |
| key         | 标注对象标识字段                                                     | `string`    | `--`   |
| select      | 标识是否呈现选中态<br/>目前仅支持最多一个标注的 select:true 为编辑态 | `boolean`   | `--`   |
| label       | 标签名相关配置                                                       | `object`    | `--`   |
| label.name  | 标签名名称                                                           | `string`    | `--`   |
| label.style | 标签名样式                                                           | `object`    | `--`   |
| type        | 当前标注框类型，'rect' or 'polygon'                                  | `string`    | `--`   |
| texts       | 关联文本对象集合                                                     | `Text:[]`   | `--`   |
| markers     | 关联标记对象集合                                                     | `Marker:[]` | `--`   |
| points      | 标注框集合                                                           | `Point:[]`  | `--`   |
| style       | 标注框样式                                                           | `object`    | `--`   |

```js static
// example: 
const defaultLabels = [
    {
        key: '110',
        select: false,
        label: { // 标签名配置
            name: '中国', // 标签名称
            style: labelNameStyle // 标签样式
        },
        type: 'rect', // 矩形，支持'rect'， 'polygon'
        texts: [{ // 该标注对象关联的文本集合，一般业务不需要
            position: {x: 20, y: 20},
            offset: {x: 0, y: 0},
            maxWidth: 100,
            text: '中国北京',
            style: labelTextStyle
        }],
        markers: [{ // 该标注对象关联的标记集合，一般业务不需要
            position: {x: 150, y: 100},
            offset: {x: 0, y: 0},
            events: {click: (p1, p2) => {
                console.log('p1, p2', p1, p2);
            }}
        }],
        points: [ // 该标注对象坐标信息【相对于图像左上角的坐标值】
            {x: 100, y: 50},
            {x: 200, y: 50},
            {x: 200, y: 150},
            {x: 100, y: 150}
        ],
        style: labelFeatureStyle // 标注框展示样式
    }
];
```

### Text配置参数

| 参数     | 说明                       | 类型     | 默认值 |
| -------- | -------------------------- | -------- | ------ |
| position | 文本框左上角位置 {x:, y: } | `object` | `--`   |
| offset   | 文本偏移量 {x:, y: }       | `object` | `--`   |
| maxWidth | 文本框最大宽               | `number` | `--`   |
| text     | 文本框中文字               | `string` | `--`   |
| style    | 文本样式                   | `object` | `--`   |

```js static
// example: 
const defaultText = { // 该标注对象关联的文本集合，一般业务不需要
    position: {x: 20, y: 20},
    offset: {x: 0, y: 0},
    maxWidth: 100,
    text: '中国北京',
    style: labelTextStyle
};
```

### Marker配置参数

| 参数     | 说明                         | 类型     | 默认值 |
| -------- | ---------------------------- | -------- | ------ |
| src      | 标记对象图标路径             | `string` | `--`   |
| position | 标记对象左上角位置 {x:, y: } | `object` | `--`   |
| offset   | 标记对象偏移量 {x:, y: }     | `object` | `--`   |
| events   | 标记对象绑定事件             | `object` | `--`   |

```js static
// example: 
const defaultMarker = { // 该标注对象关联的标记集合，一般业务不需要
    src: '',
    position: {x: 150, y: 100},
    offset: {x: 0, y: 0},
    events: {click: (p1, p2) => {
        console.log('p1, p2', p1, p2);
    }}
};
```

### onChange: (type: string, label: any, event: object, wxy: Point) => void 配置参数

| 参数  | 说明                                                                             | 类型     |
| ----- | -------------------------------------------------------------------------------- | -------- |
| type  | changeType类型，如 'add'、'delete'、'update' 等                                  | `string` |
| label | 相应 changeType 对应的不同返回数据                                               | `any`    |
| event | event 事件对象，针对鼠标事件有效，目前仅针对 'hover'                             | `object` |
| wxy   | 针对鼠标事件有效，目前仅针对 'hover', {x: , y: }，注意：此处是基于图片中心的坐标 | `object` |

```js static
// example: 
const handleLabelChange = useCallback((operateType, label, evt, wxy) => {
    // 有些中间状态是不需要进行label重设
    if (_.includes(['updating', 'boundsChanged', 'updateReset', 'hover'], operateType)) {
        return;
    }
    // 需要进行labels变化时，才进行setBizLabels，否则中间态持续执行，如果不停的setBizLabels会造成死循环
    setBizLabels(preLabels => {
        let newLabels = _.cloneDeep(preLabels);
        // label添加
        if (operateType === 'add') {
            newLabels.push({
                key: `model-label-${_.uniqueId()}`,
                label: {
                    name: '测试',
                    style: labelNameStyle
                },
                ...label,
                style: labelFeatureStyle
            });
        }
        // label删除/更新/选中
        else if (_.includes(['delete', 'update', 'select'], operateType)) {
            const findIndex = _.findIndex(newLabels, {key: label.key});
            if (findIndex >= 0) {
                newLabels.splice(findIndex, 1);
                operateType === 'update' && newLabels.push(label);
                operateType === 'select' && newLabels.push({...label, select: true});
            }
        }
        // 【【特别注意：特别注意：特别注意】】：reset 这一步目前必须，需要将label进行直接覆盖即可【作用：所有select: false】
        else if (operateType === 'reset') {
            const formatLabels = _.map(newLabels, label => ({...label, select: false}));
            newLabels = formatLabels;
        }
        return newLabels;
    });
}, []);
```

## 参考文档

<https://react-app-common.now.baidu-int.com/#/hooks/UseLabelBox>
