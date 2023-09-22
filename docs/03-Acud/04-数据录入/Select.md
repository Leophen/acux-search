---
title: Select 选择器
---

下拉选择器。

## 引入

```js
import {Select} from 'acud';
```

## 基本用法

```jsx live fff
function App() {
    const {Option} = Select;
    const [value, setValue] = useState('data1');

    const handleChange = val => {
        console.log(val);
        setValue(val);
    };

    return (
        <div className="acux-demo-column">
            <h5>无默认值</h5>
            <Select>
                <Option value="data1">data1</Option>
                <Option value="data2">data2</Option>
                <Option value="data3">data3</Option>
                <Option value="data4">data4</Option>
            </Select>

            <h5>有默认值（非受控）</h5>
            <Select defaultValue={value}>
                <Option value="data1">data1</Option>
                <Option value="data2">data2</Option>
                <Option value="data3">data3</Option>
                <Option value="data4">data4</Option>
            </Select>

            <h5>有固定值（受控）</h5>
            <Select value={value}>
                <Option value="data1">data1</Option>
                <Option value="data2">data2</Option>
                <Option value="data3">data3</Option>
                <Option value="data4">data4</Option>
            </Select>

            <h5>通用方法</h5>
            <Select value={value} onChange={handleChange}>
                <Option value="data1">data1</Option>
                <Option value="data2">data2</Option>
                <Option value="data3">data3</Option>
                <Option value="data4">data4</Option>
            </Select>
        </div>
    );
}
```

## 禁用状态

```jsx live fff
<Select disabled>
    <Option value="data1">data1</Option>
    <Option value="data2">data2</Option>
    <Option value="data3">data3</Option>
    <Option value="data4">data4</Option>
</Select>
```

## 传入列表的用法

```jsx live fff
function App() {
    const {Option} = Select;

    const optionsDemo = [
        {value: 'data1', label: 'data1'},
        {value: 'data2', label: 'data2'},
        {value: 'data3', label: 'data3'},
        {value: 'data4', label: 'data4'}
    ];

    return (
        <div className="acux-demo-column">
            <Select options={optionsDemo} />
            <Select>
                <Option value="data1">data1</Option>
                <Option value="data2">data2</Option>
                <Option value="data3">data3</Option>
                <Option value="data4">data4</Option>
            </Select>
        </div>
    );
}
```

## 空选项

```jsx live fff
<div className="acux-demo-column">
    <Select options={[]} />
    <Select></Select>
</div>
```

## 可清空

```jsx live fff
<Select allowClear>
    <Option value="data1">data1</Option>
    <Option value="data2">data2</Option>
    <Option value="data3">data3</Option>
    <Option value="data4">data4</Option>
</Select>
```

## 弹窗位置

```jsx live fff
<div className="acux-demo-column">
    <h5>bottomLeft</h5>
    <Select placement="bottomLeft">
        <Option value="data1">data1</Option>
        <Option value="data2">data2</Option>
        <Option value="data3">data3</Option>
        <Option value="data4">data4</Option>
    </Select>

    <h5>bottomRight</h5>
    <Select placement="bottomRight">
        <Option value="data1">data1</Option>
        <Option value="data2">data2</Option>
        <Option value="data3">data3</Option>
        <Option value="data4">data4</Option>
    </Select>

    <h5>topLeft</h5>
    <Select placement="topLeft">
        <Option value="data1">data1</Option>
        <Option value="data2">data2</Option>
        <Option value="data3">data3</Option>
        <Option value="data4">data4</Option>
    </Select>

    <h5>topRight</h5>
    <Select placement="topRight">
        <Option value="data1">data1</Option>
        <Option value="data2">data2</Option>
        <Option value="data3">data3</Option>
        <Option value="data4">data4</Option>
    </Select>
</div>
```

## 弹窗滚动逻辑

弹层展示逻辑，默认为可视区域滚动，可配置成滚动区域滚动。

