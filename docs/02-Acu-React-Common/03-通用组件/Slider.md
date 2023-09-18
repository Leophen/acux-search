---
title: Slider
---

滑块组件。

- 支持每次滑动个数的设定
- 支持整页滑动

## 引入

```js
import {components} from 'baidu-acu-react-common';

const Slider = components.Slider;
```

## 基本用法

```jsx
<div>
    <div>每次滚动一条</div><br />
    <Slider itemWidth={200} height={100} step={1} isPageTurn={false}>
        <div key="slider-demo1-1">
            <img width="200" height="80" src="http://cyberplayer.bcelive.com/resource/react-common/slider.png" />
        </div>
        <div key="slider-demo1-2">
            <img width="200" height="80" src="http://cyberplayer.bcelive.com/resource/react-common/slider.png" />
        </div>
        <div key="slider-demo1-3">
            <img width="200" height="80" src="http://cyberplayer.bcelive.com/resource/react-common/slider.png" />
        </div>
        <div key="slider-demo1-4">
            <img width="200" height="80" src="http://cyberplayer.bcelive.com/resource/react-common/slider.png" />
        </div>
        <div key="slider-demo1-5">
            <img width="200" height="80" src="http://cyberplayer.bcelive.com/resource/react-common/slider.png" />
        </div>
        <div key="slider-demo1-6">
            <img width="200" height="80" src="http://cyberplayer.bcelive.com/resource/react-common/slider.png" />
        </div>
        <div key="slider-demo1-7">
            <img width="200" height="80" src="http://cyberplayer.bcelive.com/resource/react-common/slider.png" />
        </div>
        <div key="slider-demo1-8">
            <img width="200" height="80" src="http://cyberplayer.bcelive.com/resource/react-common/slider.png" />
        </div>
    </Slider>
</div>
```

## 整页翻转

```jsx
<div>
    <div>整页翻转</div><br />
    <Slider itemWidth={200} height={100} isPageTurn>
        <div key="slider-demo2-1">1</div>
        <div key="slider-demo2-2">2</div>
        <div key="slider-demo2-3">3</div>
        <div key="slider-demo2-4">4</div>
        <div key="slider-demo2-5">5</div>
        <div key="slider-demo2-6">6</div>
        <div key="slider-demo2-7">7</div>
        <div key="slider-demo2-8">8</div>
    </Slider>
</div>
```

## API

| 参数       | 说明             | 类型      | 默认值  |
| ---------- | ---------------- | --------- | ------- |
| itemWidth  | 每一项内容的宽度 | `number`  | `100`   |
| height     | 滑动组件的高     | `number`  | `100`   |
| step       | 滑动个数         | `number`  | `1`     |
| isPageTurn | 是否整页滑动     | `boolean` | `false` |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/Slider>
