# 前端开发笔记

[TOC]

## 1、判断对象和数组是否为空

1.判断空对象

```javascript
let obj = {}
Object.keys(obj).length === 0 //表示是空对象
```

2.判断空数组

```javascript
let array1 = []
array1.length === 0 //表示是空数组
```

## 2、js 分割字符串

split() 方法用于把一个字符串分割成字符串数组。

```javascript
var str1 = "2,25,234,234,a"
var result = string.split(",")
//result的内容如下
result = ['12','25','234','234','a']
-------------------------------------------------
var str2 = "a"
var result = string.split(",")
//result的内容如下
result = ['a']
-------------------------------------------------
var str3 = ""
var result = string.split(",")
//result的内容如下
result = ""
```

[更多](https://www.w3school.com.cn/jsref/jsref_split.asp)

## 3、js 指定小数位数

toFixed() 方法可把 Number 四舍五入为指定小数位数的数字。

```javascript
var coordinate = "12.2212345,25.2343235" //坐标
var data = coordinate.split(",") //将坐标存入数组中
//parseFloat()先将字符串转化float类型，再用toFixed(6)保留小数点后六位。
coordinate = parseFloat(data[0]).toFixed(6) + "," + parseFloat(data[1]).toFixed(6)
```

## 4、vue中使用input监听事件

```javascript
//@input设置监听事件,可以监听input中值的变化，方法名自取
<input type="text" @input="inputEvent()" >
//js代码，e是监听事件自带参数不需要在方法中参入
inputEvent(e) {
    //获取输入框的值有两种方法
    const value = e.detail
    const value = e.target.value
    //e中还有许多其他参数如图。可自行百度了解
}
//若需传入其他参数，且还要获取e值,这时需手动传入$event
<input type="text" @input="inputEvent($event,parameter)" >
//js
inputEvent(e,parameter) {
    const value = e.detail
    const value = e.target.value
}
```

e值的内容

![image-20210718104720864](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20210718104720864.png)

## 5、楼层跳转时，设置滚动条跳转距离

```javascript
window.scrollTo({
    top: 600, //设置滚动的距离
    behavior:'smooth'//设置滚动速度
})
```

## 6、vue添加监听和消除滚动条事件

```javascript
//注册滚动监听事件
mounted() {
	window.addEventListener("scroll", this.handleScroll)
},
//销毁滚动监听
beforeDestroy() {
	window.removeEventListener("scroll",this.handleScroll)
},
methods: {
    //滚动条事件
	handleScroll() {}    
}
```

## 7、正则身份证验证

```javascript
//传入身份证号，先判断长度，再进行正则验证。
export function isCardNo(num){
	var len = num.length
	if(len<15 || len>18){
		return false
	}
	var re15 = /^[1-9]\d{7}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{3}$/ //第一代身份证
	var re18 = /^[1-9]\d{5}(18|19|([23]\d))\d{2}((0[1-9])|(10|11|12))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/ //第二代身份证
	var res = (re15.test(num) || re18.test(num))
	if(res==false){
		return false
	}
	return res
}
```

## 8、vue中数组更新后，不能及时响应

对于已经创建的实例，Vue 不允许动态添加根级别的响应式 property。但是，可以使用 `Vue.set(object, propertyName, value)` 方法向嵌套对象添加响应式 property

[使用方法见官方api](https://cn.vuejs.org/v2/guide/reactivity.html#%E5%A6%82%E4%BD%95%E8%BF%BD%E8%B8%AA%E5%8F%98%E5%8C%96)

```javascript
//index是数组索引，ture是赋给item.displayPhoto[index]的值
<image v-if="item.displayPhoto[index]" :src="item.idPhoto[index]" ></image>
//js
this.$set(item.displayPhoto[index], index, true)
```

## 9、uniapp解决input设置高度后文字不垂直剧中

```css
.input{
		border: 1rpx solid #EEEEEE;
		height: 96rpx;
		line-height: 96rpx;
		//主要是下面这三个
		display: flex;
		justify-content: center;
		align-items: center;
	}
```

## 10、uniapp文本输入限制为正整数

```javascript
export function intValidation(value){
	let final = ''
	const zero = /^(0{2,})|[^0-9]/g
	if (!value) {
	  final = ''
	} else {
		//如果不是正整数就返回空
	  final = value.toString().replace(zero, (value) => {
		return ''
	  })
	  //如果是082这种，去掉前面的0
	  if (final.split('')[0] * 1 === 0) {
		final = final.slice(1) - 0
	  }
	}
	return final
}
```

## 11、uniapp用globalData定义全局变量

定义在APP.vue里

```javascript
<script>
	export default {
		globalData: {
			zjr: '',//指界人
			xdm: ''//小地名
		},
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>
```

给全局变量赋值

```javascript
getApp().globalData.zjr = this.zjr
getApp().globalData.xdm = this.xdm
```

获取全局变量的值

```javascript
this.zjr = getApp().globalData.zjr
this.xdm = getApp().globalData.xdm
```

