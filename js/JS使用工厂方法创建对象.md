## JS使用工厂方法创建对象

工厂模式的思想简单的说就是建立一个工厂类，然后往工厂里输送原料，工厂拿到这些原料就会产出产品。

现在我们建一个造人的工厂，即一个创造人的函数。这个工厂想要产出产品对象，需要name、age、gender三种原料。于是我们只要给工厂送去原料就可以得到一个产品（人）。

```js
//建立一个造人工厂
function creatPerson(name,age,gender){
    var person = new Object();
    person.name = name;
    person.age = age;
    person.gender = gender;
    person.sayName = function(){
        alert(this.name);
    }
    return person;
}
//给工厂送去原料并获得产品
var person1 = creatPerson("张三",18,"男");
var person2 = creatPerson("李四",19,"女");

```

