---
title: Grid 栅格
---

24 栅格系统。

:::note 说明

布局的栅格化系统，我们是基于行（row）和列（col）来定义信息区块的外部框架，以保证页面的每个区域能够稳健地排布起来。下面简单介绍一下它的工作原理：

- 通过 `row` 在水平方向建立一组 `column`（简写 col）。
- 你的内容应当放置于 `col` 内，并且，只有 `col` 可以作为 `row` 的直接元素。
- 栅格系统中的列是指 1 到 24 的值来表示其跨越的范围。例如，三个等宽的列可以使用 `<Col span={8} />` 来创建。
- 如果一个 `row` 中的 `col` 总和超过 24，那么多余的 `col` 会作为一个整体另起一行排列。

我们的栅格化系统基于 Flex 布局，允许子元素在父节点内的水平对齐方式 - 居左、居中、居右、等宽排列、分散排列。子元素与子元素之间，支持顶部对齐、垂直居中对齐、底部对齐的方式。同时，支持使用 order 来定义元素的排列顺序。

布局是基于 24 栅格来定义每一个『盒子』的宽度，但不拘泥于栅格。

:::

## 引入

```js
import {Row, Col} from 'acud';
```

## 基本用法

使用单一的一组 `Row` 和 `Col` 栅格组件，就可以创建一个基本的栅格系统，所有列（Col）必须放在 `Row` 内。

```jsx live
function App() {
    const demoData = [
        Array(24).fill(1),
        Array(12).fill(2),
        Array(8).fill(3),
        Array(6).fill(4),
        Array(4).fill(6),
        Array(3).fill(8),
        Array(2).fill(12),
        Array(1).fill(24)
    ];

    return (
        <div className="acux-demo">
            {/* 直接使用 */}
            <Row>
                <Col span={8}>
                    <div>Col-1</div>
                </Col>
                <Col span={8}>
                    <div>Col-2</div>
                </Col>
                <Col span={8}>
                    <div>Col-3</div>
                </Col>
            </Row>

            {/* 遍历使用 */}
            {demoData.map((grid, i) => (
                <Row key={i}>
                    {grid.map((item, j) => (
                        <Col span={item} key={j}>
                            <div>{item}</div>
                        </Col>
                    ))}
                </Row>
            ))}

            {/* span 总和超出换行 */}
            <Row>
                <Col span={8}>
                    <div>span8</div>
                </Col>
                <Col span={8}>
                    <div>span8</div>
                </Col>
                <Col span={12}>
                    <div>span12</div>
                </Col>
            </Row>
        </div>
    );
}
```

## 区块间隔

栅格常常需要和间隔进行配合，你可以使用 `Row` 的 `gutter` 属性，我们推荐使用 `(16+8n)px` 作为栅格间隔(n 是自然数)。

如果要支持响应式，可以写成 `{ xs: 8, sm: 16, md: 24, lg: 32 }`。

如果需要垂直间距，可以写成数组形式 `[水平间距, 垂直间距]` `[16, { xs: 8, sm: 16, md: 24, lg: 32 }]`。

```jsx live
<div className="acux-demo">
    <Row gutter={0}>
        <Col span={6}>
            <div>Col-1</div>
        </Col>
        <Col span={6}>
            <div>Col-2</div>
        </Col>
        <Col span={6}>
            <div>Col-3</div>
        </Col>
        <Col span={6}>
            <div>Col-4</div>
        </Col>
    </Row>

    <Row gutter={16}>
        <Col span={6}>
            <div>Col-1</div>
        </Col>
        <Col span={6}>
            <div>Col-2</div>
        </Col>
        <Col span={6}>
            <div>Col-3</div>
        </Col>
        <Col span={6}>
            <div>Col-4</div>
        </Col>
    </Row>

    <Row gutter={{xs: 8, sm: 16, md: 24, lg: 32}}>
        <Col span={6}>
            <div>Col-1</div>
        </Col>
        <Col span={6}>
            <div>Col-2</div>
        </Col>
        <Col span={6}>
            <div>Col-3</div>
        </Col>
        <Col span={6}>
            <div>Col-4</div>
        </Col>
    </Row>
</div>
```

## 向右偏移

使用 `offset` 可以将列向右侧偏。例如，`offset={4}` 将元素向右侧偏移了 4 个列（column）的宽度。

