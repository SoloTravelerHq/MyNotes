-  在js调用函数时传递的变量参数，可以理解为全部是值传递，即基本数据类型传递的是值，引用数据类型传递的是对象的地址值；第二种理解为基本数据类型是值传递，引用数据类型是引用传递。
- 内存生命周期为：分配小内存空间得到它的使用权；存储数据，可以反复进行操作；释放小内存空间。函数中的局部变量，在函数执行时创建，在函数执行完释放。js的垃圾回收机制是每个一段时间执行一次。
- 必须使用['属性名']的方式存在两种情况：1）属性名包含特殊字符；2）属性名存在变量中

### 原型对象

- 构造函数和它的原型对象是相互引用的关系
- ![image-20220129125756140](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220129125756140.png)
- ![image-20220129125152310](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220129125152310.png)

- ![image-20220130131438852](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220130131438852.png)