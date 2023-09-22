---
title: DatePicker 日期选择器
---

输入或选择日期的控件。

当用户需要输入一个日期，可以点击标准输入框，弹出日期面板进行选择。

## 引入

```js
import {DatePicker} from 'acud';
import moment from 'moment';
```

## 基本用法

```jsx live fff
function App() {
    const dateFormat = 'YYYY-MM-DD';
    const [value, setValue] = useState(moment('2023-06-26', dateFormat));

    const handleChange = (moment) => {
        console.log(moment);
        setValue(moment);
    };

    return (
        <div className="acux-demo-column">
            <h5>无默认值</h5>
            <DatePicker />

            <h5>有默认值（非受控）</h5>
            <DatePicker defaultValue={value} />

            <h5>有固定值（受控）</h5>
            <DatePicker value={value} />

            <h5>通用方法</h5>
            <DatePicker value={value} onChange={handleChange} />
        </div>
    );
}
```

## 禁用状态

```jsx live fff
<DatePicker disabled />
```

## 不同类型

```jsx live fff
<div className="acux-demo-column">
    <h5>time</h5>
    <DatePicker picker='time' />

    <h5>date</h5>
    <DatePicker picker='date' />

    <h5>month</h5>
    <DatePicker picker='month' />

    <h5>year</h5>
    <DatePicker picker='year' />

    <h5>decade</h5>
    <DatePicker picker='decade' />

    <h5>quarter</h5>
    <DatePicker picker='quarter' />
</div>
```

## 不同状态

```jsx live fff
<DatePicker status="error" />
```

## 隐藏面板

```jsx live fff
<div className="acux-demo-column">
    <DatePicker />
    <DatePicker showToday={false} />
    <DatePicker showTime />
    <DatePicker showTime showNow={false} />
</div>
```

## 带时间的日期选择

```jsx live fff
<DatePicker showTime />
```

## 范围选择器

```jsx live fff
function App() {
    const dateFormat = 'YYYY-MM-DD';

    const {RangePicker} = DatePicker;

    return (
        <div className="acux-demo-column">
            <RangePicker locale={locale} />
            <RangePicker
                locale={locale}
                ranges={{
                    今天: [moment(), moment()],
                    '本月': [moment().startOf('month'), moment().endOf('month')]
                }}
            />
            <RangePicker locale={locale} showTime />
            <RangePicker locale={locale} picker="month" />
            <RangePicker locale={locale} picker='week' />
        </div>
    );
}
```

## 选择器汉化

引入：

```js
import locale from 'acud/es/date-picker/locale/zh_CN';
```

使用：

```jsx live fff
<div className="acux-demo-column">
    <DatePicker />
    <DatePicker locale={locale} />
</div>
```

国际化：

```jsx
// 默认语言为 en-US，如果你需要设置其他语言，推荐在入口文件全局设置 locale
import moment from 'moment';
import 'moment/locale/zh-cn';
import locale from 'acud/lib/locale/zh_CN';

<ConfigProvider locale={locale}>
    <DatePicker defaultValue={moment('2023-06-26', 'YYYY-MM-DD')} />
</ConfigProvider>;
```

## API

以下 API 为 DatePicker、 RangePicker 共享的 API。

| 参数              | 说明                                                          | 类型                                                              | 默认值     |
| ----------------- | ------------------------------------------------------------- | ----------------------------------------------------------------- | ---------- |
| allowClear        | 是否显示清除按钮                                              | `boolean`                                                         | `true`     |
| autoFocus         | 自动获取焦点                                                  | `boolean`                                                         | `false`    |
| bordered          | 是否有边框                                                    | `boolean`                                                         | `true`     |
| className         | 选择器 className                                              | `string`                                                          | `--`       |
| dateRender        | 自定义日期单元格的内容                                        | `function(currentDate: moment, today: moment) => React.ReactNode` | `--`       |
| disabled          | 禁用                                                          | `boolean`                                                         | `false`    |
| disabledDate      | 不可选择的日期                                                | `(currentDate: moment) => boolean`                                | `--`       |
| dropdownClassName | 额外的弹出日历 className                                      | `string`                                                          | `--`       |
| getPopupContainer | 定义浮层的容器，默认为 body 上新建 div                        | `function(trigger)`                                               | `--`       |
| inputReadOnly     | 设置输入框为只读（避免在移动设备上打开虚拟键盘）              | `boolean`                                                         | `false`    |
| locale            | 国际化配置                                                    | `object`                                                          | `默认配置` |
| mode              | 日期面板的状态                                                | `time`〡`date`〡`month`〡`year`〡`decade`                         | `--`       |
| open              | 控制弹层是否展开                                              | `boolean`                                                         | `--`       |
| panelRender       | 自定义渲染面板                                                | `(panelNode) => ReactNode`                                        | `--`       |
| picker            | 设置选择器类型                                                | `date`〡`week`〡`month`〡`quarter`〡`year`                        | `date`     |
| placeholder       | 输入框提示文字                                                | `string〡[string, string]`                                        | `--`       |
| popupStyle        | 额外的弹出日历样式                                            | `CSSProperties`                                                   | `{}`       |
| size              | 输入框大小，`large` 高度为 40px，`small` 为 24px，默认是 32px | `large`〡`middle`〡`small`                                        | `--`       |
| style             | 自定义输入框样式                                              | `CSSProperties`                                                   | `{}`       |
| suffixIcon        | 自定义的选择框后缀图标                                        | `ReactNode`                                                       | `--`       |
| onOpenChange      | 弹出日历和关闭日历的回调                                      | `function(open)`                                                  | `--`       |
| onPanelChange     | 日历面板切换的回调                                            | `function(value, mode)`                                           | `--`       |

