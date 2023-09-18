---
title: Search
---

Search 搜索组件。

- 支持输入框内容变化时的回调
- 支持按下回车、搜索按钮的回调
- 支持按下清空按钮的回调

## 引入

```js
import {components} from 'baidu-acu-react-common';

const Search = components.Search;
```

## 基本用法

```jsx live fff
function App() {
    const [change, setChange] = useState();
    const [search, setSearch] = useState();

    const handleSearchChange = value => {
        setChange('Change:' + value);
    };
    const handleSearchPress = value => {
        setSearch('Search:' + value);
    };

    return (
        <>
            <div>基本用法</div><br />
            <Search
                placeholder={'请输入搜索名称'}
                onChange={handleSearchChange}
                onPressButton={handleSearchPress}
            />
            {change && <div>{change}</div>}
            {search && <div>{search}</div>}
        </>
    );
}
```

## 监听回车事件

```jsx live fff
function App() {
    const [enter, setEnter] = useState();

    const handleSeachEnter = value => {
        setEnter('Enter:' + value);
    }

    return (
        <>
            <div>监听回车事件</div><br />
            <Search
                placeholder={'请输入搜索名称'}
                onPressEnter={handleSeachEnter}
            />
            {enter && <div>{enter}</div>}
        </>
    );
}
```

## 清空默认文本

```jsx live fff
function App() {
    const [clear, setClear] = useState();

    const handleSearchClear = e => {
        setClear('cleared');
    }

    return (
        <>
            <div>清空默认文本</div><br />
            <Search
                placeholder={'请输入搜索名称'}
                value="Default value"
                onClear={handleSearchClear}
            />
            {clear && <div>{clear}</div>}
        </>
    );
}
```

## API

| 参数          | 说明                   | 类型       | 默认值         |
| ------------- | ---------------------- | ---------- | -------------- |
| placeholder   | 输入说明               | `string`   | `'请输入名称'` |
| value         | 默认值                 | `string`   | `''`           |
| onChange      | 输入框内容变化时的回调 | `function` | `--`           |
| onPressEnter  | 按下回车的回调         | `function` | `--`           |
| onPressButton | 按下搜索按钮的回调     | `function` | `--`           |
| onClear       | 按下清空按钮的回调     | `function` | `--`           |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/Search>