```jsx live fff
<div className="acux-demo-column">
    <h5>viewport</h5>
    <Select popupOverflow="viewport">
        <Option value="data1">data1</Option>
        <Option value="data2">data2</Option>
        <Option value="data3">data3</Option>
        <Option value="data4">data4</Option>
    </Select>

    <h5>scroll</h5>
    <Select popupOverflow="scroll">
        <Option value="data1">data1</Option>
        <Option value="data2">data2</Option>
        <Option value="data3">data3</Option>
        <Option value="data4">data4</Option>
    </Select>
</div>
```

## 下拉多选

多选，从已有条目中选择。

```jsx live fff
function App() {
    const {Option} = Select;

    const optionsDemo = [
        {value: 'data1', label: 'data1'},
        {value: 'data2', label: 'data2'},
        {value: 'data3', label: 'data3', disabled: true},
        {value: 'data4', label: 'data4'}
    ];

    return (
        <div className="acux-demo-column">
            <Select mode="multiple" options={optionsDemo} />
            <Select mode="multiple" defaultValue={['data1', 'data2']} options={optionsDemo} />
            <Select mode="multiple">
                <Option value="data1">data1</Option>
                <Option value="data2">data2</Option>
                <Option value="data3" disabled>data3</Option>
                <Option value="data4">data4</Option>
            </Select>
        </div>
    );
}
```

## 带搜索框

```jsx live fff
function App() {
    const {Option} = Select;

    function onChange(value) {
        console.log(`selected ${value}`);
    }

    function onBlur() {
        console.log('blur');
    }

    function onFocus() {
        console.log('focus');
    }

    function onSearch(val) {
        console.log('search:', val);
    }

    return (
        <Select
            showSearch
            style={{width: 200}}
            optionFilterProp="children"
            onChange={onChange}
            onFocus={onFocus}
            onBlur={onBlur}
            onSearch={onSearch}
            filterOption={(input, option) =>
                option.children.toLowerCase().indexOf(input.toLowerCase()) >= 0
            }
        >
            <Option value="jack">Jack</Option>
            <Option value="lucy">Lucy</Option>
            <Option value="tom">Tom</Option>
        </Select>
    );
}
```

## 多选搜索

```jsx live fff
function App() {
    const {Option} = Select;

    const children = [];
    for (let i = 10; i < 16; i++) {
        children.push(
            <Option value={i.toString(36) + i}>{i.toString(36) + i}</Option>
        );
    }

    const children2 = [
        <Option value="data1">data1</Option>,
        <Option value="data2">data2</Option>,
        <Option value="data3">data3</Option>,
        <Option value="data4" disabled>
            data4
        </Option>,
        <Option value="data5">data5</Option>,
        <Option value="data6">data6</Option>,
        <Option value="data7">data7</Option>,
        <Option value="sakta8">SaKta8</Option>,
        <Option value="data9">data9</Option>,
        <Option value="data10" disabled>
            data10
        </Option>,
        <Option value="data11">data11</Option>
    ];

    function handleChange(value) {
        console.log(`selected ${value}`);
    }

    return (
        <div className="acux-demo-column">
            <Select
                mode="multiple"
                allowClear
                showSearch
                style={{width: '100%'}}
                defaultValue={['a10', 'c12']}
                onChange={handleChange}
            >
                {children}
            </Select>
            <Select
                mode="multiple"
                style={{width: '100%'}}
                allowClear
                showSearch
                placeholder="请选择"
                defaultValue={['data3', 'data4']}
                onChange={handleChange}
            >
                {children2}
            </Select>
        </div>
    );
}
```

## 大数据量、展示 title

