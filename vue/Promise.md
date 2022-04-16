## Promise

- 传统的异步解决方案采用回调函数来实现
  - 必须在启动异步任务前指定回调函数
  - 回调函数嵌套调用会引发回调地狱问题，回调地狱不便于阅读，不便于异常处理

- Promise方案支持链式调用，可以解决回调地狱的问题
  - 启动异步任务=>返回Promise对象=>给Promise对象绑定回调函数（甚至可以在异步任务结束后指定多个回调函数）

- resolve和reject都是函数类型的数据

  - ```js
    const p = new Promise((resolve, reject) => {
    	let n = rand(1, 100)
        if(true) resolve(n)
        else reject(n)
    })
    ```

  - 调用then方法，成功执行左边的函数，失败执行右边的函数

  - ```js
    p.then((value) => {}, (reason) => {})
    ```

- Promise的状态

  - 实例对象中的一个属性PromiseState
  - pending => resolved / fulfilled
  - pending => rejected
  - 只能变换一次，且只能由pending转换成resolved或rejected

- Promise对象的值

  - 实例对象中的另一个属性PromiseResult，保存着异步任务成功/失败的结果，可由resolve和reject函数操作该结果

- Promise.all([p1,p2,p3])包含n个promise的数组
  - 返回一个新的promise，只有所有的promise都成功才成功，否则返回失败的对象
- Promise.race([p1,p2,p3])包含n个promise的数组
  - 返回一个新的promise，返回率先完成promise状态改变的promise对象的结果。
- 一个Promise指定多个回调函数，在状态改变时都会调用
- Promise可能先改变状态再执行回调，也可能先执行回调再改变状态，一般Promise中封装的是异步任务，则会先执行回调
- then
  - 抛出错误时，返回的是rejected
  - 返回非promise对象时，结果是fulfilled的值，不是promise对象
  - 返回promise对象时，结果是返回的promise对象结果
- 异常穿透：就是在回调函数的最后加上catch来对错误进行处理，而其他的then函数中不必定义处理错误的函数参数
- 只有返回一个pending的Promise对象才能终端Promise链：return new Promise(() => {})

- async函数：函数返回值为Promise对象，对象的结果由async的返回值决定，如果是返回非Promise对象，则结果是fulfilled。
- await表达式：await右侧的表达式一般为Promise对象，也可以是其他值，如果表达式是Promise对象，则await返回promise成功的值
  - await必须写在async函数中，如果await的promise失败了，需要通过try...catch来捕获处理