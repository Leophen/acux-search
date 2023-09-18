---
title: Cyberplayer
---

用于播放视频使用的 react 组件，支持常见播放格式（mp4/flv/hls）视频的播放。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const Cyberplayer = components.Cyberplayer;
```

## 基本用法

```jsx live fff
<Cyberplayer
    autostart={false}
    width={560}
    height={400}
    file="http://gcqq450f71eywn6bv7u.exp.bcevod.com/mda-hbqagik5sfq1jsai/mda-hbqagik5sfq1jsai.mp4"
/>
```

## API

| 参数         | 说明                                      | 类型               | 默认值            |
| ------------ | ----------------------------------------- | ------------------ | ----------------- |
| containerId  | domId                                     | `string`           | `playerContainer` |
| file         | 播放地址，支持mp4、hls、flv等常用视频格式 | `string`           | `无`              |
| thumbnailUrl | 封面图                                    | `string`           | `无`              |
| autostart    | 是否自动播放                              | `boolean`          | `true`            |
| volume       | 音量                                      | `number`           | `100`             |
| width        | 宽度                                      | `number/string(%)` | `680`             |
| height       | 高度                                      | `number/string(%)` | `448`             |
| onTime       | 播放时的实时回调                          | `function`         |                   |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/Cyberplayer>