```jsx live fff
function App() {
    const {Option} = Select;

    function handleChange(value) {
        console.log(`selected ${value}`);
    }

    function getOptions() {
        const options = [];
        for (let i = 3, len = 100000; i < len; i++) {
            options.push(
                <Option key={i} title={`data${i}`} value={`data${i}`}>
                    data{i}
                </Option>
            );
        }
        return options;
    }

    const children = [
        <Option value="data1">data10000000000000000000</Option>,
        <Option value="data2">data2000000000000000</Option>,
        <Option value="data3">data300000000000000000</Option>,
        <Option value="data4">data400000000000000000</Option>,
        <Option value="data5">data50000000000000000</Option>,
        <Option value="data6">data60000000000000000</Option>,
        <Option value="data7">data70000000000000000</Option>,
        <Option value="data8">data80000000000000000</Option>,
        <Option value="data9">data90000000000000000</Option>,
        <Option value="data10">data100000000000000000</Option>,
        <Option value="data11">data11000000000000000</Option>
    ];

    return (
        <div className="acux-demo-column">
            <Select
                defaultValue="data2"
                showTitle
                maxTagTextLength={8}
                style={{width: 160}}
                onChange={handleChange}
            >
                <Option key={1} value="data1">
                    data1
                </Option>
                <Option key={2} value="data2">
                    我的数据量非常大，已经超过了最大宽度了
                </Option>
                {getOptions()}
            </Select>
            <Select
                mode="multiple"
                style={{width: 160}}
                showTitle
                onChange={handleChange}
            >
                {children}
            </Select>
        </div>
    );
}
```

## 自定义 option 渲染

option children 外层加 Tooltip 并正确显示的例子 此方法可以不干扰搜索高亮效果。

```jsx live fff
function App() {
    const {Option} = Select;

    const children = [
        <Option value="data1">data177777756764564654564546564546564</Option>,
        <Option value="data2">data2</Option>,
        <Option value="data3">data3</Option>,
        <Option value="data4">data4</Option>,
        <Option value="data5">data5</Option>,
        <Option value="data6">data6</Option>,
        <Option value="data7">data7</Option>,
        <Option value="data8">data8</Option>,
        <Option value="data9">data9</Option>,
        <Option value="data10">data10</Option>,
        <Option value="data11">data11</Option>
    ];

    const options = [
        {value: 'data1', label: 'data11111111111111111111111111111'},
        {value: 'data2', label: 'data2'},
        {value: 'data3', label: 'data3'},
        {value: 'data4', label: 'data4'},
        {value: 'data5', label: 'data5'}
    ];

    function handleChange(value) {
        console.log(`selected ${value}`);
    }

    return (
        <div className="acux-demo-column">
            <Select
                mode="multiple"
                maxTagCount={6}
                allowClear
                style={{width: 200}}
                maxTagTextLength={10}
                placeholder="请选择"
                defaultValue={['data3', 'data4']}
                onChange={handleChange}
                optionRender={(label, option) => {
                    return (
                        <Tooltip placement="right" title={label}>
                            <span style={{
                                display: 'inline-block',
                                maxWidth: '100%',
                                overflow: 'hidden',
                                textOverflow: 'ellipsis',
                                verticalAlign: 'middle'
                            }}
                            >{label}
                            </span>
                        </Tooltip>
                    );
                }}
            >
                {children}
            </Select>
            <Select
                mode="multiple"
                maxTagCount={6}
                allowClear
                style={{width: 200}}
                maxTagTextLength={10}
                placeholder="请选择"
                onChange={handleChange}
                options={options}
                optionRender={(label, option) => {
                    return (
                        <Tooltip placement="right" title={label}>
                            <span style={{
                                display: 'inline-block',
                                maxWidth: '100%',
                                overflow: 'hidden',
                                textOverflow: 'ellipsis',
                                verticalAlign: 'middle'
                            }}
                            >{label}
                            </span>
                        </Tooltip>
                    );
                }}
            />
        </div>
    );
}
```

## 下拉分组

用 `OptGroup` 进行选项分组。

