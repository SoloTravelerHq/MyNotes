# 盒子模型——margin

[TOC]

## 1、水平布局

margin在块状元素中设置时，上下左右都可设置，在设置margin-left,margin-top时，是移动当前盒子的位置。而设置margin-bottom时是移动下方盒子的位置。

但是设置元素的margin-right时，是没有变化的。这主要是因为盒子的水平布局的总宽度是必须等于其父元素的总宽度。假设父元素的宽是800px，则子元素的

**margin-left + border-left + padding-left + content(width) + margin-right+ border-right+ padding-right = 800px**

假设子元素只设置了宽100px，上述等式为：**0+0+0+100+0+0+0 = 800**

显然这个是不成立的，所以浏览器就会自动补充左侧等式的值，即将margin-right设置成700px，这样保证了等式成立。所以我们在设置margin-right时是没有效果的，因为浏览器已经帮你自动设置了。如果我们设置的子元素宽度超过父元素的宽度，比如子元素宽度设置了900px，父元素是800px，那么浏览器就会将margin-right设置成 -100px。

## 2、margin水平居中

如果子元素宽度设置的是auto，那么子元素宽度就会占满整个宽度。如果子元素设置了固定宽度，margin左右设置了auto，浏览器就会平均分配剩下的宽度，就是为什么margin：0 auto;能将子元素居中的原因。如果宽度值、margin-left、margin-right三个都设置了auto，那么浏览器只会把父元素的宽度全给子元素的宽度值。

![image-20210922223537370](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20210922223537370.png)

## 3、外边距重叠

两个相邻的块级元素，上方的设置了margin-bottom = 100px，下方的设置了margin-top = 200px，这时相邻块级元素的间距是等于100px的。就是说，相邻块级元素之间设置的margin是不会叠加的，只会取最大的那一方。当然如果相邻块级元素设置的外边距都是负值，则取绝对值大的那一个，如果是一正一负则取和。

<img src="C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20210922221147667.png" alt="image-20210922221147667" style="zoom:50%;" />

## 4、父子元素外边距重叠问题及解决方案

父子元素相邻时，子元素设置的外边距会传递给父元素，导致父子元素位置一起移动

![image-20210922221944558](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20210922221944558.png)

这个问题的解决的方案有很多，但开发中最常用的使用伪元素在父子元素之间加一个隔层。让他们不相邻。代码如下

css代码：

```css
.box1{
    width:200px;
    height:200px;
    background-color:#bfa;
}
.box1::before{
    content: '';
    display: table;
}
.box2{
    width:100px;
    height:100px;
    margin-top:100px;
    background-color:orange;
}
```

html代码：

```html
<div class="box1">
    <div class="box2"></div>
</div>
```

