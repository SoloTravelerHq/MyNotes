##  Express

### 简介

- 基于Node.js平台的一个快速、开放、极简的web开发框架，就是一个npm上的第三方包，提供了快速创建Web服务器的便捷方法
- Node的内置模块http也可以创建Web服务器，但是用起来复杂、开发效率低，Express是基于http模块进一步封装的，极大的提高了开发效率

### 安装

- 在终端输入npm i express
- 使用

```js
//导入express
const express = require('express')
// 创建web服务器
const app = express()
// 启动web服务器
app.listen(8081,() => {
  console.log('启动成功');
})
```

### req

- req.query：可以访问到客户端通过查询字符串的形式发送到服务器的参数
- req.params：可以访问到URL中的动态参数

### express.static()

- express.static()可以非常方便的创建一个静态资源服务器，是express的内置中间件，app.use(express.static('文件路径'))
- 可以在前面加个路径前缀，app.use('路径前缀', express.static('文件路径'))

### nodemon

- nodemon可以替换node命令启动项目，之后修改了node项目后，nodemon会自动重新启动项目
- 使用npm i nodemon -g进行全局安装

### 路由

- 导入express
- 创建路由对象：const router = express.Router()
- 挂载路由：router.get()
- 向外导出路由对象：module.exports = router

### 中间件

- 业务处理过程中的处理环节，有输入输出，上一级的输入作为下一级的输出

- 多个中间件共享一份req、res。为此可以在上游中间件中统一为req、res对象自定义属性和方法供下游中间件火或路由使用

- 局部中间件只在当前路由生效，即先定义中间件函数，在请求方法中加入该中间件

  - ```js
    // 局部中间件
    const mw = function(req,res,next){
      console.log('局部中间件')
      next()
    }
    //当前路由生效
    router.get('/',mw,(req,res) => {
      res.send('router')
    })
    ```

    

- 用app绑定的中间件称作应用级别中间件，用router绑定的中间件称作路由级别中间件
- 错误级别中间件用来捕获整个项目中发生的异常错误，从而防止程序崩溃，必须注册在所有路由之后。
  - 格式：app.use(function(err,req,res,next){console.log(err.message)})
- ![image-20220305175515132](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220305175515132.png)

- 使用第三方中间件时需要先安装，再用require导入，再用app.use注册

### 接口跨域问题

- 在编写接口时，出现协议不同时会出现跨域问题，可以采用CORS（主流方案），而一般不采用JSONP（有缺陷的方案，只支持GET请求）
- 安装npm i cors，使用require导入，再使用app.use(cors())注册
- CORS（跨域资源共享）由一系列HTTP响应头组成，这些HTTP响应头决定浏览器是否阻止JS代码跨域获取资源
- 浏览器的同源安全策略默认会阻止网页“跨域”获取资源。
- CORS主要在服务器端配置，客户端浏览器无须做任何额外配置
- CORS在浏览器中有兼容性，只支持XMLHttpRequest Level2的浏览器，如IE10+、Chrome4+、Firefox3.5+
- 简单请求：请求方式质保函get、post、head三者之一；http头部信息不能超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain）
- 预检请求：请求方式不再以上的三者之内；请求头包含自定义头部字段；向服务器发送了application/json。发生预检请求时，浏览器在于服务器正式通信之前，浏览器会先发送OPTION请求进行预检，以获知服务器是否允许该请求，服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据
