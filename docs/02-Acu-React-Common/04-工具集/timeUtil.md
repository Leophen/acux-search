---
title: timeUtil
---

时间转换工具。

## 引入

```js
import {timeUtil} from 'baidu-acu-react-common';
```

## timeToUtc()

```js
timeUtil.timeToUtc('2018-07-01')
// 2018-06-30T16:00:00Z

timeUtil.timeToUtc('2018-07-01 00:00')
// 2018-06-30T16:00:00Z
```

## getStartTime()

```js
timeUtil.getStartTime('2018-07-01')
// 2018-07-01 00:00:00
```

## getEndTime()

```js
timeUtil.getEndTime('2018-07-01')
// 2018-07-01 23:59:59
```

## getMonthFirstDay()

```js
timeUtil.getMonthFirstDay('2018-07-13')
// 2018-07-01
```

## toTime()

```js
timeUtil.toTime('2018-11-30T16:00:00Z')
// 2018-12-01 00:00:00
```

## toDate()

```js
timeUtil.toDate('2018-11-30T16:00:00Z')
// 2018-12-01

timeUtil.toDate('2018-11-30 16:00:00')
// 2018-11-30
```

## formatTimeRange()

```js
timeUtil.formatTimeRange(['2017-07-01', '2017-08-01'])
// ['2017-06-30T16:00:00Z' '2017-08-01T15:59:59Z']
```

## durationBySecond()

```js
timeUtil.durationBySecond(59)
// 00:59

timeUtil.durationBySecond(70)
// 01:10

timeUtil.durationBySecond(3601)
// 01:00:01
```
