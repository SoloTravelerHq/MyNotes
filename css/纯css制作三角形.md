## 纯css制作三角形

纯css制作三角形的原理是通过设置元素border的属性来达到的。我们先将一个div的border上下左右设置不同的颜色，可以看到border其实是一个梯形。

```css
div {
    width: 100px;
    height: 100px;
    border: 10px solid red;
    border-color: red orange blue yellow;
}
```

![image-20210926204427964](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20210926204427964.png)

现在我们将div的宽度和高度设置成0，可以看到现在是四个小三角形

```css
div {
    width: 0px;
    height: 0px;
    border: 10px solid red;
    border-color: red orange blue yellow;
}
```

![image-20210926204941550](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20210926204941550.png)

然后根据我们的需求，来选取不同方向的小三角形，以下方的三角形为例，我们将border-top去掉，将border-left和border-right的颜色设置成透明，就得到了我们想要的三角形了。

```css
div {
    width: 0px;
    height: 0px;
    border: 10px solid red;
    border-top: none;
    border-color: transparent transparent blue transparent;
}
```

![image-20210926205440851](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20210926205440851.png)

