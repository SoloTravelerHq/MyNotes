## js非布尔值的“与”，“或”运算

#### 1、非布尔值的“与”运算

```js
//非布尔值的与运算是短路的，即在判断第一个为false后，就不会再判断第二个
var a = 123 && 0;
console.log(a);//a = 123
var a = 0 && 0;
console.log(a);//a = 0
var a = 0 && 123;
console.log(a);//a = 0//第一个为0，直接返回，不再判断123
```

#### 2、非布尔值的“或”运算

```js
//非布尔值的或运算是短路的，即在判断第一个为true后，就不会再判断第二个
var a = 123 || 0;
console.log(a);//a = 123
var a = 0 || 123;
console.log(a);//a = 123
var a = 0 || 0;
console.log(a);//a = 0
```

## js关系运算符非数值的比较

```js
//1、对于非数值比较时，会将其先转换为数值，再进行比较
var a = 1 > "2";
console.log(a);//a = false
var a = "2" > 12;
console.log(a);//a = false
var a = "2" > 12;
console.log(a);//a = false
//2、如果符号两边都是字符串，则比较他们的Unicode编码
var a = "a" > "b";//a的Unicode编码是97，b是98
console.log(a);//a = true
```

## js中 == 和 === 的区别

== 可以自动将不同类型进行转换再比较数值的大小

```js
console.log(1 == 1);//返回true
console.log(1 == "1");//返回true
console.log(true == "1");//返回true
```

=== 则不会自动转换类型，直接比较

```js
console.log(1 === "1");//返回false
console.log(true === "1");//返回false
console.log("1" === "1");//返回true
```

