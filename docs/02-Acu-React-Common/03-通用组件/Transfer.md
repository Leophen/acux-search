---
title: Transfer
---

穿梭组件。

- 支持搜索框过滤
- 支持单选删除/全选清空
- 声明 selectedKeys 为完全受控，记得在 onSelectChange 中更新 state

## 引入

```jsx
import {components} from 'baidu-acu-react-common';

const Transfer = components.Transfer;
```

## 基本用法

```jsx
const DATASOURCE =  [
    {
        key: '0-0',
        title: '0-0'
    }, {
        key: 'a组',
        title: 'a组',
        children: [{
            key: '0-1-0',
            title: '0-1-0'
        }, {
            key: '0-1-1',
            title: '0-1-1'
        }],
    },
    {
        key: '0-2',
        title: '0-2'
    },
    {
        key: '0-3',
        title: '0-3'
    },
    {
        key: 'b组',
        title: 'b组',
        children: [{
            key: '0-4-0',
            title: '0-4-0'
        }, {
            key: '0-4-1',
            title: '0-4-1'
        }],
    }
];

function handleSearch(value) {
    console.log('search', value);
}

function onSelectChange(value) {
    console.log('selected', value);
    setState({selectedKeys: value});
}

initialState = {
    selectedKeys: []
};

function initSelectedKeys() {
    setState({selectedKeys: ['0-2']});
}

<div>
    <div>分组层级穿梭框（取值只包含叶子节点）</div><br />
    <button type="button" onClick={initSelectedKeys}>初始化选中项</button><br /><br />
    <Transfer
        type="tree"
        treeType="group"
        dataSource={DATASOURCE}
        showSearch
        showResultSearch
        selectedKeys={state.selectedKeys}
        onSearch={handleSearch}
        onSelectChange={onSelectChange}
        render={item => item.title}
    />
</div>
```

## 穿梭框

```jsx
const DATASOURCE = [
    {title: 'test1', key: 'a'},
    {title: 'test2', key: 'b', disabled: true},
    {title: 'test3', key: 'c', disabled: true},
    {title: 'test4', key: 'd'},
    {title: 'test5', key: 'e'},
    {title: 'test6', key: 'f'},
    {title: 'test7', key: 'g', disabled: true},
    {title: 'test8', key: 'h'},
    {title: 'test9', key: 'i'},
    {title: 'test0', key: 'j', disabled: true},
    {title: 'test11', key: '11'},
    {title: 'test12', key: '12'},
    {title: 'test13', key: '13'},
];

function handleSearch(value) {
    console.log('search', value);
}

function onSelectChange(value) {
    console.log('selected', value);
    setState({selectedKeys: value});
}

function renderItem(item) {
    const customLabel = (
        <span className="custom-item">
            {item.title} - {item.key}
        </span>
    );

    return {
        label: customLabel, // for displayed item
        value: item.title   // for title and filter matching
    };
};

function filterOption(filterText, item) {
    const curTitle = `${item.title} - ${item.key}`;
    return curTitle.indexOf(filterText) >= 0;
}

initialState = {
    selectedKeys: ['a', 'b']
};

<div>
 <div>穿梭框</div><br />
    <Transfer
        dataSource={DATASOURCE}
        selectedKeys={state.selectedKeys}
        showSearch
        showResultSearch
        onSearch={handleSearch}
        onSelectChange={onSelectChange}
        render={item => item.title}
        // render={renderItem}
        // filterOption={filterOption}
    />
</div>
```

## 树形穿梭框

