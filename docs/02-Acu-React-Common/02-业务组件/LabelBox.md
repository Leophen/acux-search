---
title: LabelBox
---

指标图像平移缩放&标注展示&在线标注等功能。(注：使用坐标系原点为容器中心点(0, 0))

- 支持图像浏览【平移缩放等】
- 支持标注框及对应标签名展示
- 支持在线标注 & 标注编辑

## 引入

```js
import {components} from 'baidu-acu-react-common';

const {LabelBox} = components;
```

## 使用方法

```jsx
import {components} from 'baidu-acu-react-common';

const {LabelBox} = components;

const Image = {
    url: 'http://img2.imgtn.bdimg.com/it/u=1962045236,1139336730&fm=26&gp=0.jpg',
    width: 500,
    height: 334
};
const Labels = [{
    key: 'key',
    text: '中国',
    points: [{
        x: -100,
        y: 100
    },
    {
        x: 100,
        y: 100
    },
    {
        x: 100,
        y: -100
    },
    {
        x: -100,
        y: -100
    }]
}];

handleAdd = (type, points) => {
    const newLabels = [...this.state.labels];
    newLabels.push({
        key: new Date().getTime() + '',
        text: 'ceshi',
        points
    });
    this.setState({labels: newLabels});
}
handleRemove = label => {
    const newLabels = [...this.state.labels];
    const findIndex = _.findIndex(newLabels, {key: label.key});
    if (findIndex > -1) {
        newLabels.splice(findIndex, 1);
    }
    this.setState({labels: newLabels});
}
handleUpdate = label => {
    const newLabels = _.cloneDeep(this.state.labels);
    const findIndex = _.findIndex(newLabels, {key: label.key});
    if (findIndex > -1) {
        newLabels.splice(findIndex, 1);
        newLabels.push(label);
    }
    this.setState({labels: newLabels});
}

render() {
    const {labels} = this.state;
    return (
        <LabelBox
            wrapClassName="label-ocr-container"
            image={Image}
            labels={labels}
            mode="drawRect"
            onAdd={this.handleAdd}
            onRemove={this.handleRemove}
            onUpdate={this.handleUpdate}
        />
    );
}

```

### 代码演示

```jsx
const Image = {
    url: 'http://img2.imgtn.bdimg.com/it/u=1962045236,1139336730&fm=26&gp=0.jpg',
    width: 500,
    height: 334,
    grid: {
       rowCount: 5,
       columnCount: 5,
       color: 'blue' 
    }
};

class Label extends React.Component {
    constructor(props) {
        super(props);
        this.gdboxRef = React.createRef();
        this.gdboxRef2 = React.createRef();
        this.state = {
            labels: [{
                key: '110',
                label: {
                    name: '中国',
                    style: {fontColor: '#FFFFFF', fontSize: 12, bgColor: '#1890FF'}
                },
                type: 'rect',
                texts: [],
                markers: [{
                    position: {x: 0, y: 0},
                    offset: {x: 0, y: 0},
                    events: {click: (p1, p2) => {
                        console.log('p1, p2', p1, p2);
                    }}
                }],
                points: [
                    {x: 0, y: 50},
                    {x: 100, y: 50},
                    {x: 100, y: 150},
                    {x: 0, y: 150}
                ],
                style: {strokeColor: '#0000FF', fillColor: '#FF0000', opacity: 0.5}
            }],
            rectLabels: [],
            polygonLabels: []
        }
    }

    handleOnChange(graphType, operateType, label) {
        let newLabels = [...this.state[`${graphType}Labels`]];
        // label添加
        if (operateType === 'add') {
            newLabels.push({
                key: new Date().getTime() + '',
                label: {
                    name: 'ceshi',
                    style: {fontColor: '#FFFFFF', fontSize: 12, bgColor: '#1890FF'}
                },
                ...label,
                style: {strokeColor: '#0000FF', fillColor: '#FF0000', opacity: 0.5}
            });
        }
        // label删除/更新/选中
        else if (operateType === 'delete' || operateType === 'update' || operateType === 'select') {
            const findIndex = _.findIndex(newLabels, {key: label.key});
            if (findIndex > -1) {
                newLabels.splice(findIndex, 1);
                operateType === 'update' && newLabels.push(label);
                operateType === 'select' && newLabels.push({...label, select: true});
            }
        }
        // 浏览范围变化
        else if (operateType === 'boundsChanged') {
            console.log('boundsChanged');
        }
        // label处于编辑中...
        else if (operateType === 'updating') {
            console.log('updating', label);
            const currentGDboxRef = graphType === 'rect' ? this.gdboxRef : this.gdboxRef2;
            const screenPoints = currentGDboxRef.current.worldToScreen(label.points);
            console.log('screenPoints', screenPoints);
        }
        // 更新完成后内部filter不通过，则会进行updateReset重置
        else if (operateType === 'updateReset') {
            console.log('updateReset', label);
        }
        // 特别注意：reset 这一步目前必须，需要将label进行直接覆盖即可【作用：所有select: false】
        else if (operateType === 'reset') {
            newLabels = label;
        }
        this.setState({[`${graphType}Labels`]: newLabels});
    }

    render() {
        const {labels = [], rectLabels, polygonLabels} = this.state;
        return (
            <div style={{overflow: 'hidden'}}>
                <div style={{float: 'left', marginLeft: '10px', marginTop: '10px'}}>
                    <div>标注组件【预览：图片】</div>
                    <LabelBox.LabelBox
                        wrapClassName="label-ocr-container"
                        container={{width: 440, height: 300}}
                        image={Image}
                        labels={[]}
                        mode="pan"
                    />
                </div>
                <div style={{float: 'left', marginLeft: '10px', marginTop: '10px'}}>
                    <div>标注组件【预览：图片&标注】</div>
                    <LabelBox.LabelBox
                        wrapClassName="label-ocr-container2"
                        container={{width: 440, height: 300}}
                        image={Image}
                        labels={labels}
                        mode="pan"
                    />
                </div>
                <div style={{float: 'left', marginLeft: '10px', marginTop: '10px'}}>
                    <div>标注组件【编辑：矩形（绘制、删除、修改）】</div>
                    <LabelBox.LabelBox
                        ref={this.gdboxRef}
                        wrapClassName="label-ocr-container3"
                        container={{width: 440, height: 300}}
                        image={Image}
                        labels={rectLabels}
                        mode="drawRect"
                        onChange={this.handleOnChange.bind(this, 'rect')}
                    />
                </div>
                <div style={{float: 'left', marginLeft: '10px', marginTop: '10px'}}>
                    <div>标注组件【编辑：多边形（绘制、删除、修改）】</div>
                    <LabelBox.LabelBox
                        ref={this.gdboxRef2}
                        wrapClassName="label-ocr-container4"
                        container={{width: 440, height: 300}}
                        image={Image}
                        labels={polygonLabels}
                        mode="drawPolygon"
                        eagleMap={{
                            container: 'eaglemap',
                            grid: {
                                rowCount: 5,
                                columnCount: 5,
                                color: 'blue'
                            },
                            size: {
                                width: 300,
                                height: 150
                            }
                        }}
                        onChange={this.handleOnChange.bind(this, 'polygon')}
                    />
                </div>
                <div id="eaglemap"></div>
            </div>
        );
    }
}
<Label />
```

