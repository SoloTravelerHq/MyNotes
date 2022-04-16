## 纯css实现旋转正方体

思路：

1、建一个父div作为正方体容器，在div里面建六个子div作为正方体六个面。

2、创建关键帧，让父div旋转起来。

效果：

![cube](C:\Users\hq\Desktop\cube.gif)

代码：

```html
<style>
  /* 设置正方体容器 */
  .fu {
    margin: 150px auto;
    height: 200px;
    width: 200px;
    /* 设置3d转换效果 */
    transform-style: preserve-3d;
    animation: cube 5s infinite linear;
  }

  /* 设置正方体六个面大小透明度 */
  .fu>div {
    position: absolute;
    width: 200px;
    height: 200px;
    opacity: 0.8;
  }

  /* 设置左面 */
  .z {
    transform: rotateY(90deg) translateZ(100px);
    background-color: yellow;
  }

  /* 设置右面 */
  .y {
    transform: rotateY(-90deg) translateZ(100px);
    background-color: blue;
  }

  /* 设置上面 */
  .s {
    transform: rotateX(-90deg) translateZ(100px);
    background-color: pink;
  }

  /* 设置下面 */
  .x {
    transform: rotateX(90deg) translateZ(100px);
    background-color: black;
  }

  /* 设置前面 */
  .q {
    transform: rotateY(0deg) translateZ(100px);
    background-color: red;
  }

  /* 设置后面 */
  .h {
    transform: rotateY(180deg) translateZ(100px);
    background-color: greenyellow;
  }

  /* 创建正方体旋转动画 */
  @keyframes cube {
    from {
      transform: rotateX(0) rotateZ(0);
    }

    to {
      transform: rotateX(360deg) rotateZ(360deg);
    }
  }
</style>

<body>
  <div class="fu">
    <div class="z"></div>
    <div class="y"></div>
    <div class="s"></div>
    <div class="x"></div>
    <div class="q"></div>
    <div class="h"></div>
  </div>
</body>
```

