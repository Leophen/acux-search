---
title: useForm
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

用于配置自定义表单的 hooks。

## 引入

```js
import {HooksForm, useForm} from 'baidu-acu-react-common';
```

## 基本用法

```jsx live fff
function App() {
    const controls = (props, options) => {
        return [
            {
                type: 'radio',
                name: 'trainMethod',
                label: '训练方式',
                defaultValue: 'standAlone',
                config: {
                    options: [
                        {label: '单机模型', value: 'standAlone'},
                        {label: '分布式模型', value: 'distributed'}
                    ]
                },
                rules: [{required: true, message: '请选择训练方式'}]
            },
            {
                type: 'input',
                name: 'datasetId',
                label: '数据集',
                config: {
                    subType: 'text',
                    placeholder: '请输入数据集',
                    limitLength: 50
                },
            },
            {
                type: 'input',
                name: 'name',
                label: '任务名称',
                config: {
                    subType: 'text',
                    placeholder: '请输入任务名称',
                    limitLength: 50
                },
                rules: [
                    {required: true, message: '任务名称不可为空'}
                ],
                extra: '中英文、数字和下划线组成，不能以下划线开头，2-50个字符',
                infoIcon: {
                    tooltipProps: {
                        title: '时序预测任务暂且只支持单机模型训练'
                    }
                }
            },
            {
                type: 'input',
                name: 'splitRatio',
                label: '拆分比例',
                defaultValue: 0.8,
                config: {
                    subType: 'number',
                    placeholder: '请输入拆分比例',
                    step: 0.1,
                    min: 0.1,
                    max: 0.9
                },
                rules: [
                    {required: true, message: '请填写拆分比例'},
                    {pattern: /^0\.[1-9]$/, message: '请输入0-1之间的数,最多保留1位小数'}
                ]
            }
        ];
    };

    const ProForm = React.forwardRef((props, ref) => {
        const options = {
            controls,
            formItemOption: {
                noStyle: true
            }
        };
        const {formRef, formProps} = useForm(ref, {...props}, options);

        const moreSettingCollapsed = {
            label: 'datasetId',
            defaultExpand: false
        };

        return (
            <HooksForm
                title="表单标题"
                description="表单描述"
                moreSettingCollapsed={moreSettingCollapsed}
                wrappedComponentRef={formRef}
                {...formProps}
            />
        );
    });

    return (
        <ProForm />
    );
}
```

## API

### useForm 参数

| 参数    | 说明       | 类型             | 默认值 |
| ------- | ---------- | ---------------- | ------ |
| ref     | forwardRef | `any`            | `--`   |
| props   | props      | `any`            | `--`   |
| options | 配置数据   | `UseFormOptions` | `--`   |

### UseFormOptions

| 参数            | 说明                                             | 类型             | 默认值 |
| --------------- | ------------------------------------------------ | ---------------- | ------ |
| type            | 类型，只在分步表单时传入step                     | `string`         | `--`   |
| controls        | 表单项配置方法                                   | `ControlsType`   | `--`   |
| actionConfig    | 初始化 fetch / options配置 / submit 提交数据请求 | `ActionConfig`   | `--`   |
| customFunctions | 自定义方法                                       | `object`         | `--`   |
| formItemOption  | formItem 表单项参数                              | `object`         | `--`   |
| stepConfig      | 分步表单额外配置                                 | `StepFormConfig` | `--`   |

```mdx-code-block
<Tabs>
<TabItem value="类型概览">
```

```ts
/**
 * 表单项配置方法类型
 */
type ControlsType = (
  props: HooksFormProps,
  options: object,
  customFunctions: object,
  values: object
) => DuFormItemControl[] | StepControls[];

/**
 * 初始化 fetch / options配置 / submit 提交数据请求类型
 */
export interface ActionConfig {
    fetchDataAction?: FetchDataAction;
    fetchOptionsAction?: FetchOptionsAction[];
    submitAction?: SubmitAction;
}

/**
 * 分步表单额外配置类型
 */
export interface StepFormConfig {
    prevText?: string;
    prevClick?: () => boolean;
    nextText?: string;
    nextClick?: (formData: object) => boolean;
    endText?: string;
    isSavedRealTime?: boolean;
}
```

```mdx-code-block
</TabItem>
<TabItem value="类型详情">
```

```ts
export interface DuFormItemControl {
    type: string; // 表单项类型
    name?: string; // 表单项名称
    label?: string;
    disabled?: boolean; // 是否禁用
    rules?: any[]; // antd 校验规则
    extra?: string; // 额外提示帮助信息
    events?: object;
    style?: object;
    defaultValue?: any;
    onDisplay?: OnDisplayItem[]; // 显示的条件
    config?: object[] | object;
    dynamic?: boolean | object;
    content?: React.ComponentType<any>;
}

export interface StepControls {
    title: string;
    controls: DuFormItemControl[];
}
```

```mdx-code-block
</TabItem>
</Tabs>
```

### HooksFormProps

