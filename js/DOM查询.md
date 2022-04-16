## DOM查询

### 1、节点属性

![image-20220105143127207](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220105143127207.png)

### 2、获取元素节点

1. childNodes获取所有子节点，注意：元素标签之间的换行、空格等也算作一个Text结点

![image-20220105142250972](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220105142250972.png)

![image-20220105143059036](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220105143059036.png)

### 3、CSS选择器选择元素

- document.querySelector()，IE8也支持。但该方法只返回第一个满足条件的元素
- document.querySelectorAll()，该方法将所有满足的元素封装到一个数组中

### 4、其他查询

- document.body：保存的是body的引用，包括js脚本
- document.html
- document.all：获取页面中全部元素

### 5、dom的增删改

- createElement("li")：创建元素结点对象
- createTextNode("文本结点")：创建一个文本结点对象
- appendChild()：向父节点中添加一个新的子节点

```js
var li = document.createElement("li");
var text = document.createTextNode("hello");
var b = document.getElementById("aa");
li.appendChild(text)
b.appendChild(li)
```

![image-20220107152124142](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220107152124142.png)

- 父节点.insertBefore(新节点，指定结点)：在指定的子节点前插入新的子节点
- 父节点.replaceChild(新节点，旧节点)：替换指定的子节点
- 父节点.removeChild(指定结点)：删除指定结点
- 一般常用，子节点.parentNode.removeChild

### 6、操作内联样式

- 元素.style.样式名 = 值：box.style.width = "300px"
- css中的样式名含有 - 的在js中需采用单驼峰命名：box.style.backgroundColor = "red"
- 通过style设置和读取的都是内联样式

### 7、获取样式

- 元素.currentStyle.样式名：获取当前显示的样式值，只有IE浏览器支持
- getComputedStyle：方法可以获取元素当前样式，需要传两个参数，第一个是要获取样式的元素，第二个是传入一个伪元素，一般设置成null，该方法会返回一个封装了当前元素样式的对象。不支持IE8及以下

```js
var obj = getgetComputedStyle(box,null);
console.log(obj.width)
```

### 8、元素的其他属性

- clientWidth、clientHeight：这两个属性可以获取元素的可见宽度和高度，其包括内容区和内边距，不包括边框，返回的是一个数字。且都是只读的，不可修改
- offsetWidth、offsetHeight：返回元素的高度和宽度，包括内容区、内边距、边框。返回的是数字，只读。
- offsetParent：获取当前元素距离最近的开启了position的父元素，若所有父元素都没开启定位，则返回body
- offsetLeft、offsetTop：返回当前元素距离最近开启了position的父元素的偏移量
- scrollWidth、scrollHeight：获取元素整个滚动区域的宽度和高度，即子元素的宽高比父元素大时，在父元素设置了overflow：auto时就会出现滚动条，这两个属性就会返回滚动条可以滚动的整个宽高。
- scrollLeft、scrollTop：获取滚动条距离左则或顶部的距离。
- 当满足scrollHeight - scrollTop == clientHeight时，说明滚动条已经滚动到最底部了。