```jsx live fff
function App() {
    const {Option, OptGroup} = Select;

    function handleChange(value) {
        console.log(`selected ${value}`);
    }

    function handleExpandChange(key) {
        console.log('expand key:', key);
    }

    return (
        <div className="acux-demo-column">
            <Select
                defaultValue="zhangsan"
                keepExpand
                style={{width: 320}}
                groupSelectorRender={(groupLabel, value) => value}
                onChange={handleChange}
            >
                <OptGroup label="Manager" key="manager">
                    <Option value="zhangsan">zhangsan</Option>
                    <Option value="lisi">lisi</Option>
                </OptGroup>
                <OptGroup label="Engineer">
                    <Option value="xiaoming">xiaoming</Option>
                </OptGroup>
                <Option value="xiaodong">xiaodong</Option>
            </Select>

            <Select
                defaultValue="zhangsan"
                defaultExpandGroupKey={['manager']}
                style={{width: 320}}
                onChange={handleChange}
                onExpandChange={handleExpandChange}
            >
                <OptGroup label="Manager" key="manager">
                    <Option value="zhangsan">zhangsan</Option>
                    <Option value="lisi">lisi</Option>
                </OptGroup>
                <OptGroup label="Engineer">
                    <Option value="xiaoming">xiaoming</Option>
                </OptGroup>
                <Option value="xiaodong">xiaodong</Option>
            </Select>

            <Select
                defaultValue="zhangsan"
                style={{width: 320}}
                defaultExpandGroupKey={['manager']}
                mode="multiple"
                onChange={handleChange}
                onExpandChange={handleExpandChange}
            >
                <OptGroup label="Manager" key="manager">
                    <Option value="zhangsan">zhangsan</Option>
                    <Option value="lisi">lisi</Option>
                </OptGroup>
                <OptGroup label="Engineer" key="engineer">
                    <Option value="xiaoming">xiaoming</Option>
                </OptGroup>
            </Select>

            <Select
                defaultValue={['zhangsan', 'xiaohua']}
                allowClear
                defaultExpandGroupKey
                style={{width: 320}}
                mode="multiple"
                onChange={handleChange}
            >
                <OptGroup label="Manager" key="manager">
                    <Option value="zhangsan">zhangsan</Option>
                    <Option value="lisi">lisi</Option>
                    <Option value="wanger" disabled>wanger</Option>
                </OptGroup>
                <OptGroup label="Engineer" key="engineer">
                    <Option value="xiaoming">xiaoming</Option>
                    <Option value="xiaohua" disabled>xiaohua</Option>
                </OptGroup>
                <OptGroup label="Disabled" key="disabled">
                    <Option value="d1" disabled>d1</Option>
                    <Option value="d2" disabled>d2</Option>
                </OptGroup>
            </Select>
        </div>
    );
}
```

## options 可变

```jsx live fff
function App() {
    const [opts, setOpts] = useState([{label: 1, value: 1}]);
    const onChange = () => {
        setOpts([{value: 2, label: 2}, {value: 3, label: 3}]);
    };

    return (
        <div className="acux-demo-row">
            <Button onClick={onChange}>change options</Button>
            <Select
                options={opts}
            />
        </div>
    );
}
```

## 自定义选择器菜单

自定义选择器下拉菜单，支持新增菜单项和删除菜单项。