```jsx
<LabelBox.LabelImageView
    image={{
        url: 'http://img2.imgtn.bdimg.com/it/u=1962045236,1139336730&fm=26&gp=0.jpg',
        width: 500,
        height: 334
    }}
    container={{width: 900, height: 500}}
    labels={[{
        text: '试试',
        location: {
            top: 100,
            left: 100,
            width: 200,
            height: 200
        }
    }]}
/>
```

## Props

| 参数          | 说明                                                                      | 类型      | 默认值 |
| ------------- | ------------------------------------------------------------------------- | --------- | ------ |
| wrapClassName | 外层包裹class                                                             | `string`  | `--`   |
| image         | 图像信息                                                                  | `Image`   | `--`   |
| labels        | 标注框列表                                                                | `Label[]` | `--`   |
| coord         | 坐标系基准-默认会首先判断是否存在image{width:,height:}['image', 'center'] | `string`  | `--`   |
| drawStyle     | 绘制过程样式，如{opacity: .4, fillColor: '#f00', ...}                     | `object`  | `--`   |
| mode          | 当前操作模式['pan', 'drawRect']                                           | `string`  | `--`   |

onRef(ref)：初始化完成返回当前实例对象：可调用zoomIn、zoomOut实现放大缩小

onAdd(points: Point[])：标注绘制完成

onRemove(Label): 标注删除完成

onUpdate(Label): 标注更新完成

## Image

| 参数   | 说明     | 类型     | 默认值 |
| ------ | -------- | -------- | ------ |
| url    | 图片地址 | `string` | `--`   |
| width  | 图片宽度 | `number` | `--`   |
| height | 图片高度 | `number` | `--`   |

## Label

| 参数      | 说明                                                | 类型             | 默认值 |
| --------- | --------------------------------------------------- | ---------------- | ------ |
| key       | 标注框唯一标识                                      | `string〡number` | `--`   |
| text      | 名称                                                | `string`         | `--`   |
| points    | 坐标集合                                            | `Point[]`        | `--`   |
| style     | 标注框样式，如{opacity: .4, fillColor: '#f00', ...} | `object`         | `--`   |
| textStyle | 标注框样式，如{fontSize: 12, ...}                   | `object`         | `--`   |

## Point

| 参数 | 说明   | 类型     | 默认值 |
| ---- | ------ | -------- | ------ |
| x    | 横坐标 | `number` | `--`   |
| y    | 纵坐标 | `number` | `--`   |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E4%B8%9A%E5%8A%A1%E7%BB%84%E4%BB%B6/LabelBox>
