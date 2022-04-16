## JS数组相关的方法

[TOC]

#### 1、push()

push()方法向数组的末尾添加新的元素，并返回新的数组长度，会改变原数组。时间复杂度为O(1)。

```js
var arr = [1, 2, 3];
arr.push(4);
console.log(arr);
```

```tex
[1, 2, 3, 4]
```

#### 2、pop()

pop()方法删除数组最末尾的元素，并返回删除的元素，会改变原数组。时间复杂度为O(1)。

```js
var arr = [1, 2, 3];
arr.pop();
console.log(arr);
```

```tex
[1, 2]
```

#### 3、unshift()

unshift()方法向数组头部插入新的元素，并返回新的数组长度，会改变原数组。时间复杂度为O(n)。

```
var arr = [1, 2, 3];
arr.unshift(0);
console.log(arr);
```

```tex
[0,1, 2, 3]
```

#### 4、shift()

shift()方法删除数组第一个元素，并返回删除后的元素，会改变原数组。时间复杂度为O(n)。

```js
var arr = [1, 2, 3];
arr.shift();
console.log(arr);
```

```tex
[2, 3]
```

#### 5、slice()

slice()方法会返回所提取数组指定位置的元素，不会改变原数组。

​	5.1 第一个参数是数组索引的起始位置（包含）。

​	5.2 第二个参数是数组索引的结束位置（不包含）。

​	5.3 第二个参数可以省略不写，则会从起始位置一直提取到最后。

```js
var arr = [1, 2, 3];
var arr2 = arr.slice(0,2);
console.log(arr);
console.log(arr2);
```

```tex
[1, 2, 3]
[1, 2]
```

​	5.4 如果参数是负值，则表示从数组末尾开始取，如：

​	arr.slice(-1,-2)表示提取数组倒数第一个到倒数第二个前的元素。

#### 6、splice()

splice()方法会返回所删除数组指定起始位置的指定数量的元素，会改变原数组。

​	6.1 第一个参数为数组索引的起始位置。

​	6.2 第二个参数为所删除元素的数量。

​	6.3 第三个参数之后，为在数组指定的起始位置前添加的新元素。

​	6.4 将第二元素设置成0，可以在指定位置前添加新元素。

#### 7、concat()

concat()可以连接两个或多个数组，然后返回一个新数组，不改变原数组。

```js
var arr = ["张三"];
var arr2 = ["李四"];
var arr3 = arr.concat(arr2, "王麻子");
console.log(arr);
console.log(arr3);
```

```tex
["张三"]
["张三","李四","王麻子"]
```

#### 8、join()

join()将数组转换成字符串并返回，不会改变原数组。

```js
var arr = ["张三", "李四", "王麻子"];
var result = arr.join();
console.log(arr);
console.log(result);
console.log(typeof result);
```

```tex
["张三", "李四", "王麻子"]
"张三,李四,王麻子"
string
```

join()在将数组转换成字符串时，默认用逗号隔开，如果想换其他方式隔开，可以在join()方法中设置。

```js
var arr = ["张三", "李四", "王麻子"];
var result = arr.join("#");
console.log(result);
var result = arr.join("");
console.log(result);
```

```tex
"张三#李四#王麻子"
"张三李四王麻子"
```

#### 9、reverse()

reverse()将数组翻转，会改变原数组

```js
var arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr);
```

```
[5, 4, 3, 2, 1]
```

#### 10、sort()

sort()方法将原数组进行排列，会改变原数组。不同浏览器的算法不同，时间复杂度也不同，如谷歌浏览器采用的是插入排序（数组长度<=10，O(n^2)）和快速排序（数组长度>10，平均情况O(nlogn)，最坏情况O(n^2)）。

sort()按照Unicode编码进行排序。

```js
var arr = ['b', 'd', 'f', 'q', 'a'];
arr.sort();
console.log(arr);
```

```tex
['a', 'b', 'd', 'f', 'q']
```

但用sort()来排序数字的话，就会出现问题，即sort()对数组中的数字同样是按照Unicode的编码方式来排序的。

为此，我们可以在sort()方法中添加回调函数，自定义排序功能。

在回调函数中设置两个参数，浏览器会分别使用数组中的元素作为实参去调用回调函数。如下

```js
var arr = [4, 5];
arr.sort(function (a, b) {
    console.log(a, b);
});
```

```tex
5 4
```

浏览器会根据回调函数的返回值来决定元素的顺序

如果返回值大于0，则元素会交换位置

如果返回值小于0，则元素不交换位置

如果返回值是0，则认为两个元素相等

```js
var arr = [5, 4, 3, 1, 2];
arr.sort(function (a, b) {
    return a - b;//升序
});
console.log(arr);

var arr = [5, 4, 3, 1, 2];
arr.sort(function (a, b) {
    return b - a;//倒序
});
console.log(arr);
```

```tex
[1, 2, 3, 4, 5]
[5, 4, 3, 2, 1]
```

#### 11、reduce()

reduce(callback, [initialValue])方法为数组的每一个元素调用回调函数。

回调函数用于遍历数组中的元素，该回调函数有四个参数

```
第一个参数是该回调函数上一次的返回值或初始值

第二个参数是当前遍历的数组元素

第三个参数是当前遍历的数组索引

第四个参数是数组本身
```

下面用reduce方法实现计算数组中的数字总和

```js
var arr = [5, 2, 2, 2, 1];
//sum为上一次回调函数返回的值或初始值，arr为当前遍历的数组元素
var result = arr.reduce(function (sum, arr) {
    return sum + arr;
}, 0)
console.log(result);
```

输出：

```
12
```

如果reduce方法没有设置初始值，那么reduce会从索引为1（设了初始值从索引为0）的位置开始执行callback方法。

```js
var arr = [5, 2, 2, 2, 1];
//没加索引值
var result = arr.reduce(function (sum, arr, index) {
    console.log(index)
    return sum + arr;
})
```

输出：

```
1
2
3
4
```

```js
var arr = [5, 2, 2, 2, 1];
//加了索引值
var result = arr.reduce(function (sum, arr, index) {
    console.log(index)
    return sum + arr;
},3)
```

```
0
1
2
3
4
```

所以，一般情况下我们都会设置初始值。

#### 12、filter()

filter()方法用于数组过滤，将满足条件的数组元素返回，不改变原数组。回调函数参数为：当前遍历元素、当前遍历索引、数组。

```js
var arr = [1, 1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4];
var arr2 = arr.filter((p) => {
    //将数组元素大于1的元素返回
    return p > 1;
})
console.log(arr2);
```

输出

```
[2, 2, 2, 3, 3, 3, 4, 4]
```

#### 13、fill()

fill方法用于将一个固定值替换数组中的元素，会改变原数组。

fill中有三个参数：要填充的值；开始填充的位置；结束填充的位置。

```js
var arr = ["张三",2,1,3,"李四"];
arr.fill("王麻子",1,4);
console.log(arr);
```

```
['张三', '王麻子', '王麻子', '王麻子', '李四']
```

#### 14、map()

map方法需要传入一个回调函数，该回调函数同样具有三个参数，即当前遍历的元素；当前遍历的索引；当前数组。可在该函数中对数组元素进行逻辑处理，最后map会返回一个新数组，不会改变元素组。

```js
var arr = [-1,2,-1,3,-2];
// 将数组所有元素取绝对值
var arr2 = arr.map((a) => {
return a<0?Math.abs(a):a;
})
console.log(arr2)
```

```
[1, 2, 1, 3, 2]
```

