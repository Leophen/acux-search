---
title: Button 按钮
---

按钮用于触发一个即使操作的命令控件。

## 引入

```js
import {Button} from 'acud';
```

## 基本用法

按钮分为 主要按钮、加强按钮、普通按钮、文字按钮和强调按钮五种：

- 主要按钮：一个⻚面内主要按钮使用数量建议 1-2 个，规范 1 个。目前主要按钮主要用于新建/购买入口、弹框的“确定”操作等。
- 加强按钮：在按钮分级较多的场景下使用，重要性介于“主要按钮”和“普通按钮”之间。
- 普通按钮：普通按钮颜色⻛格较弱，不会打扰用户，可在一个⻚面或对话框内放置多个普通按钮。
- ⽂字按钮：文字按钮，是重要性最低的按钮，常用于操作频率较低的辅助型命令。
- 强调按钮：当⽤用户需要进⾏⼀些特别重要，执⾏错误后会造成重⼤损失的命令，可使⽤强调按钮，如危险删除。

```jsx live fffx
<div className="acux-demo-row">
    <Button>default</Button>
    <Button type="primary">primary</Button>
    <Button type="enhance">enhance</Button>
    <Button type="highlight">highlight</Button>
    <Button type="text">文字按钮</Button>
</div>
```

## 禁用状态

可以使用 `disabled` 属性来定义按钮是否被禁用，该属性接受一个 `Boolean` 类型的值。

```jsx live fffx
<div className="acux-demo-row">
    <Button disabled>default</Button>
    <Button type="primary" disabled>primary</Button>
    <Button type="enhance" disabled>enhance</Button>
    <Button type="highlight" disabled>highlight</Button>
    <Button type="text" disabled>文字按钮</Button>
</div>
```

## 加载状态

`loading`: 加载中，该属性接受一个 `Boolean` 类型的值。

```jsx live fffx
<div className="acux-demo-row">
    <Button loading>default</Button>
    <Button type="primary" loading>primary</Button>
    <Button type="enhance" loading>enhance</Button>
    <Button type="highlight" loading>highlight</Button>
    <Button type="text" loading>文字按钮</Button>
</div>
```

## 不同尺寸

提供 `small`、`middle`（默认）、`large` 三种尺寸的按钮。

```jsx live fffx
<div className="acux-demo-row">
    <Button size="small">小按钮</Button>
    <Button size="middle">中按钮</Button>
    <Button size="large">大按钮</Button>
</div>
```

## 带图标按钮

可以使用 `icon` 属性来添加按钮图标。

```jsx live fffx
<div className="acux-demo-row">
    <Button icon={<OutlinedPlus />}>default</Button>
    <Button type="primary" icon={<OutlinedPlus />}>primary</Button>
    <Button type="enhance" icon={<OutlinedPlus />}>enhance</Button>
    <Button type="highlight" icon={<OutlinedPlus />}>highlight</Button>
    <Button type="text" icon={<OutlinedPlus />}>文字按钮</Button>
</div>
```

## 按钮组

若某一区域按钮过多或⻚面空间有限只能放置少量按钮时，可使用按钮组，将次要操作进行收折，突出主要操作，并保持⻚面的简洁，节省空间 建议一个区域内只保留一个按钮组。

```jsx live fffx
function App() {
    const menuEl = (
        <Menu>
            <Menu.Item key="1">1st item</Menu.Item>
            <Menu.Item key="2">2nd item</Menu.Item>
            <Menu.Item key="3">3rd item</Menu.Item>
        </Menu>
    )

    return (
        <div className="acux-demo-row">
            <Dropdown.Button overlay={menuEl}>
                Dropdown
            </Dropdown.Button>
            <Dropdown.Button overlay={menuEl} type="primary">
                Dropdown
            </Dropdown.Button>
            <Dropdown.Button overlay={menuEl} type="enhance">
                Dropdown
            </Dropdown.Button>
            <Dropdown.Button overlay={menuEl} type="highlight">
                Dropdown
            </Dropdown.Button>
            <Dropdown.Button overlay={menuEl} type="text">
                Dropdown
            </Dropdown.Button>
            <Dropdown.Button overlay={menuEl} disabled>
                Dropdown
            </Dropdown.Button>
        </div>
    );
}
```

## API

通过设置 Button 的属性来产生不同的按钮样式，推荐顺序为：`type` -> `size` -> `loading` -> `disabled`。

按钮的属性说明如下：

| 属性     | 说明                                                                                                                                 | 类型                                                         | 默认值    |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ | --------- |
| block    | 将按钮宽度调整为其父宽度的选项                                                                                                       | `boolean`                                                    | `false`   |
| disabled | 按钮失效状态                                                                                                                         | `boolean`                                                    | `false`   |
| href     | 点击跳转的地址，指定此属性 button 的行为和 a 链接一致                                                                                | `string`                                                     | `--`      |
| htmlType | 设置 `button` 原生的 `type` 值，可选值请参考 [HTML 标准](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#attr-type) | `string`                                                     | `button`  |
| icon     | 设置按钮的图标组件                                                                                                                   | `ReactNode`                                                  | `--`      |
| loading  | 设置按钮载入状态                                                                                                                     | `boolean`                                                    | `false`   |
| size     | 设置按钮大小                                                                                                                         | `large` \| `middle` \| `small`                               | `middle`  |
| target   | 相当于 a 链接的 target 属性，href 存在时生效                                                                                         | `string`                                                     | `--`      |
| type     | 设置按钮类型                                                                                                                         | `primary` \| `text` \| `highlight` \| `enhance` \| `default` | `default` |
| onClick  | 点击按钮时的回调                                                                                                                     | `(event) => void`                                            | `--`      |
