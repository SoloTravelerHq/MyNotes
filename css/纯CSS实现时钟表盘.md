## 纯CSS实现时钟表盘

思路：

1、先创建一个表盘div。

2、再在表盘div里设置三个子div，分别作为秒针、分针、时针的旋转载体

3、最后在三个子div里分别再设置一个div，作为秒针、分针、时针

4、表盘可以用背景图片，也可以用css写，我这里直接百度了一张表盘的图片

代码：

```html
<style>
  /* 表盘 */
  .biao-pan {
    width: 300px;
    height: 300px;
    margin: 150px auto;
    border-radius: 50%;
    position: relative;
    background-image: url(./img/yazi.png);
    background-size: cover;
  }

  /* 设置旋转载体相对于表盘左右垂直居中 */
  .miao-zhen,
  .fen-zhen,
  .shi-zhen {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    margin: auto;
  }

  /* 设置指针左右居中 */
  .miao,
  .fen,
  .shi {
    position: absolute;
    right: 0;
    left: 0;
    margin: 0 auto;
  }

  /* 设置秒针 */
  .miao-zhen {
    width: 280px;
    height: 280px;
    animation: move 60s linear infinite;
  }

  .miao {
    height: 140px;
    width: 1px;
    background-color: black;

  }

  /* 设置分针 */
  .fen-zhen {
    width: 220px;
    height: 220px;
    animation: move 3600s linear infinite;
  }

  .fen {
    height: 110px;
    width: 2px;
    background-color: black;

  }

  /* 设时针 */
  .shi-zhen {
    width: 180px;
    height: 180px;
    animation: move 43200s linear infinite;
  }

  .shi {
    height: 90px;
    width: 4px;
    background-color: black;
  }

  /* 设置指针从0度转到360度 */
  @keyframes move {
    from {
      transform: rotateZ(0);
    }

    to {
      transform: rotateZ(360deg);
    }
  }
</style>

<body>
  <div class="biao-pan">
    <div class="miao-zhen">
      <div class="miao"></div>
    </div>
    <div class="fen-zhen">
      <div class="fen"></div>
    </div>
    <div class="shi-zhen">
      <div class="shi"></div>
    </div>
  </div>
</body>
```

效果：



![biaopan](C:\Users\hq\Desktop\biaopan.gif)