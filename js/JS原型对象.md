## JS原型对象

我们所创建的每一个函数，解析器都会向函数中添加一个属性prototype，这个属性对应着一个对象，这个对象就是所谓的原型对象。而prototype属性会指向该函数原型对象。![image-20211225153136844](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211225153136844.png)

如果函数作为普通函数调用时，prototype没有什么用处；当函数作为构造函数调用时，这个构造函数所创建的对象都会有一个隐含的属性\_\_proto\_\_，该属性会指向该构造函数的原型函数，如图所示

![image-20211225153958769](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211225153958769.png)

很容易看出，原型对象相当于一个公共区域，所有同一个类的实例都可以访问到这个对象。

现在我们要创建一个构造函数，该函数有如下属性和一个方法

```js
function Person(name,age) {
        this.name = name;
        this.age = age;
        this.say = function(){
            console.log("我不是哑巴！");
        }
    }
var per1 = new Person("张三",20);
var per2 = new Person("李四",21);
```

如上，我们每创建一个实例就会在堆内存上创建一个新的say方法，创建10000000个就会新建10000000个say方法，而且这10000000方法都是一样的，而且非常占用空间。但是把这个say方法提取到全局作用域中就会污染全局作用域的命名空间，而且也很不安全，在实际开发中很容易被同名函数覆盖。

这时就可以将这个say方法定义在Person类的原型函数中，就可以解决上述问题，创建多个对象实例时既不占用额外空间，也不会污染全局作用域的命名空间。

```js
function Person(name, age) {
        this.name = name;
        this.age = age;
}
Person.prototype.say = function () {
    console.log("我不是哑巴！");
}
var per1 = new Person("张三", 20);
var per2 = new Person("李四", 21);
per1.say();
per2.say();
```

![image-20211225155454118](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211225155454118.png)

最后要说的是，原型函数本身也是函数，即原型函数也有它自己的原型函数。

当我们使用一个对象的属性或方法时，会先在自身中寻找，

如果自身没有就会到该对象的原型函数中寻找，

如果还没有就会到该对象的原型函数的原型函数中寻找。

直至找到Object对象的原型，而Object对象原型没有原型，

如果还没有找到想要的属性或方法，就会返回undefined。

```js
function Person() {

}
var per1 = new Person("张三", 20);
//Object对象的原型函数没有hello属性，返回undefined
console.log(per1.hello);
//Person对象的原型函数
console.log(per1.__proto__);
//Person对象的原型的原型，是Object对象的原型
//即等价于console.log(Object.prototype);
console.log(per1.__proto__.__proto__);
//Object对象的原型（__proto__）的值是个null
console.log(per1.__proto__.__proto__.__proto__);
```

![image-20211225173738307](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211225173738307.png)