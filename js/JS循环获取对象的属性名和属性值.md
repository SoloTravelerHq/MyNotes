## JS循环获取对象的属性名和属性值

```js
var obj = {
    name: '张三',
    age: 20,
    gender: '男',
    address: '水帘洞'
}
//遍历对像
for(var n in obj){
    //输出属性名
    console.log(n);
    //输出属性的值
    console.log(obj[n]);
}

```

输出结果

```tex
"name"
"age"
"gender"
"address"
"张三"
"20"
"男"
"水帘洞"
```

