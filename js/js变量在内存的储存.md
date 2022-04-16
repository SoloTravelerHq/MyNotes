## js变量在内存中的存储

js中的变量都是保存在栈内存中的

对于基本数据类型（String、Number等）来说，值是直接保存在栈内存里

如下图：

![image-20211119153614967](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211119153614967.png)

而对于引用数据类型（Object）来说，在new了一个对象后，就会在堆内存中创建一个空间，其在栈内存中的值是堆内存中该空间的地址值。

如下图：

![image-20211119155522906](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211119155522906.png)

所以在进行对象的增删改和比较时，要注意他们是不是一个地址值，即是不是同一个对象。

如下图，虽然定义的两个对象设置的name值一模一样，但是他们的地址不一样，所以在比较obj == obj2 时返回的是false

![%8N@4V8VMV2(WRNP$3LY]F9](C:\Users\hq\Desktop\%8N@4V8VMV2(WRNP$3LY]F9.png)