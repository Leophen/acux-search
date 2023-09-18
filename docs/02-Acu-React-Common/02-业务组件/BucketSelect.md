---
title: BucketSelect
---

BOS 路径选择组件。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const {BucketSelect} = components;
```

## 基本用法

```jsx live fff
function App() {
    const api = {
        bosBucketList: '/api/bos/bucket/list',
        bosObjectFolder: '/api/bos/object/folder'
    }

    function handleBucketChange(value) {
        console.log(value);
    }

    return (
        <BucketSelect
            viewType="folder"
            bucketListApi={api.bosBucketList}
            folderListApi={api.bosObjectFolder}
            locations={['bj']}
            urlPrefix="bos:/"
            layerWidth={300}
            onChange={handleBucketChange}
        />
    );
}
```

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E4%B8%9A%E5%8A%A1%E7%BB%84%E4%BB%B6/BucketSelect>
