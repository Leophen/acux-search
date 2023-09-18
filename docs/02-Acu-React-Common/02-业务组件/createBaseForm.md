---
title: createBaseForm
---

通过配置，结合 redux 用来快速生成表单的高阶组件。

## 引入

```js
import {components} from 'baidu-acu-react-common';

const createBaseForm = components.createBaseForm;
```

## 基本用法

为了提高开发效率，避免大量逻辑类似的 antd 组件代码，将 antd 组件及基本的逻辑功能抽取出来并通过配置来生成表单页。功能如下：

- 支持表单内容获取：
  - 请求
  - 传值
- 支持表单选项内容获取
- 支持表单提交

```jsx
import {components} from 'baidu-acu-react-common';

const createBaseForm = components.createBaseForm;

// 表单项配置项
const controls = function () {
    return [];
};

const stepControls = function () {
    return [
        {
            title: '第一步',
            controls: []
        },
        ...
    ];
};

@createBaseForm
class Form extends React.Component {
    options = {
        controls
        ...
    }
}
export default Form;
```

## options 配置方法

```js
{
    className: '',
    title: '',
    controls: function () {return controls},             // 必传：DuFormItem配置项

    type: 'step',                                       // 若传了type为step，则为分步表单，controls取stepControls，而非controls
    stepControls: function () {return stepControls},    // 分步表单配置项
    
    formData: {},                                       // 非接口直接传值给form
    
    fetchFormAction: '',                                // 接口获取表单数据
    fetchFormPayload: {},
    fetchKey: '',                                       // actions里的key值
    $onFetchFormResponse(formData) {},                  // 成功之后回调
    updateDetailAction: ''                              // 伴随$onFetchFormResponse存在，用于修改了detail再通过redux传给props
    $formatFormData(formData) {},                       // 接口数据格式化
    
    submitFormAction: ''                                // 必传：submit提交接口
    submitFormPayload: [],                              // 额外的请求参数
    $onSubmitRequest(payload) {},                       // 发起请求之前
    $onSubmitResponse: res => function () {},           // 成功之后
    $onSubmitError(error) {},                           // 错误之后
    $toastSuccessMessage: 'success~~~',
    $toastErrorMessage: '',

    fetchOptionsAction: [                               // 接口获取选项内容
        {
            name: '',                                   // 选项内容关联controls - name
            action: '',                                 // action
            payload: {},
            fetchKey: ['value', 'label']                // fetch[0]为value对应字段，fetch[1]为label对应字段
        }
    ]
}
```

## options - api

| 参数                 | 说明                 | 类型       | 默认值 |
| -------------------- | -------------------- | ---------- | ------ |
| className            |                      | `string`   | `--`   |
| title                |                      | `string`   | `--`   |
| controls             | 表单项配置项，见下文 | `Function` | `--`   |
| type                 | 表单类型             | `string`   | `--`   |
| stepControls         | 分步表单配置项       | `Function` | `--`   |
| fetchFormAction      | 接口获取表单数据     | `string`   | `--`   |
| fetchFormPayload     | 请求参数             | `Object`   | `--`   |
| fetchKey             | actions里的key值     | `string`   | `--`   |
| formData             | 非接口直接传值给form | `bool`     | `--`   |
| $onFetchFormResponse | 成功回调             | `Function` | `--`   |
| $formatFormData      | 接口数据格式化       | `Function` | `--`   |
| submitFormAction     | submit提交接口       | `string`   | `--`   |
| submitFormPayload    | 额外的请求参数       | `Object`   | `--`   |
| $onSubmitRequest     | 发起请求之前回调     | `Function` | `--`   |
| $onSubmitResponse    | 成功回调             | `Function` | `--`   |
| $onSubmitError       | 失败回调             | `Function` | `--`   |
| $toastSuccessMessage | 成功提示文案         | `string`   | `--`   |
| $toastErrorMessage   | 失败提示文案         | `string`   | `--`   |

### fetchOptionsAction API

接口获取选项内容

| 参数     | 说明                                             | 类型     | 默认值 |
| -------- | ------------------------------------------------ | -------- | ------ |
| name     | 选项内容关联controls - name                      | `string` | `--`   |
| action   | action                                           | `string` | `--`   |
| payload  | 请求参数                                         | `Object` | `--`   |
| fetchKey | fetch[0]为value对应字段，fetch[1]为label对应字段 | `Array`  | `--`   |

## DuFormItem

表单项展示 - 可直接使用不通过 createBaseForm

通过配置生成表单单项内容

## 功能说明

1. 配置表单

2. 展示表单数据

3. 改变表单布局

## 使用方法

```javascript static
/**
 * control {Object} 每一个item的配置
 * option {Object} 表单项的配置
 * results {Object} 表单默认数据
 */
<DuFormItem
    control={control}
    option={option}
    formData={formData}
/>
```

