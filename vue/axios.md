## axios

### config配置项

- url：请求的对象
- method：请求的方法
- baseURL：设置url的基础值，比如设置http，url就不用了再写http了
- transformRequest：将发送的数据进行处后再发送给服务器
- transformResponse：将响应的结果做一些改变
- headers：请求头信息
- params：url参数
- paramsSerializer：参数序列化，即将params参数转换成字符串，如：/post?a=100&b=200转化成/post/a.100/b.200
- data：请求体，如果是对象形式，axios会将其转换成JSON格式字符串，如果是字符串格式会直接传递
- timeout：超时时间，超过指定时间，请求会被取消
- withCredentials：跨域请求时，对cookie的携带做设置，false时不携带
- adapter：对请求的识别器做一个设置，一种是发送ajax，一种是在js里发送http请求
- auth：请求基础验证，设置用户名和密码
-  responseType：对响应体结果格式做一个设置，默认是json
- xsrfCookieName：跨站请求标识，对cookie的名字进行设置
- xsrfHeaderName：跨站请求标识，对头信息做一个设置，
  - xsrfCookieName和xsrfHeaderName保证我们的请求时来自于我们自己的客户端；服务器返回结果时，会返回一个唯一的标识，客户端再次发送请求时把唯一表示传给服务器，服务器检验通过后再响应

### 创建实例对象

- const instance = axios.create({})：这里的instance的功能与axios的功能几乎是一样的

- 在对象实例中可以设置一些默认参数，之后再发送请求时就会默认带上这些参数

  - ```js
    const instance = axios.create({
    	baseURL: 'http',
    	timeout: 2000
    })
    ```

- 在有多个服务器提供数据接口时，可以定义多个对象实例

### 拦截器

- 请求拦截器

  - 作用：在发送请求前，对请求参数和内容做一些处理和检测，如果没有问题，则发送请求，如果有问题，则终止请求

  - ```js
    axios.interceptors.request.use(function(config) {
        console.log('请求拦截器 成功')
        return config
    }, function(error) {
        console.log('请求拦截器 失败')
        return Promise.reject(error)
    })
    ```

    

- 响应拦截器

  - 作用：在处理服务器返回的结果之前做一些预处理

  - ```js
    axios.interceptors.response.use(function(response) {
        console.log('响应拦截器 成功')
        return response
    }, function(error) {
        console.log('响应拦截器 失败')
        return Promise.reject(error)
    })
    ```


### 取消请求

- cancel是一个函数

```js
let cancel = null
axios({
    method: 'GET',
    url: 'xxxx',
    cancelToken: new axios.CancelToken(function(c){
        cancel = c//c是一个函数
    })
})
cancel()
```

### 源码分析

- 实例化对象

  - var axios = new Axios(defaults)，向构造函数中传入默认配置项（method、baseURL等）

- 在构造函数Axios中定义了interceptors对象

  - ```js
    this.interceptors = {
        request: new InterceptorManager(),
        response: new InterceptorManager()
    }
    ```

- 在Axios.js文件中，Axios在原型上加了许多方法
  - 如：Axios.prototype.request = function request(config) {...}

- 在axios.js文件createInstance方法中创建Axios实例对象context
  - 将request方法的this指向context，并返回一个新函数instance
  - 用extend方法将Axios原型和实例对象的方法都添加到instance函数身上
  - 再将context实例对象的方法和属性扩展到instance函数身上

- axios发送请求的过程

  - axios发送请求是通过request方法的，其他的post、get等请求也是调用的request方法
  - request方法中调用dispatch方法，dispatch方法调用xhrAdapter方法，xhrAdapter方法中运用ajax来发送请求，将请求结果以promise形式返回

- 拦截器

  - 在InterceptorManager函数中创建handlers数组
  - 在InterceptorManager原型上添加use方法，将拦截器添加到handlers数组中
  - 在request方法中将handlers中的元素添加到chains数组中，请求拦截器添加在dispatch方法前，响应拦截器添加到undefined后
  - 使用while循环中，在promise的回调中执行拦截器

- 取消请求

  - 创建CancelToken构造函数
  - 在外部定义一个变量，用来保存构造函数中的resolvePromise函数。resolvePromise用于存储promise成功的回调
  - 当外部执行取消函数时，就会执行构造函数中的resolvePromise函数，从而传回一个成功的Promise，就会执行xhrAdapter中的回调函数，而这个回调函数中就是取消请求的xhr.abort
  - 这里涉及到Promise的源码，即在创建axios时，创建CancelToken的实例，此时执行resolvePromise的函数已经存在了cancel中
  - 在Promise源码中，执行异步任务会先执行回调，此时Promise原型上的then方法会将两个回到函数先储存在数组中，等异步任务执行resolve或reject时再执行事先储存的回调函数。
