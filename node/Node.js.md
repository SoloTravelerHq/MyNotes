## Node.js

- 单线程

### 1、内置模块

- const fs = require('fs')：导入文件模块
  - fs.readFile(路径, ‘utf8’, function(err,dataStr){})：读取文件
  - fs.writeFile(路径, 写入的数据, function(err){})：写入文件
- const path = require('path')：导入path模块
  - path.join(__dirname, '/grades.txt')：拼接路径
  - path.basename()：获取文件路径中的文件名
  - path.extname()：获取文件路径中的文件扩展名
- const http = require('http')：导入http模块
  - http.createServer()：创建web服务器实例
  - server.on('request',function(req, res){})：绑定request事件，监听客户端请求
    - req.url：客户端请求的url地址
    - req.method：客户端请求的method类型（get，post等）
    - res.end()：向客户端发送指定内容，并结束这次请求的处理过程
    -  res.setHeader('Content-Type','text/html;charset=utf-8')：解决中文乱码问题
  - server.listen(8080, function(){})：启动服务器

### 2、module

- module.exports：将模块内的成员共享出去，外界使用require()方法导入自定义模块时，得到的就是module.exports所指的对象
- require()模块时，得到的永远是module.exports指向的对象，但初始时，exports和module.exports指向的是同一个对象。

### 3、npm与包

- npm install 包的完整名称：在项目中安装指定的包，简写为npm i，默认安装最新的版本，若要安装指定版本则在包名后面加上‘@版本号’，如npm i moment@2.24.0
- 包的语义化版本规范：运用点分十进制表示，第一位数字表示大版本的更新，即底层代码的重构；第二位数字表示功能版本的更新；第三个数字表示bug修复更新。
- node_modules文件夹从来存放所有已安装到项目中的包
- package-lock.json配置文件用来记录node_module中每个包的信息
- package.json记录项目中安装了哪些包，包括包的版本、名称、开发期间使用还是部署期间时使用等等
- 使用npm init -y在项目中创建package.json文件，项目文件名不能含有中文和空格
- dependencies：记录项目中安装了哪些包；在运行npm install时会将dependencies中记录的包全部下载下来
- npm uninstall 卸载包
- npm init -y：初始化package文件
- npm i 包名 --save-dev：将包安装在DevDependencies中，表示该包只在项目开发阶段会用到，项目上线时不会用到。简写为npm i 包名 -D
- npm config get registry：查看当前下包的镜像资源服务器地址
- npm config set registry = xxxx：将下包的镜像源切换成淘宝的镜像源
- nrm：用于切换下包资源地址
  - npm i nrm -g：全局安装nrm
  - nrm ls：查看所有可用的镜像资源
  - nrm use taobao：将下包的镜像资源切换为taobao
- ![image-20220222161030239](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220222161030239.png)

### 4、模块加载机制

- 模块第一次加载后会被缓存
- 内置模块加载优先级最高
- 自定义模块加载需要加上./或../否则会被当成内置模块或第三方模块
- 当省略扩展名时，Node会自动补全扩展名，优先确切的文件名、.js、.json、.node、加载失败报错
- 加载第三方模块时，如果在当前目录没找到，则会返回上一级查找，一直找到根目录还未找到则报错
- 当把目录作为模块标识符传递给require()时，有三种加载方式
  - 查找package.js，寻找main属性作为加载入口
  - 如果没有package.js或没有main属性，则Node会视图加载目录下的index.js
  - 若都无则报错

### 5、操作MySQL

- 安装操作MySQL数据库的第三方模块：npm i mysql

- 通过mysql模块连接到数据库

  - ```js
    const mysql = require('mysql')
    const db = mysql.createPool({
      host: '127.0.0.1',
      user: 'root',
      password: 'admin123',
      database: 'my_db_01'
    })
    ```

    

- 通过mysql模块执行SQL语句

  - ```js
    // 需要插入的数据
    const user = {username: 'insert-hq',password: 'hq123'}
    // sql语句，？表示占位
    const sqlInsert = 'insert into users (username,password) values (?,?)'
    // 执行
    db.query(sqlInsert,[user.username,user.password], (err,results) => {
      if(err) return console.log(err.message);
      if(results.affectedRows === 1) console.log('success');
    })
    ```

### 前后端身份认证

- 服务端渲染优缺点
  - 优点：前端耗时少，因为服务器负责动态生成HTML内容，浏览器直接渲染就可以，尤其是移动端，更省电；有利于SEO，因为服务器响应的是完整的HTML页面内容，所以爬虫更容易获取信息
  - 缺点：占用服务器资源，如果请求过多，会对服务器造成一定的访问压力；不利于前后端分离，开发效率低
- 前后端分离的优缺点
  - 优点：开发体验好；用户体验好；减轻了服务器端的渲染压力
  - 缺点：不利于SEO，但是对于Vue、React等前端框架的SSR可解决

### Session认证机制

- Cookie：存储在用户浏览器中的一段不超过4kb的字符串。它由一个名称、一个值即键值对组成和其他几个用于控制Cookie有效期、安全性、使用范围的可选属性组成
  - 特性：自动发送、域名独立、过期时限、4KB限制
- Cookie和Cookie认证的设计理念是Session认证机制的精髓 
- Session的工作原理：客户端提交账号密码—>服务器验证，并将登录成功的用户信息存储在服务器的内存中同时生成对应的Cookie字符串—>浏览器接受服务器响应的Cookie并存储在当前域名下—>客户端再次发送请求时，通过请求头自动把当前域名下所有可用的Cookie发送给服务器—>服务器根据请求头中携带的Cookie从内存中查找对应的用户信息，认证成功后返回特定的响应内容
- Cookie不支持跨域访问，当涉及到前端跨域请求时，需要做许多额外配置，才能实现Session认证

### JWT（JSON Web Token）认证机制

- 目前最流行的跨域认证解决方案
- 工作原理：客户端提交账号密码—>服务端验证，验证通过后将用户信息对象经过加密生成token字符串，并返回给客服端—>浏览器将token字符串存储到LocalStorage或SessionStorage中—>客户端再次发送请求时，通过请求头的Authorization字段，将token发送给服务器—>服务器把token字符串还原成用户信息对象，对用户身份认证成功后生成特定的响应内容发送给浏览器
- JWT由Header、Payload（有效荷载）、Signature（签名）组成
  - Payload部分是真正的用户信息，是加密过后生成的字符串
  - Header和Signature是安全性相关的部分，只是为了保证Token的安全
- 安装JWT的两个包：npm i jsonwebtoken express-jwt
  - jsonwebtoken用于生成jwt字符串，通过sign()方法将用户信息加密生成JWT字符串，并相应给客户端
  - express-jwt用于将jwt字符串解析还原成JSON对象