```jsx live
<div className="acux-demo">
    <Row>
        <Col span={4}>
            <div>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>

    <Row>
        <Col span={4}>
            <div>Col-1</div>
        </Col>
        <Col span={4} offset={2}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>

    <Row gutter={16}>
        <Col span={4}>
            <div>Col-1</div>
        </Col>
        <Col span={4} offset={2}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>
</div>
```

## 水平排列方式

子元素根据不同的值 `start`,`center`,`end`,`space-between`,`space-around`，分别定义其在父节点里面的排版方式。

```jsx live
<div className="acux-demo">
    <h4>start</h4>
    <Row justify="start">
        <Col span={4}>
            <div>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>

    <h4>center</h4>
    <Row justify="center">
        <Col span={4}>
            <div>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>

    <h4>end</h4>
    <Row justify="end">
        <Col span={4}>
            <div>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>

    <h4>space-between</h4>
    <Row justify="space-between">
        <Col span={4}>
            <div>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>

    <h4>space-around</h4>
    <Row justify="space-around">
        <Col span={4}>
            <div>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>
</div>
```

## 垂直排列方式

子元素垂直对齐。

```jsx live
<div className="acux-demo">
    <h4>top</h4>
    <Row align="top">
        <Col span={4}>
            <div style={{ height: '80px' }}>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div style={{ height: '60px' }}>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>

    <h4>middle</h4>
    <Row align="middle">
        <Col span={4}>
            <div style={{ height: '80px' }}>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div style={{ height: '60px' }}>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>

    <h4>bottom</h4>
    <Row align="bottom">
        <Col span={4}>
            <div style={{ height: '80px' }}>Col-1</div>
        </Col>
        <Col span={4}>
            <div>Col-2</div>
        </Col>
        <Col span={4}>
            <div style={{ height: '60px' }}>Col-3</div>
        </Col>
        <Col span={4}>
            <div>Col-4</div>
        </Col>
    </Row>
</div>
```

## 自定义排序

通过 `order` 来改变元素的排序。

```jsx live
<div className="acux-demo">
    <Row gutter={10}>
        <Col span={2}>
            <div>1</div>
        </Col>
        <Col span={2}>
            <div>2</div>
        </Col>
        <Col span={2} order={4}>
            <div>3</div>
        </Col>
        <Col span={2} order={3}>
            <div>4</div>
        </Col>
        <Col span={2} order={3}>
            <div>5</div>
        </Col>
        <Col span={2} order={2}>
            <div>6</div>
        </Col>
        <Col span={2} order={1}>
            <div>7</div>
        </Col>
        <Col span={2} order={0}>
            <div>8</div>
        </Col>
        <Col span={2}>
            <div>9</div>
        </Col>
        <Col span={2}>
            <div>10</div>
        </Col>
    </Row>
</div>
```

## Flex 填充

Col 提供 `flex` 属性以支持填充。

```jsx live
<div className="acux-demo">
    <h4>Percentage columns</h4>
    <Row>
        <Col flex={2}>
            <div>2 / 5</div>
        </Col>
        <Col flex={3}>
            <div>3 / 5</div>
        </Col>
    </Row>

    <h4>Fill rest</h4>
    <Row>
        <Col flex="100px">
            <div>100px</div>
        </Col>
        <Col flex="auto">
            <div>Fill Rest</div>
        </Col>
    </Row>

    <h4>Raw flex style</h4>
    <Row>
        <Col flex="1 1 200px">
            <div>1 1 200px</div>
        </Col>
        <Col flex="0 1 300px">
            <div>0 1 300px</div>
        </Col>
    </Row>

    <Row wrap={false}>
        <Col flex="none">
            <div>none</div>
        </Col>
        <Col flex="auto">
            <div>auto with no-wrap</div>
        </Col>
    </Row>
</div>
```

## 响应式布局

