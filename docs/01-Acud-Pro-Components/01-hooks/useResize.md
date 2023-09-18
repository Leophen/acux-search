---
title: useResize
---

用于监听 DOM 元素或 window 实时宽高变化的 hooks。

:::note 三种传参示例

```js
// 获取 ref={wrapRef} 的元素的宽高
const {height: refDomHeight, width: refDomWidth} = useResize(wrapRef);

// 获取 window 的宽高
const {height: windowHeight, width: windowWidth} = useResize();

// 获取 DOM 元素宽高
const {height: selectDomHeight, width: selectDomWidth} =
useResize(document.querySelector('body'));
```

:::

## 引入

```js
import {useResize} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live fff
function App() {
    let timer = null;
    const wrapRef = useRef(null);
    const {height: refDomHeight, width: refDomWidth} = useResize(wrapRef);
    const {height: windowHeight, width: windowWidth} = useResize();
    const {height: selectDomHeight, width: selectDomWidth} = useResize(document.querySelector('body'));

    const [wrapElementStyle, setWrapElementStyle] = useState({width: '100%', height: '200px'});
    const [windowSize, setWindowSize] = useState({width: 0, height: 0});
    const [refDomSize, setRefDomSize] = useState({width: 0, height: 0});
    const [selectDomSize, setSelectDomSize] = useState({width: 0, height: 0});

    useEffect(() => {
        setRefDomSize({width: refDomWidth, height: refDomHeight});
    }, [refDomHeight, refDomWidth]);

    useEffect(() => {
        setWindowSize({width: windowWidth, height: windowHeight});
    }, [windowHeight, windowWidth]);

    useEffect(() => {
        setSelectDomSize({width: selectDomWidth, height: selectDomHeight});
    }, [selectDomHeight, selectDomWidth]);

    useEffect(() => {
        timer = setTimeout(() => {
            setWrapElementStyle({width: '50%', height: '100px'});
        }, 3000);
        return () => {
            clearTimeout(timer);
        };
    }, []);

    return (
        <div ref={wrapRef} style={{...wrapElementStyle, border: '1px solid #000'}}>
            <p>
                3 秒后 DOM 元素宽高变化
            </p>
            <p>
                window：height = {windowSize.height} width = {windowSize.width}
            </p>
            <p>
                ref 绑定的 DOM 元素: height = {refDomSize.height} width = {refDomSize.width}
            </p>
            <p>
                直接获取 DOM 元素（body）: height = {selectDomSize.height} width = {selectDomSize.width}
            </p>
        </div>
    );
}
```

## API

```typescript static
type Arg = HTMLElement | React.MutableRefObject<any>;
useResize(...args: [Arg?]) : ({width: number, height: number}: object);
```
