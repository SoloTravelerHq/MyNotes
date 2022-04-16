## 模拟Vue的数据监测

```js
// 要监测的数据
let data = {
    name: 'hq',
    age: 12
}
//实例化Observe
let ob = new Observe(data);
//定义一个对象
let vm = {};
//将劫持后的数据赋给vm_data
vm._data = data = ob;

function Observe(obj) {
    //获取对象属性
    let key = Object.keys(obj);
    //循环对象属性
    key.forEach((k) => {
        //将循环的属性值赋给Observe实例化对象
        Object.defineProperty(this, k, {
            //读取data中的数据
            get() {
                return obj[k];
            },
            //修改data中的数据
            set(val) {
                return obj[k] = val;
            }
        })
    })
}
```

![image-20220104173022975](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220104173022975.png)
