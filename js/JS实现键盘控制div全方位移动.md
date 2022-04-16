## JS实现键盘控制div全方位移动

- 创建onkeydown的全局响应事件，给div设置加速度，并控制div开始移动。
- 创建定时器控制div持续移动，这样可以防止div移动的卡顿现象。
- 创建onkeyup的全局响应事件，控制div停止移动。
- div移动的卡顿现象是由于在按下键盘时，系统需要区分用户是否是持续输入，这个过程就会出现短暂的卡顿，用定时器可以巧妙的避免。

完整代码：

```html
<style lang="css">
    #box1{
        width: 100px;
        height: 100px;
        background-color: red;
        position: absolute;
    }
</style>
<body>
    <div id="box1"></div>
</body>
<script>
    var box1 = document.getElementById("box1");    
    // 初始化移动速度
    var speed = 5;
    // 控制方向(上、左、下、右)
    var dir = [false,false,false,false];
    // 设置定时器控制元素全方位移动
    setInterval(function(){
            // 向左
            if(dir[3]) box1.style.left = box1.offsetLeft - speed + 'px';
            // 向右
            if(dir[1]) box1.style.left = box1.offsetLeft + speed + 'px';
            // 向上
            if(dir[0]) box1.style.top = box1.offsetTop - speed + 'px';
            // 向下
            if(dir[2]) box1.style.top = box1.offsetTop + speed + 'px';
    },10)
    // 鼠标按下设置速度和方向
    document.onkeydown = function(event){
        var e = event || window.event;
        switch(e.keyCode){
            case 37:dir[3]=true;
                    break;
            case 38:dir[0]=true;
                    break;
            case 39:dir[1]=true;
                    break;
            case 40:dir[2]=true;
                    break;
        }
        // 按住ctrl键加速移动，松开恢复
        if(event.ctrlKey){
            speed = 10;
        }else{
            speed = 5;
        }
        
    }
    // 松开鼠标停止移动
    document.onkeyup = function(event){
        var e = event || window.event;
        switch(e.keyCode){
            case 37:dir[3]=false;
                    break;
            case 38:dir[0]=false;
                    break;
            case 39:dir[1]=false;
                    break;
            case 40:dir[2]=false;
                    break;
        }
    }
</script>
```

