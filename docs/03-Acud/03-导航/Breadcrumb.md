---
title: Breadcrumb 面包屑
---

面包屑是辅助导航模式，用于识别页面在层次结构内的位置，并根据需要向上返回。

## 引入

```js
import {Breadcrumb} from 'acud';
```

## 基本用法

```jsx live fffx
<Breadcrumb>
    <Breadcrumb.Item>Home</Breadcrumb.Item>
    <Breadcrumb.Item>
        <a href="">Application Center</a>
    </Breadcrumb.Item>
    <Breadcrumb.Item>
        <a href="">Application List</a>
    </Breadcrumb.Item>
    <Breadcrumb.Item>An Application</Breadcrumb.Item>
</Breadcrumb>
```

## 自定义分隔符

使用 separator="/" 可以自定义分隔符。

```jsx live fffx
<Breadcrumb separator="/">
    <Breadcrumb.Item>Home</Breadcrumb.Item>
    <Breadcrumb.Item href="">Application Center</Breadcrumb.Item>
    <Breadcrumb.Item href="">Application List</Breadcrumb.Item>
    <Breadcrumb.Item>An Application</Breadcrumb.Item>
</Breadcrumb>
```

## 带有图标的

图标放在文字前面。

```jsx live fff
<Breadcrumb>
    <Breadcrumb.Item href="">
        <OutlinedHome />
    </Breadcrumb.Item>
    <Breadcrumb.Item href="">
        <OutlinedUser />
        <span>Application List</span>
    </Breadcrumb.Item>
    <Breadcrumb.Item>Application</Breadcrumb.Item>
</Breadcrumb>
```

## 带下拉菜单的

面包屑支持下拉菜单。

```jsx live fff
function App() {
    const menu = (
        <Menu>
            <Menu.Item>
                <a target="_blank" rel="noopener noreferrer" href="#">
              General
                </a>
            </Menu.Item>
            <Menu.Item>
                <a target="_blank" rel="noopener noreferrer" href="#">
              Layout
                </a>
            </Menu.Item>
            <Menu.Item>
                <a target="_blank" rel="noopener noreferrer" href="#">
              Navigation
                </a>
            </Menu.Item>
        </Menu>
    );

    return (
        <Breadcrumb>
            <Breadcrumb.Item>ACUD</Breadcrumb.Item>
            <Breadcrumb.Item>
                <a href="">Component</a>
            </Breadcrumb.Item>
            <Breadcrumb.Item overlay={menu}>
                <a href="">General</a>
            </Breadcrumb.Item>
            <Breadcrumb.Item>Button</Breadcrumb.Item>
        </Breadcrumb>
    );
}
```

## 参考文档

<https://acud.now.baidu-int.com/components/breadcrumb>
