---
title: Tree
---

可编辑树。

- 树的增删改
- 展示树的线

## 引入

```jsx
import {components} from 'baidu-acu-react-common';

const Tree = components.Tree;
```

## 基本用法

```jsx
import {StrikethroughOutlined} from '@ant-design/icons';

const treeData = {
    "value": "000000000000000000000000",
    "text": "全部位置",
    "children": [{
        "value": "5dc51d374136c4156cfd05a9",
        "text": "百度",
        "children": [{
            "value": "5dc521ad4136c4156cfd05ac",
            "text": "百度大厦",
            "children": [{
                "value": "5dc523fb4136c4156cfd05c2",
                "text": "A座",
                "children": []
            }, {
                "value": "5dc525674136c4156cfd05c9",
                "text": "B座",
                "children": []
            }, {
                "value": "5dc5256f4136c4156cfd05cd",
                "text": "C座",
                "children": []
            }]
        }, {
            "value": "5dc521b94136c4156cfd05ad",
            "text": "百度科技园",
            "children": [{
                "value": "5dc522324136c4156cfd05b1",
                "text": "科技园K5",
                "children": [{
                    "value": "5dc522e44136c4156cfd05b4",
                    "text": "A座",
                    "children": [{
                        "value": "5dc5270e4136c4156cfd05d8",
                        "text": "F1",
                        "children": []
                    }, {
                        "value": "5dc527124136c4156cfd05d9",
                        "text": "F2",
                        "children": []
                    }, {
                        "value": "5dc527154136c4156cfd05da",
                        "text": "F3",
                        "children": []
                    }, {
                        "value": "5dc527184136c4156cfd05db",
                        "text": "F4",
                        "children": []
                    }, {
                        "value": "5dc5271d4136c4156cfd05dc",
                        "text": "F5",
                        "children": []
                    }, {
                        "value": "5dc527254136c4156cfd05dd",
                        "text": "F6",
                        "children": []
                    }, {
                        "value": "5dc5272a4136c4156cfd05de",
                        "text": "F7",
                        "children": []
                    }]
                }, {
                    "value": "5dc522f34136c4156cfd05b5",
                    "text": "B座",
                    "children": [{
                        "value": "5dc522f94136c4156cfd05b7",
                        "text": "F7",
                        "children": []
                    }]
                }]
            }, {
                "value": "5dc525804136c4156cfd05ce",
                "text": "科技园K6",
                "children": []
            }, {
                "value": "5dc525954136c4156cfd05cf",
                "text": "科技园K2",
                "children": []
            }]
        }, {
            "value": "5dc526864136c4156cfd05d6",
            "text": "鹏寰大厦",
            "children": []
        }, {
            "value": "5dc5268c4136c4156cfd05d7",
            "text": "奎科大厦",
            "children": []
        }]
    }, {
        "value": "5dc526124136c4156cfd05d3",
        "text": "腾讯",
        "children": [{
            "value": "5dc526254136c4156cfd05d4",
            "text": "北京总部",
            "children": []
        }, {
            "value": "5dc526654136c4156cfd05d5",
            "text": "深圳总部",
            "children": []
        }]
    }, {
        "value": "5dc9271f1eb7e86030bcf313",
        "text": "阿里巴巴",
        "children": []
    }]
};

const handleCheck = checkedKeys => {
    console.log('checked: ', checkedKeys);
};
const handleUpdate = params => {
    console.log('update: ', params);
};
const handleCreate = params => {
    console.log('create: ', params);
};
const handleDelete = data => {
    console.log('delete: ', data);
};
const handleSelect = selectId => {
    console.log('select: ', selectId);
};

<Tree
    height={400}
    width={700}
    className="position-location"
    placeholder="输入所属位置"
    list={treeData}
    selectId="5dc51d374136c4156cfd05a9"
    editable
    checkable
    expandable
    nodeIcon={<StrikethroughOutlined />}
    onCheck={handleCheck}
    onUpdate={handleUpdate}
    onCreate={handleCreate}
    onDelete={handleDelete}
    onSelect={handleSelect}
/>
```

## API

| 参数        | 说明                            | 类型                                                                     | 默认值 |
| ----------- | ------------------------------- | ------------------------------------------------------------------------ | ------ |
| list        | 结构数据                        | `{value?: string; text?: string; type?: string; children?: TreeData[];}` | `{}`   |
| width       | 宽，横向超过会出现滚动条        | `string,number`                                                          | `100%` |
| height      | 高，纵向超过会出现滚动条        | `string,number`                                                          | `--`   |
| itemHeight  | 高，每个节点的高度              | `string`                                                                 | `50px` |
| placeholder | 输入框提示文案                  | `string`                                                                 | `--`   |
| className   | 类名                            | `string`                                                                 | `--`   |
| nodeIcon    | 节点前icon                      | `React.ReactNode`                                                        | `--`   |
| selectId    | 默认选中项，与list中的value对应 | `string`                                                                 | `--`   |
| editable    | 是否可以编辑                    | `boolean`                                                                | `true` |
| checkable   | 节点前添加 Checkbox 复选框      | `boolean`                                                                | `true` |
| expandable  | 是否可以展开收起                | `boolean`                                                                | `true` |
| onError     | 请求失败提示                    | `(error: Error) => void`                                                 | `--`   |
| onUpdate    | 更新回调                        | `(params: UpdateParams, callback: Callback) => void`                     | `--`   |
| onCreate    | 新增回调                        | `(params: CreateParams, callback: Callback) => void`                     | `--`   |
| onDelete    | 删除回调                        | `(data: TreeData, callback: () => void) => void`                         | `--`   |
| onSelect    | 选择回调                        | `(selectId: string) => void`                                             | `--`   |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E9%80%9A%E7%94%A8%E7%BB%84%E4%BB%B6/Tree>