| 参数                | 说明                                          | 类型                        | 默认值 |
| ------------------- | --------------------------------------------- | --------------------------- | ------ |
| className           | 类名                                          | `string`                    | `--`   |
| title               | 页面大标题                                    | `string`〡`React.component` | `--`   |
| type                | 表单类型（normal / step）                     | `string`                    | `--`   |
| controlsConfig      | 表单项配置结果                                | `DuFormItemControl[]`       | `--`   |
| formData            | 传入 formData 及 fetchData 的合并结果         | `object`                    | `--`   |
| doSubmit            | 提交方法                                      | `() => void`                | `--`   |
| stepIndex           | 在分步表单 (type = step) 情况下，当前步骤数   | `number`                    | `--`   |
| stepButtonConfig    | 在分步表单 (type = step) 情况下，按钮渲染配置 | `() => DuFormItemControl[]` | `--`   |
| formItemOptionMerge | 处理后的 formItem 表单项参数                  | `object`                    | `--`   |

### actionConfig > fetchDataAction

| 参数                 | 说明                   | 类型                       | 默认值 |
| -------------------- | ---------------------- | -------------------------- | ------ |
| formData             | 非接口直接传值给 form  | `object`                   | `--`   |
| fetchFormAction      | 接口获取表单数据       | `string`                   | `--`   |
| fetchFormPayload     | 接口参数               | `object`                   | `--`   |
| $onFetchFormRequest  | 请求发出前钩子函数     | `(params: object) => void` | `--`   |
| $onFetchFormResponse | 请求返回成功后钩子函数 | `(data: object) => void`   | `--`   |

### actionConfig > fetchOptionsAction[]

| 参数                    | 说明                                                            | 类型                      | 默认值 |
| ----------------------- | --------------------------------------------------------------- | ------------------------- | ------ |
| name                    | 获取后在 controls 中 options 里的 key                           | `string`                  | `--`   |
| action                  | 接口获取选项数据的 action                                       | `string`                  | `--`   |
| payload                 | 接口获取选项数据的请求参数                                      | `object`                  | `--`   |
| fetchKey                | fetchKey[0] 为 value 对应字段<br/>fetchKey[1] 为 label 对应字段 | `array`                   | `--`   |
| $onFetchOptionsResponse | 请求返回成功后钩子函数                                          | `(options: array) => any` | `--`   |

### actionConfig > submitAction

| 参数                 | 说明                   | 类型                       | 默认值 |
| -------------------- | ---------------------- | -------------------------- | ------ |
| submitFormAction     | submit提交接口         | `string`                   | `--`   |
| payload              | 额外的请求参数         | `string[]`                 | `--`   |
| $onSubmitRequest     | 请求发出前钩子函数     | `(params: object) => void` | `--`   |
| $onSubmitResponse    | 请求返回成功后钩子函数 | `(data: object) => void`   | `--`   |
| $onSubmitError       | 请求返回失败后钩子函数 | `(error: object) => void`  | `--`   |
| $toastSuccessMessage | 成功提示文案           | `string`                   | `--`   |
| $toastErrorMessage   | 失败提示文案           | `string`                   | `--`   |

### control > common

DuFormItem 的功能：

- 配置表单
- 展示表单数据
- 改变表单布局

| 参数         | 说明                                      | 是否必填                                    | 类型 |
| ------------ | ----------------------------------------- | ------------------------------------------- | ---- |
| type         | 表单项类型                                | `string`                                    | `--` |
| name         | 表单控件唯一标志                          | `string`                                    | `--` |
| label        | 控件 label                                | `string`                                    | `--` |
| disabled     | 是否不可用                                | `boolean`                                   | `--` |
| defaultValue | 默认值                                    | `string`                                    | `--` |
| extra        | 额外的提示信息                            | `string`                                    | `--` |
| dynamic      | 可增删控件相关配置(可配置 true 或 object) | `{max, min, rules}`                         | `--` |
| rules        | 表单校验规则，同 antd                     | `Array`                                     | `--` |
| events       | 事件（key 值为事件名）                    | `Object`                                    | `--` |
| style        | 自定义样式                                | `Object`                                    | `--` |
| onDisplay    | 联动配置                                  | `OnDisplayItem[]`                           | `--` |
| config       | 其他配置                                  | `{subType, placeholder, options, fileList}` | `--` |
| content      | 其他配置                                  | `自定义组件内容`                            | `--` |

### control > type

| 类型        | 说明         | 子类型                                                   |
| ----------- | ------------ | -------------------------------------------------------- |
| text        | 纯展示文案   | `--`                                                     |
| rangePicker | 日历         | `--`                                                     |
| input       | 输入框       | `config: {subType: ' - / number / textarea / password'}` |
| select      | 下拉框       | `config: {mode: ' - /multiple / tags'}`                  |
| radio       | radio 选择框 | `config: {subType: ' - / button'}`                       |
| checkbox    | 复选框       | `config.options存在为多选`                               |
| cascader    | 级联选择器   | `--`                                                     |
| upload      | 上传         | `--`                                                     |
| custom      | 自定义组件   | `--`                                                     |
| button      | 按钮         | `--`                                                     |

### control > onDisplay

| 参数     | 说明                                              | 类型                                                                             |
| -------- | ------------------------------------------------- | -------------------------------------------------------------------------------- |
| name     | 关联 controls - name                              | `string`                                                                         |
| relation | 与前面所有项的关系（`&&`、`&#124; &#124;`  `''`） | `string`                                                                         |
| content  | 匹配表达式                                        | `{relation, exp: '=== / !== / > / < / >= / <= / in / not-in / custom', value}[]` |

## 参考文档

<https://react-app-common.now.baidu-int.com/#/hooks/UseForm>
