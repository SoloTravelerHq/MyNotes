## css实现过渡效果

css实现过渡效果主要是通过transition属性来设置。代码如下

```css
/* 设置下载app的二维码下拉效果 */
.topbar .app .qr-code {
  width: 124px;
    /*将过渡元素的高度设置为0，元素内容设置隐藏*/
  height: 0px;
  overflow: hidden;
    /*transition的第一个值监听高度的变化（其他css属性同样可以监听）第二值设置过渡时间*/
  transition: height 1s;
    /*------------------------------*/
  line-height: 1;
  position: absolute;
  left: -38px;
  background-color: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  
}
/*鼠标移入，改变高度，transition会监听高度变化，实现过渡效果*/
.topbar .app:hover .qr-code {
  height: 148px;
}
```

<video src="C:\Users\hq\Desktop\QQ录屏20210930110816.mp4"></video>