## control - 配置项

```javascript static
// 基本配置
{
    type: 'input',                          /* 必传:
                                                text: 纯展示文案,
                                                custom: 自定义组件,
                                                rangePicker: 日历,
                                                input: 输入框,
                                                select: 下拉框,
                                                radio: 单选,
                                                cascader: 级联选择器,
                                                upload: 上传,
                                                button: 按钮,
                                                checkbox: 复选框
                                            */
    name: 'id',                             // 必传: 表单控件唯一标志
 
 
    label: '序号',
    disabled: true,
    rules: [{required: true, message: '请输入'}]        // 同antd
    extra: '',                              // 额外的提示信息
    events: {                               // key值为事件名
        onChange: e => console.log(e.target.value),
        onBlur: e => this.handleConfirmBlur(e)
    },
    style: {},                              // 自定义样式
    onDisplay: []                           // 是否展示[] <Array> -> <Object>
                                            // {
                                            //     name         - string - 关联controls - name
                                            //     relation     - 与前面所有项的关系（&&、||、 ''）
                                            //     content      - Array -> Object 匹配表达式
                                            //                  - {
                                            //                      relation,
                                            //                      exp,      - 表达式（===、!==、>、<、>=、<=、in、no-in)
                                            //                      value     - 值
                                            //                    }
                                            // }
}

// 额外配置项
{
    config: {               // 额外配置
                            // 1. button - <Array>
                            // [{
                            //     type: 'submit',    // 如果需要触发表单Form - submit事件
                            //     skin: 'primary',
                            //     text: '创建',
                            //     config: {},
                            //     event: {}
                            // }]
                            // 2. 其他
 
        placeholder: '',
 
        subType,            // input - 必传 - <String> -> number, text, textarea
 
        options: [],        // select, radio, cascader - 必传 - <Array>
 
        content: (),        // checkbox - 必传 - <TPL>
 
        fileList,           // upload - <Array> 文件list
                            // {
                            //     uid: '1',
                            //     name: 'xxx.png',
                            //     url: 'http://localhost:3000/8097111c196697377a697034d00c9beb'
                            // }
    }
}
```

## control - api

| 参数     | 说明                                                                                                                                                                              | 类型   | 默认值 |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------ |
| name     | 表单控件唯一标志                                                                                                                                                                  | string | `--`   |
| type     | 表单项类型:text: 纯展示文案,custom: 自定义组件,rangePicker:<br/>日历,input: 输入框,select: 下拉框,radio: 单选,cascader: 级联选择器<br/>upload: 上传,button: 按钮,checkbox: 复选框 | string | `--`   |
| label    |                                                                                                                                                                                   | string | `--`   |
| disabled |                                                                                                                                                                                   | bool   | `--`   |
| rules    | 表单校验规则，同antd                                                                                                                                                              | Array  | `--`   |
| extra    | 额外的提示信息                                                                                                                                                                    | string | `--`   |
| events   | 事件（key值为事件名）                                                                                                                                                             | Object | `--`   |
| style    | 自定义样式                                                                                                                                                                        | Object | `--`   |

### onDisplay API

| 参数               | 说明                                            | 类型          | 默认值 |
| ------------------ | ----------------------------------------------- | ------------- | ------ |
| name               | 关联controls - name                             | string        | `--`   |
| relation           | 与前面所有项的关系（'&&'、'&#124; &#124;'  ''） | string        | `--`   |
| content            | 匹配表达式                                      | Array[Object] | `--`   |
| content - relation |                                                 | string        | `--`   |
| content - exp      | 表达式（===、!==、>、<、>=、<=、in、not-in)     | string        | `--`   |
| content - value    | 匹配值                                          |               | `--`   |

### config API

| 参数        | 说明                                   | 类型   | 默认值 |
| ----------- | -------------------------------------- | ------ |
| placeholder |                                        | string | `--`   |
| subType     | input - 必传 -> number, text, textarea | string | `--`   |
| options     | select, radio, cascader - 必传         | Array  | `--`   |
| content     | checkbox - 必传                        | TPL    | `--`   |
| fileList    | upload - Array 文件list                | Object | `--`   |

## option - 表单 Form 的基本配置

```javascript static
{
    libs: {
        getFieldDecorator           // 必传: Form(this.props)
    },
    layouts: {
        formItemLayout              // <Object>
        formItemEmptyLabelLayout    // <Object>
    }
}
```

## formData - 表单回填数据

```javascript static
{
    id: 1             // “key”值与control里“name”保持一致
}
```

## 参考文档

<https://react-app-common.now.baidu-int.com/#/%E4%B8%9A%E5%8A%A1%E7%BB%84%E4%BB%B6/CreateBaseForm>
