## JS函数的call()和apply()

这两个都是函数对象的方法，需要通过函数对象来调用，调用时都会执行函数体内的代码

这两个方法可以将一个对象作为函数的第一个参数，此时这个对象会成为该函数的this指向

```js
function fun(){
      console.log(this);
}
var obj = {
    name:'张三',
    age:20
}
fun.call(obj);
```

![image-20220104141703887](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220104141703887.png)

call()方法可以跟在obj后传递多个参数，apply()只能跟在obj后传一个数组

```js
function fun(a,b){
      console.log(this,a,b);
}
var obj = {
    name:'张三',
    age:20
}
fun.call(obj,2,3);
fun.apply(obj,[2,3])
```

![image-20220104142504316](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220104142504316.png)