```jsx live fff
function App() {
    const {Option} = Select;

    const [value, setValue] = useState();
    const [newData, setNewData] = useState();
    const [data, setData] = useState(['data1', 'data2']);
    const [addEdData, setAddEdData] = useState([]);
    const [addDisabled, setAddDisabled] = useState(true);

    const handleChange = value => {
        console.log(value);
        setValue(value);
    };

    const handleDataChange = e => {
        const value = e.target.value;
        setNewData(value);
    };

    useEffect(() => {
        setAddDisabled(!newData);
        return () => setAddDisabled(true);
    }, [newData]);

    const handleAdd = () => {
        setData(data => [...data, newData]);
        setAddEdData(addEdData => [...addEdData, newData]);
        setNewData();
    };

    const handleDeleteData = (e, item) => {
        const index = data.indexOf(item);
        setData(data => {
            const cloneData = [...data];
            cloneData.splice(index, 1);
            return cloneData;
        });
        const addEdIndex = addEdData.indexOf(item);
        setAddEdData(addEdData => {
            const cloneAddEdData = [...addEdData];
            cloneAddEdData.splice(addEdIndex, 1);
            return cloneAddEdData;
        });
        if (value === item) {
            setValue(undefined);
        }
        e.stopPropagation();
    };

    return (
        <Select
            allowClear
            style={{width: 240}}
            value={value}
            dropdownRender={menu => {
                return (
                    <>
                        {menu}
                        <div className="acux-demo-row">
                            <Input
                                style={{width: "60%"}}
                                placeholder="请输入"
                                size="small"
                                value={newData}
                                onChange={handleDataChange}
                            />
                            <Button
                                style={{width: "20%"}}
                                size="small"
                                icon={<OutlinedPlus />}
                                type="text"
                                disabled={addDisabled}
                                onClick={handleAdd}
                            >
                                新建
                            </Button>
                        </div>
                    </>
                );
            }}
            onChange={handleChange}
        >
            {data.map(item => {
                if (addEdData.includes(item)) {
                    return (
                        <Option
                            value={item}
                            key={item}
                            extra={
                                <OutlinedClose
                                    className={'acux-demo-row'}
                                    onClick={e => handleDeleteData(e, item)}
                                />
                            }
                        >
                            {item}
                        </Option>
                    );
                }
                return (
                    <Option value={item} key={item}>
                        {item}
                    </Option>
                );
            })}
        </Select>
    );
}
```

## API

### Select props

