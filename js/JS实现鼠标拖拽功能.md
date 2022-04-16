## JS实现鼠标拖拽功能

- 创建鼠标点下的**元素对象**的响应事件函数（onmousedown）。
- 计算鼠标位置和所点击元素偏移量的差值；如果不这样做，就会出现如下现象。即元素的左上角会直接定位在鼠标上。

![tuozhai](E:\图库\tuozhai.gif)

- 在onmousedown内创建鼠标移动的**全局**响应事件函数（onmousemove）。
- 在onmousedown内创建鼠标松开的**全局**响应事件函数（onmouseup）。

完整代码：注：必须给元素加上position属性

```html
<style lang="css">
    #box1{
        width: 100px;
        height: 100px;
        background-color: red;
        position: absolute;
    }
    #box2{
        width: 100px;
        height: 100px;
        background-color: yellow;
        position: absolute;
        left: 300px;
    }
</style>
<body>
    <div id="box1"></div>
    <div id="box2"></div>
</body>
<script>
    var box1 = document.getElementById("box1");
    drag(box1);
    drag(box2);
    function drag(obj){
        obj.onmousedown = function(event){
            // 兼容IE
            event = event || window.event;
            // 计算鼠标位置和元素偏移量的差值。
             var ol = event.clientX - obj.offsetLeft;
             var tl = event.clientY - obj.offsetTop;
            // 创建鼠标移动事件
            document.onmousemove = function(event){
                event = event || window.event;
                // 计算元素的移动位置
                var left = event.clientX - ol;
                var top = event.clientY - tl;
                obj.style.left = left + 'px';
                obj.style.top = top + 'px';
            }
            // 鼠标松开注销相关事件
            document.onmouseup = function(){
                this.onmousemove = null;
                this.onmouseup = null;
            }
            // 消除浏览器默认行为；IE8及以下版本不支持
            return false;
        }
    }
</script>
```

