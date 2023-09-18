---
title: ErrorBoundary
---

错误处理组件。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const ErrorBoundary = components.ErrorBoundary;
```

## 基本用法

```jsx live fff
function App() {
    const MyComponent = () => {
        return <div>MyComponent</div>;
    };

    return (
        <ErrorBoundary>
            <MyComponent />
        </ErrorBoundary>
    );
}
```

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/ErrorBoundary>
