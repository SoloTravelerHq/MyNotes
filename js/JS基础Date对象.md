## JS基础Date对象

```js
//创建一个日期对象
var d = new Date()
//指定日期 "月/日/年 时:分:秒"
var d2 = new Date("01/01/2022 00:00:00")
//获取当前日期是几号
var d3 = d2.getDate();//输出：01
//获取当前日期是周几（0表示周日）
var d4 = d2.getDay();//输出：6
//getTime()获取时间戳：从格林威治标准时间1970年01月01号 00:00:00到当前日期的毫秒数
//可以用时间戳来测试代码执行时间
var start = Date.now()
{....}
var end = Date.now()
console.log(end-start)
```

## JS基础Math

Math不是构造函数，它是一个类，里面封装了很多跟数学相关的属性和方法，直接用Math.

## 包装类

String()、Number()、Boolean()是三个对象，开发时不用，但是在数据转换时，js会自动调用

```js
//number类型转string
var a = 123;
//此时，a会先转为String()对象
var b = a.toString()
```

## 字符串的方法

- indexOf("a")返回a第一次出现的字符的位置

- indexOf("a",2)从指定位置开始查找
- substring(开始截取，结束截取)与slice类似，substring不能传负数，如果开始截取位置大于结束截取位置，substring会自动调整位置
- substr(开始截取，截取数量)
- split将字符串拆分成数组str.split(",")根据逗号分隔
- toUpperCase将字符串转换为大写
- toLowerCase将字符串转换成小写