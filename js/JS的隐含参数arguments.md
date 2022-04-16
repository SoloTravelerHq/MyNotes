## JS的隐含参数arguments

在调用函数时，浏览器除了会传入this隐含参数，还会传入arguments

arguments用于存储函数传进来的实参

```js
function fun(){
    console.log(arguments);
}
fun(1,'a')
```

![image-20220104143209902](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220104143209902.png)

arguments还有一个属性callee，这个属性对应着一个函数对象，就是当前正在指向的函数对象

```js
function fun(){
    console.log(arguments.callee);
}
fun()
```

![image-20220104143528418](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220104143528418.png)