参照 Bootstrap 的 [响应式设计](https://getbootstrap.com/docs/3.4/css/)，预设六个响应尺寸：`xs` `sm` `md` `lg` `xl` `xxl`

```jsx live
<div className="acux-demo">
    <Row>
        <Col xs={2} sm={4} md={6} lg={8} xl={10}>
          <div>Col</div>
        </Col>
        <Col xs={20} sm={16} md={12} lg={8} xl={4}>
          <div>Col</div>
        </Col>
        <Col xs={2} sm={4} md={6} lg={8} xl={10}>
          <div>Col</div>
        </Col>
    </Row>
</div>
```

`span` `pull` `push` `offset` `order` 属性可以通过内嵌到 `xs` `sm` `md` `lg` `xl` `xxl` 属性中来使用。

其中 `xs={6}` 相当于 `xs={{ span: 6 }}`

示例：

```jsx live
<div className="acux-demo">
    <Row>
        <Col xs={{span: 5, offset: 1}} lg={{span: 6, offset: 2}}>
          <div>Col</div>
        </Col>
        <Col xs={{span: 11, offset: 1}} lg={{span: 6, offset: 2}}>
          <div>Col</div>
        </Col>
        <Col xs={{span: 5, offset: 1}} lg={{span: 6, offset: 2}}>
          <div>Col</div>
        </Col>
    </Row>
</div>
```

## 个性化布局

使用 `useBreakpoint` Hook 个性化布局。

```jsx
function App() {
    const {useBreakpoint} = Grid;

    function UseBreakpointDemo() {
        const screens = useBreakpoint();
        return (
            <>
                Current break point:{' '}
                {Object.entries(screens)
                    .filter(screen => !!screen[1])
                    .map(screen => (
                        <span
                            style={{
                                padding: '4px 6px',
                                border: '1px solid #ccc',
                                color: 'blue',
                                marginRight: '5px'
                            }
                            }
                            key={screen[0]}
                        >
                            {screen[0]}
                        </span>
                    ))}
            </>
        );
    }

    return (
        <UseBreakpointDemo />
    );
}
```

如果 acud 的布局组件若不能满足需求，也可以直接使用社区的优秀布局组件：

- [react-flexbox-grid](http://roylee0704.github.io/react-flexbox-grid/)
- [react-blocks](https://github.com/whoisandy/react-blocks/)

## API

### Row

| 成员    | 说明                                                                                                                                   | 类型                                                      | 默认值  |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- | ------- |
| align   | 垂直对齐方式                                                                                                                           | `top`〡`middle`〡`bottom`                                 | `top`   |
| gutter  | 栅格间隔，可以写成像素值或支持响应式的对象写法来设置水平间隔 { xs: 8, sm: 16, md: 24}。或者使用数组形式同时设置 `[水平间距, 垂直间距]` | `number`〡`object`〡`array`                               | `0`     |
| justify | 水平排列方式                                                                                                                           | `start`〡`end`〡`center`〡`space-around`〡`space-between` | `start` |
| wrap    | 是否自动换行                                                                                                                           | `boolean`                                                 | `true`  |

### Col

| 成员   | 说明                                                           | 类型               | 默认值 |
| ------ | -------------------------------------------------------------- | ------------------ | ------ |
| flex   | flex 布局属性                                                  | `string`〡`number` | `--`   |
| offset | 栅格左侧的间隔格数，间隔内不可以有栅格                         | `number`           | `0`    |
| order  | 栅格顺序                                                       | `number`           | `0`    |
| pull   | 栅格向左移动格数                                               | `number`           | `0`    |
| push   | 栅格向右移动格数                                               | `number`           | `0`    |
| span   | 栅格占位格数，为 0 时相当于 `display: none`                    | `number`           | `--`   |
| xs     | `屏幕 < 576px` 响应式栅格，可为栅格数或一个包含其他属性的对象  | `number`〡`object` | `--`   |
| sm     | `屏幕 ≥ 576px` 响应式栅格，可为栅格数或一个包含其他属性的对象  | `number`〡`object` | `--`   |
| md     | `屏幕 ≥ 768px` 响应式栅格，可为栅格数或一个包含其他属性的对象  | `number`〡`object` | `--`   |
| lg     | `屏幕 ≥ 992px` 响应式栅格，可为栅格数或一个包含其他属性的对象  | `number`〡`object` | `--`   |
| xl     | `屏幕 ≥ 1200px` 响应式栅格，可为栅格数或一个包含其他属性的对象 | `number`〡`object` | `--`   |
| xxl    | `屏幕 ≥ 1600px` 响应式栅格，可为栅格数或一个包含其他属性的对象 | `number`〡`object` | `--`   |

响应式栅格的断点扩展自 [BootStrap 4 的规则](https://getbootstrap.com/docs/4.0/layout/overview/#responsive-breakpoints)（不包含链接里 `occasionally` 的部分）
