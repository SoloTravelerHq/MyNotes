## JSON

- JSON是一个特殊的字符串，可以被任意语言识别，并且可以转换为任意语言的对象，JSON在开发中主要用于数据交互

- JSON中的属性名必须加双引号

- JSON包函对象{}，数组[]

- JSON中允许的值有：字符串、数值、布尔值、null、对象、数组

- ```js
  var json = '{"name":"hq","age":16,"obj":{}}'
  ```

- JSON.parse()：可以将JSON字符串转换成js对象
- JSON.stringify()：可以将js对象转换成JSON字符串
- IE7及以下不支持JSON
- eval()：可以执行一段字符串形式的代码，如果不希望将其代码块解析，则需要在字符串前后加一个（）；该函数一般不用，性能差且不安全。
- 解决IE7及以下版本兼容性问题是引用js文件（json2.js）