| 参数                     | 说明                                                                                                                                                                  | 类型                                                                           | 默认值                  |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ----------------------- |
| allowClear               | 支持清除                                                                                                                                                              | `boolean`                                                                      | `false`                 |
| autoClearSearchValue     | 是否在选中项后清空搜索框，只在 `mode` 为 `multiple`                                                                                                                   | `boolean`                                                                      | `true`                  |
| autoFocus                | 默认获取焦点                                                                                                                                                          | `boolean`                                                                      | `false`                 |
| bordered                 | 是否有边框                                                                                                                                                            | `boolean`                                                                      | `true`                  |
| clearIcon                | 自定义的多选框清空图标                                                                                                                                                | `ReactNode`                                                                    | `--`                    |
| defaultActiveFirstOption | 是否默认高亮第一个选项                                                                                                                                                | `boolean`                                                                      | `true`                  |
| defaultOpen              | 是否默认展开下拉菜单                                                                                                                                                  | `boolean`                                                                      | `--`                    |
| defaultValue             | 指定默认选中的条目                                                                                                                                                    | `string〡string[]`<br />`number〡number[]`<br />`LabeledValue〡LabeledValue[]` | `--`                    |
| disabled                 | 是否禁用                                                                                                                                                              | `boolean`                                                                      | `false`                 |
| dropdownClassName        | 下拉菜单的 className 属性                                                                                                                                             | `string`                                                                       | `--`                    |
| dropdownMatchSelectWidth | 下拉菜单是否和选择器同宽，值为 false 时会关闭虚拟滚动。如果设置为 number，当值小于选择框宽度时会被忽略。                                                              | `boolean〡number`                                                              | `true`                  |
| dropdownRender           | 自定义下拉框内容                                                                                                                                                      | `(originNode: ReactNode) => ReactNode`                                         | `--`                    |
| dropdownStyle            | 下拉菜单的 style 属性                                                                                                                                                 | `CSSProperties`                                                                | `--`                    |
| filterOption             | 是否根据输入项进行筛选。当其为一个函数时，会接收 `inputValue` `option` 两个参数，当 `option` 符合筛选条件时，应返回 true，反之则返回 false                            | `boolean〡function(inputValue, option)`                                        | `true`                  |
| optionRender             | 自定义 option 渲染                                                                                                                                                    | `(label: ReactNode, option) => ReactNode`                                      | `--`                    |
| filterSort               | 搜索时对筛选结果项的排序函数, 类似[Array.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)里的 compareFunction       | `(optionA: Option, optionB: Option) => number`                                 | `--`                    |
| getPopupContainer        | 菜单渲染父节点。默认渲染到 body 上，如果你遇到菜单滚动定位问题，试试修改为滚动的区域，并相对其定位。                                                                  | `function(triggerNode)`                                                        | ` () => document.body ` |
| labelInValue             | 是否把每个选项的 label 包装到 value 中，会把 Select 的 value 类型从 `string` 变为 { value: string, label: ReactNode } 的格式                                          | `boolean`                                                                      | `false`                 |
| listHeight               | 设置弹窗滚动高度                                                                                                                                                      | `number`                                                                       | `256`                   |
| loading                  | 加载中状态                                                                                                                                                            | `boolean`                                                                      | `false`                 |
| maxTagCount              | 最多显示多少个 tag，响应式模式会对性能产生损耗                                                                                                                        | `number`〡`responsive`                                                         | `--`                    |
| maxTagPlaceholder        | 隐藏 tag 时显示的内容                                                                                                                                                 | `ReactNode`〡`function(omittedValues)`                                         | `--`                    |
| maxTagTextLength         | 最大显示的 tag 文本长度                                                                                                                                               | `number`                                                                       | `--`                    |
| menuItemSelectedIcon     | 自定义多选时当前选中的条目图标                                                                                                                                        | `ReactNode`                                                                    | `--`                    |
| mode                     | 设置 Select 的模式为多选(默认单选)                                                                                                                                    | `multiple`                                                                     | `--`                    |
| notFoundContent          | 当下拉列表为空时显示的内容                                                                                                                                            | `ReactNode`                                                                    | ``Not Found``           |
| open                     | 是否展开下拉菜单                                                                                                                                                      | `boolean`                                                                      | `--`                    |
| optionFilterProp         | 搜索时过滤对应的 `option` 属性，如设置为 `children` 表示对内嵌内容进行搜索。若通过 `options` 属性配置选项内容，建议设置 `optionFilterProp="label"` 来对内容进行搜索。 | `string`                                                                       | `value`                 |
| optionLabelProp          | 回填到选择框的 Option 的属性值，默认是 Option 的子元素。比如在子元素需要高亮效果时，此值可以设为 `value`                                                              | `string`                                                                       | `children`              |
| options                  | 数据化配置选项内容，相比 jsx 定义会获得更好的渲染性能                                                                                                                 | `{label, value}[]`                                                             | `--`                    |
| placeholder              | 选择框默认文本                                                                                                                                                        | `string`                                                                       | `请选择`                |
| placement                | 选择框弹出位置                                                                                                                                                        | `bottomLeft`〡`bottomRight`〡`topLeft`〡`topRight`                             | `bottomLeft`            |
| popupOverflow            | 弹层展示逻辑，默认为可视区域滚动，可配置成滚动区域滚动                                                                                                                | `viewport`〡`scroll`                                                           | `viewport`              |
| removeIcon               | 自定义的多选框清除图标                                                                                                                                                | `ReactNode`                                                                    | `--`                    |
| searchValue              | 控制搜索文本                                                                                                                                                          | `string`                                                                       | `--`                    |
| showArrow                | 是否显示下拉小箭头                                                                                                                                                    | `boolean`                                                                      | `true`                  |
| showSearch               | 使单选模式可搜索                                                                                                                                                      | `boolean`                                                                      | `false`                 |
| showTitle                | 是否展示 option title                                                                                                                                                 | `boolean`                                                                      | `false`                 |
| showSelectAll            | 是否展示全选项，多选时有效                                                                                                                                            | `boolean`                                                                      | `true`                  |
| suffixIcon               | 自定义的选择框后缀图标                                                                                                                                                | `ReactNode`                                                                    | `--`                    |
| groupSelectorRender      | 自定义分组选择器选中项的 label                                                                                                                                        | `(groupLable, value) => ReactNode`                                             | `--`                    |
| tagRender                | 自定义 tag 内容 render                                                                                                                                                | `(props) => ReactNode`                                                         | `--`                    |
| tokenSeparators          | 在 `tags` 和 `multiple` 模式下自动分词的分隔符                                                                                                                        | `string[]`                                                                     | `--`                    |
| value                    | 指定当前选中的条目                                                                                                                                                    | `string〡string[]`<br />`number〡number[]`<br />`LabeledValue〡LabeledValue[]` | `--`                    |
| virtual                  | 设置 false 时关闭虚拟滚动（可折叠分组模式下，始终关闭虚拟滚动）                                                                                                       | `boolean`                                                                      | `true`                  |
| keepExpand               | 分组始终展开，并且不可操作，只有单选时生效                                                                                                                            | `boolean`                                                                      | `false`                 |
| defaultExpandGroupKey    | 默认展开的分组 key, 为 true 时全部展开，为 false 时全部收起，也可以指定展开组的 key（如果没有设置 key，则为该分组的 index 下标字符串）                                | `string[]`〡`string〡number[]`〡`number〡boolean`                              | `false`                 |
| onBlur                   | 失去焦点时回调                                                                                                                                                        | `function`                                                                     | `--`                    |
| onChange                 | 选中 option，或 input 的 value 变化时，调用此函数                                                                                                                     | `function(value, option:Option〡Array&lt;Option>)`                             | `--`                    |
| onClear                  | 清除内容时回调                                                                                                                                                        | `function`                                                                     | `--`                    |
| onDeselect               | 取消选中时调用，参数为选中项的 value (或 key) 值，仅在 `multiple` 或 `tags` 模式下生效                                                                                | `function(string〡number〡LabeledValue)`                                       | `--`                    |
| onDropdownVisibleChange  | 展开下拉菜单的回调                                                                                                                                                    | `function(open)`                                                               | `--`                    |
| onFocus                  | 获得焦点时回调                                                                                                                                                        | `function`                                                                     | `--`                    |
| onInputKeyDown           | 按键按下时回调                                                                                                                                                        | `function`                                                                     | `--`                    |
| onMouseEnter             | 鼠标移入时回调                                                                                                                                                        | `function`                                                                     | `--`                    |
| onMouseLeave             | 鼠标移出时回调                                                                                                                                                        | `function`                                                                     | `--`                    |
| onPopupScroll            | 下拉列表滚动时的回调                                                                                                                                                  | `function`                                                                     | `--`                    |
| onSearch                 | 文本框值变化时回调                                                                                                                                                    | `function(value: string)`                                                      | `--`                    |
| onSelect                 | 被选中时调用，参数为选中项的 value (或 key) 值                                                                                                                        | `function(string〡number〡LabeledValue, option: Option)`                       | `--`                    |
| onExpandChange           | 分组展开收起变化时触发，参数为所有展开项的 key                                                                                                                        | `function(key:(string〡number)[])`                                             | `--`                    |

:::caution 注意

如果发现下拉菜单跟随页面滚动，或者需要在其他弹层中触发 Select，请尝试使用 `getPopupContainer={triggerNode => triggerNode.parentElement}` 将下拉弹层渲染节点固定在触发器的父元素中。

:::

### Select Methods

| 名称    | 说明     |
| ------- | -------- |
| blur()  | 取消焦点 |
| focus() | 获取焦点 |

### Option props

| 参数      | 说明                              | 类型             | 默认值  |
| --------- | --------------------------------- | ---------------- | ------- |
| className | Option 器类名                     | `string`         | `--`    |
| disabled  | 是否禁用                          | `boolean`        | `false` |
| title     | 选中该 Option 后，Select 的 title | `string`         | `--`    |
| value     | 默认根据此属性值进行筛选          | `string〡number` | `--`    |
| extra     | 额外的元素                        | `ReactNode`      | `--`    |

### OptGroup props

| 参数  | 说明 | 类型                    | 默认值 |
| ----- | ---- | ----------------------- | ------ |
| key   | Key  | `string`                | `--`   |
| label | 组名 | `string〡React.Element` | `--`   |
