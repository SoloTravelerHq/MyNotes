## js基础this详解

解析器在调用函数，每次都会向函数内部传递进一个隐含参数，这个参数就是this，this指向的是一个对象。

这个对象我们称为上下文对象，根据函数的调用方式不同，this会指向不同的对象。主要有以下三种情况：

1、以函数形式调用时，this指向window

```js
function fun(){
    console.log(this);
}
//this指向window对象
fun();
```

输出：

![image-20211224200055845](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211224200055845.png)

2、以方法调用时，谁调用方法this就指向谁

```js
function fun(){
    console.log(this);
}

var obj = {
    name:"张三",
    sayName:fun
}
//obj调用方法，this就指向obj
obj.sayName();
```

输出

![image-20211224200403205](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211224200403205.png)

3、以构造函数形式调用时，this指向新创建的对象

```js
function Person(){
    //this.name指向per的name
    this.name = "张三";
}
var per = new Person();
console.log(per);
```

输出：

![image-20211225122717817](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211225122717817.png)