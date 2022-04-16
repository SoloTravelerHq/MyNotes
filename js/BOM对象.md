## BOM对象

![image-20220111213257140](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220111213257140.png)

### 1、Navigator

![image-20220111221522889](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220111221522889.png)

![image-20220111221725492](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220111221725492.png)

![image-20220111222456576](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220111222456576.png)

### 2、History

- history.back()：可以用来回退到上一个页面
- history.forward()：可以用来跳转到下一个页面
- history.go()：可以用来跳转到指定的页面。正数向前跳转，负数向后跳转

### 3、Location

- 直接打印location可以获取到当前页面的地址栏信息（完整路径）
- location.assign("xxxx")：用来跳转页面，跟直接修改location效果一样，并生成相应的历史记录。
- location.reload(true)：重新加载页面，和页面刷新效果一样。如果在这个方法中传入一个true，则会强制清空缓存刷新页面。
- location.replace("xxx")：使一个新页面替换当前页面，类似页面跳转，但不会生成历史记录