### 共同的方法

| 名称    | 描述     |
| ------- | -------- |
| blur()  | 移除焦点 |
| focus() | 获取焦点 |

### DatePicker

| 参数                  | 说明                                                                                                               | 类型                                                                         | 默认值                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------- | --------------------- |
| defaultPickerValue    | 默认面板日期                                                                                                       | [moment](http://momentjs.com/)                                               | `--`                  |
| defaultValue          | 默认日期，如果开始时间或结束时间为 `null` 或者 `undefined`，日期范围将是一个开区间                                 | [moment](http://momentjs.com/)                                               | `--`                  |
| disabledTime          | 不可选择的时间                                                                                                     | `function(date)`                                                             | `--`                  |
| format                | 设置日期格式，为数组时支持多格式匹配，展示以第一个为准。配置参考 [moment.js](http://momentjs.com/)，支持自定义格式 | ` string〡(value: moment) => string〡(string〡(value: moment) => string)[] ` | ``YYYY-MM-DD``        |
| renderExtraFooter     | 在面板中添加额外的页脚                                                                                             | `(mode) => React.ReactNode`                                                  | `--`                  |
| showNow               | 当设定了 `showTime` 的时候，面板是否显示“此刻”按钮                                                                 | `boolean`                                                                    | `--`                  |
| showTime              | 增加时间选择功能                                                                                                   | `Object〡boolean`                                                            | `[TimePicker Options` |
| showTime.defaultValue | 设置用户选择日期时默认的时分秒                                                                                     | [moment](http://momentjs.com/)                                               | `moment()`            |
| showToday             | 是否展示“今天”按钮                                                                                                 | `boolean`                                                                    | `true`                |
| value                 | 日期                                                                                                               | [moment](http://momentjs.com/)                                               | `--`                  |
| onChange              | 时间发生变化的回调                                                                                                 | `function(date: moment, dateString: string)`                                 | `--`                  |
| onSelect              | 输入框时间发生变化的回调                                                                                           | `function(date: moment)`                                                     | `--`                  |
| onOk                  | 点击确定按钮的回调                                                                                                 | `function()`                                                                 | `--`                  |
| onPanelChange         | 日期面板变化时的回调                                                                                               | `function(value, mode)`                                                      | `--`                  |

### DatePicker[picker=year]

| 参数               | 说明                                                       | 类型                                         | 默认值 |
| ------------------ | ---------------------------------------------------------- | -------------------------------------------- | ------ |
| defaultPickerValue | 默认面板日期                                               | [moment](http://momentjs.com/)               | `--`   |
| defaultValue       | 默认日期                                                   | [moment](http://momentjs.com/)               | `--`   |
| format             | 展示的日期格式，配置参考 [moment.js](http://momentjs.com/) | `string`                                     | `YYYY` |
| renderExtraFooter  | 在面板中添加额外的页脚                                     | `() => React.ReactNode`                      | `--`   |
| value              | 日期                                                       | [moment](http://momentjs.com/)               | `--`   |
| onChange           | 时间发生变化的回调，发生在用户选择时间时                   | `function(date: moment, dateString: string)` | `--`   |

### DatePicker[picker=quarter]

`4.1.0` 新增。

| 参数               | 说明                                                       | 类型                                         | 默认值     |
| ------------------ | ---------------------------------------------------------- | -------------------------------------------- | ---------- |
| defaultPickerValue | 默认面板日期                                               | [moment](http://momentjs.com/)               | `--`       |
| defaultValue       | 默认日期                                                   | [moment](http://momentjs.com/)               | `--`       |
| format             | 展示的日期格式，配置参考 [moment.js](http://momentjs.com/) | `string`                                     | `YYYY-\QQ` |
| renderExtraFooter  | 在面板中添加额外的页脚                                     | () => `React.ReactNode`                      | `--`       |
| value              | 日期                                                       | [moment](http://momentjs.com/)               | `--`       |
| onChange           | 时间发生变化的回调，发生在用户选择时间时                   | `function(date: moment, dateString: string)` | `--`       |

### DatePicker[picker=month]

| 参数               | 说明                                                       | 类型                                         | 默认值    |
| ------------------ | ---------------------------------------------------------- | -------------------------------------------- | --------- |
| defaultPickerValue | 默认面板日期                                               | [moment](http://momentjs.com/)               | `--`      |
| defaultValue       | 默认日期                                                   | [moment](http://momentjs.com/)               | `--`      |
| format             | 展示的日期格式，配置参考 [moment.js](http://momentjs.com/) | `string`                                     | `YYYY-MM` |
| monthCellRender    | 自定义的月份内容渲染方法                                   | `function(date, locale): ReactNode`          | `--`      |
| renderExtraFooter  | 在面板中添加额外的页脚                                     | `() => React.ReactNode`                      | `--`      |
| value              | 日期                                                       | [moment](http://momentjs.com/)               | `--`      |
| onChange           | 时间发生变化的回调，发生在用户选择时间时                   | `function(date: moment, dateString: string)` | `--`      |

### DatePicker[picker=week]

| 参数               | 说明                                                       | 类型                                         | 默认值    |
| ------------------ | ---------------------------------------------------------- | -------------------------------------------- | --------- |
| defaultPickerValue | 默认面板日期                                               | [moment](http://momentjs.com/)               | `--`      |
| defaultValue       | 默认日期                                                   | [moment](http://momentjs.com/)               | `--`      |
| format             | 展示的日期格式，配置参考 [moment.js](http://momentjs.com/) | `string`                                     | `YYYY-wo` |
| renderExtraFooter  | 在面板中添加额外的页脚                                     | `(mode) => React.ReactNode`                  | `--`      |
| value              | 日期                                                       | [moment](http://momentjs.com/)               | `--`      |
| onChange           | 时间发生变化的回调，发生在用户选择时间时                   | `function(date: moment, dateString: string)` | `--`      |

### RangePicker

| 参数                  | 说明                                             | 类型                                                                                                               | 默认值                 |
| --------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ | ---------------------- |
| allowEmpty            | 允许起始项部分为空                               | `[boolean, boolean]`                                                                                               | `[false, false]`       |
| dateRender            | 自定义日期单元格的内容。`info` 参数自 4.3.0 添加 | `function(currentDate: moment, today: moment, info: { range: start〡end }) => React.ReactNode`                     | `--`                   |
| defaultPickerValue    | 默认面板日期                                     | [moment](http://momentjs.com/)[]                                                                                   | `--`                   |
| defaultValue          | 默认日期                                         | [moment](http://momentjs.com/)[]                                                                                   | `--`                   |
| disabled              | 禁用起始项                                       | `[boolean, boolean]`                                                                                               | `--`                   |
| disabledTime          | 不可选择的时间                                   | `function(date: moment, partial:`start`〡`end`)`                                                                   | `--`                   |
| format                | 展示的日期格式                                   | `string`                                                                                                           | `YYYY-MM-DD HH:mm:ss`  |
| ranges                | 预设时间范围快捷选择                             | { [range: string]: [moment](http://momentjs.com/)[] }〡{ [range: string]: () => [moment](http://momentjs.com/)[] } | `--`                   |
| renderExtraFooter     | 在面板中添加额外的页脚                           | `() => React.ReactNode`                                                                                            | `--`                   |
| separator             | 设置分隔符                                       | `string`                                                                                                           | `~`                    |
| showTime              | 增加时间选择功能                                 | `Object〡boolean`                                                                                                  | `TimePicker Options`   |
| showTime.defaultValue | 设置用户选择日期时默认的时分秒                   | [moment](http://momentjs.com/)[]                                                                                   | `[moment(), moment()]` |
| value                 | 日期                                             | [moment](http://momentjs.com/)[]                                                                                   | `--`                   |
| onCalendarChange      | 待选日期发生变化的回调。`info` 参数自 4.4.0 添加 | `function(dates: [moment, moment], dateStrings: [string, string], info: { range:start〡end })`                     | `--`                   |
| onChange              | 日期范围发生变化的回调                           | `function(dates: [moment, moment], dateStrings: [string, string])`                                                 | `--`                   |