```jsx
const DATASOURCE =  [
    {
        key: '0-0',
        title: '0-0'
    }, {
        key: '0-1',
        title: '0-1',
        children: [{
            key: '0-1-0',
            title: '0-1-0'
        }, {
            key: '0-1-1',
            title: '0-1-1'
        }],
    },
    {
        key: '0-2',
        title: '0-2'
    },
    {
        key: '0-3',
        title: '0-3'
    },
    {
        key: '0-4',
        title: '0-4',
        children: [{
            key: '0-4-0',
            title: '0-4-0'
        }, {
            key: '0-4-1',
            title: '0-4-1'
        }],
    }
];

function handleSearch(value) {
    console.log('search', value);
}

function onSelectChange(value) {
    console.log('selected', value);
    setState({selectedKeys: value});
}

initialState = {
    selectedKeys: []
};

function initSelectedKeys() {
    setState({selectedKeys: ['0-2']});
}

<div>
    <div>树形穿梭框</div><br />
    <button type="button" onClick={initSelectedKeys}>初始化选中项</button><br /><br />
    <Transfer
        type="tree"
        dataSource={DATASOURCE}
        showSearch
        showResultSearch
        selectedKeys={state.selectedKeys}
        onSearch={handleSearch}
        onSelectChange={onSelectChange}
        render={item => item.title}
    />
</div>
```

## 一种业务场景的扩展

```jsx
const TransferCustom = Transfer.TransferCustom;
const DATASOURCE = [];
for (let i = 0; i < 50; i++) {
    const randomId = +new Date();
    const departmentArray = ['智能云', '富媒体', '地图'];
    DATASOURCE.push({
        "name": `啦啦啦${i}`,
        "department": departmentArray[i % 3],
        "employeeId": i,
        "avatarPath": "./logo.png",
        "userTypeList": [{
            "userTypeId": "6057e507-7f44-4329-af4c-5a5aa8218bf5",
            "userTypeName": "员工"
        }, {
            "userTypeId": "7bbc1a29-11a8-4493-8a14-3de0e3df29cb",
            "userTypeName": "访客"
        }],
        "userTypeIdList": ["6057e507-7f44-4329-af4c-5a5aa8218bf5", "7bbc1a29-11a8-4493-8a14-3de0e3df29cb"],
        "createTime": "2019-10-21T16:13:32Z",
        "updateTime": "2019-10-21T11:39:49Z",
        "employeeStatus": "valid",
        "id": i
    })
}

const dataSource = DATASOURCE.map(item => ({
    ...item,
    key: item.employeeId
}));

function handleSearch(value) {
    console.log('search', value);
}

function onSelectChange(value) {
    console.log('selected', value);
}

function filterOption(filterText, item) {
    const curTitle = `${item.name} - ${item.department}`;
    return curTitle.indexOf(filterText) >= 0;
}

function renderItem(item) {
    const customLabel = (
        <span className="custom-item">
            <span key={`${item.employeeId}-img`} className="custom-img">
                <img src={item.avatarPath} />
            </span>
            {item.name}
            <span key={`${item.employeeId}-desc`} className="custom-desc">
                {item.department}
            </span>
        </span>
    );
    return {
        label: customLabel, // for displayed item
        value: `${item.name}-${item.department}` // for title and filter matching
    };
};

function prodTreeDataSource(dataSource) {
    const dataMap = {};
    _.forEach(dataSource, data => {
        if (!dataMap[data.department]) {
            dataMap[data.department] = {
                key: data.department,
                title: data.department,
                children: [{
                    ...data,
                    key: data.employeeId,
                    title: renderItem(data).label
                }]
            };
        }
        else {
            dataMap[data.department].children.push({
                ...data,
                key: data.employeeId,
                title: renderItem(data).label
            });
        }
    });

    return Object.values(dataMap);
};

const treeDataSource = prodTreeDataSource(dataSource);

<div>
 <div>一种业务场景的扩展 ๑乛◡乛๑ </div><br />
    <TransferCustom
        type="tree"
        dataSource={dataSource}
        treeDataSource={treeDataSource}
        filterOption={filterOption}
        render={renderItem}
        onSearch={handleSearch}
        onSelectChange={onSelectChange}
    />
</div>
```

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/Transfer>
