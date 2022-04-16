## forEach和回调函数

forEach方法跟for循环差不多，写法要比for循环简单一点，但是forEach不支持IE8以下的版本。所以如果要兼容IE8以下的浏览器版本的话还是要用for循环，如果就是移动端开发就无需考虑这点。

forEach方法需要一个函数作为参数，而像这种函数，由我们创建但是不由我们调用的，我们称为回调函数。

```js
var arr = [1, 2, 3, 4];
arr.forEach(function () {
    console.log("hello");
})
```

输出：

![image-20211226144906043](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211226144906043.png)

浏览器会在回调函数中传入三个参数

第一个参数，是当前正在遍历的元素

第二个参数，是当前遍历的索引

第三个参数，是当前遍历的对象

```js
var arr = ['张三', '李四', '王麻子'];
arr.forEach(function (val, index, obj) {
    console.log(val, index, obj);
})
```

输出：

![image-20211226145343547](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211226145343547.png)