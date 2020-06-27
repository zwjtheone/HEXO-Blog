---
title: moment-quick-check 
date: 2019/10/18 21:40 
updated: 2019/10/18 21:40 
tags: 
    - moment

---

# 获取时间

```javascript
moment().valueOf()  // 获取时间戳(以毫秒为单位) 

moment().startOf('day')   // 获取今天0时0分0秒
moment().startOf('isoWeek')  // 获取本周周一0时0分0秒
moment().startOf('month')  // 获取本月第一天0时0分0秒

moment().endOf('day')   // 获取今天23时59分59秒
moment().endOf('isoWeek')  // 获取本周周日23时59分59秒
moment().endOf('month')   // 获取本月最后一天23时59分59秒

moment().year()       //   获取当前年份
moment().month()   //   获取当前月（ 0~11, 0 =>1月, 11=>12月）
moment().date()     //  获取今天
moment().day()      // 获取当前星期 (0~6, 0: 周日, 6: 周六)

moment().daysInMonth()  // 获取本月的总天数

moment().month(moment().month() - 1).startOf('month').valueOf()   //  上个月1号的00:00:00
moment().month(moment().month() - 1).endOf('month').valueOf()    //  上个月最后一天的23:59:59

moment().month(moment().month() - 1).startOf('month').valueOf()   //  上个季度第一个月1号的00:00:00
moment().month(moment().month() - 1).endOf('month').valueOf()    //  上个季度最后一个月最后一天的23:59:59
```

# 格式化时间

```javascript
moment().format('YYYY-MM-DD')
moment().format('hh:mm:ss a')    //  格式化时分秒(12小时制)
moment().format('x')    // 格式化时间戳(以毫秒为单位)
```

# 转化为JS原生Date对象

```javascript
moment().toDate()
new Date(moment())
```
# 设置时间

```javascript
moment().year(2019)       //   设置年
moment().month(9)   //   设置月（ 0~11, 0 =>1月, 11=>12月）
moment().date(2)     //  设置日期
moment().isoWeekday(1) // 设置日期为本周周一

moment().add(1, 'years')    //  设置下一年
moment().add(1, 'months')   // 设置下一月
moment().add(1, 'days')    //  设置下一天
moment().add(1, 'weeks')    //  设置下一周

moment().subtract(1, 'years')    //  设置上一年
moment().subtract(1, 'months')   // 设置上一月
moment().subtract(1, 'days')    //  设置上一天
moment().subtract(1, 'weeks')    //  设置上一周
```
# 比较时间

```javascript
let startDate = moment().subtract(1, 'weeks')
let endDate = moment()
endDate.diff(startDate)     // 返回毫秒数
 
endDate.diff(startDate, 'months')     // 0
endDate.diff(startDate, 'weeks')      // 1
endDate.diff(startDate, 'days')       // 7
startDate.diff(endDate, 'days')      // -7
```
