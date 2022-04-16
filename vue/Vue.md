# Vue

## 一、起步

### 1、安装：

- \<script\>标签引入
- npm命令

### 2、Vue实例配置对象说明

- el：与html容器绑定
- data：存储供el所绑定的容器使用

### 3、模板语法

- 插值语法：{{}}
- 指令语法：<a>v-bind:href="url"</a>

### 4、数据绑定

- 单向绑定：v-bind
- 双向绑定：v-model只能应用在表单类元素上

### 5、MVVM模型

- M：模型—对应data里的数据
- V：视图—模板（html）
- VM：视图模型—Vue实例

### 6、数据代理

- Vue实例对象vm可以操作data中的属性就是数据代理
- 原理是通过Object.defineProperty()把data对象中所有属性添加到vm，为每一个添加到vm上的属性都指定一个getter/setter，并在getter/setter内部去操作data属性

### 7、事件代理

- methods基本使用
- 事件修饰符：prevent:阻止默认事件、stop阻止事件冒泡、once事件只触发一次、capture事件捕获、self只有event.target是当前元素时才能触发事情（类似阻止事件冒泡）、passive事件默认行为立即执行，无需等待事件回调执行完毕。
- 键盘事件：keydown（按下触发），keyup（松开触发）![image-20211227222230932](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211227222230932.png)

### 8、计算属性

- 计算属性具有缓存机制，页面多次调用只执行一次
- 需要依赖data属性计算的属性写在computed中
- get()获取所依赖属性的变化，将值返回给计算属性，this指向Vue实例
- set()获取计算属性修改的值，通过this指向将变化的值赋给所依赖的属性
- 不能设置需要异步执行的计算属性

### 9、侦听属性

- Vue中的watch默认不检测内部的改变（deep默认为false）
- immediate立即执行一次
- 一般面临需要异步计算的属性用watch

### 10、箭头函数和普通函数

- Vue管理的函数写成箭头函数没有自己的this，会直接指向window，所以Vue管理的函数一般写成普通函数。
- 不是Vue管理的函数（settime、Promise、ajax等），有指向window的this，所以一般写成箭头函数去调本身的this，向外找this指向，即Vue实例。

### 11、样式绑定

- :class="表达式"，可以是变量、数组、对象
- :style="对象"，{属性名：值+'单位'}

### 12、条件渲染

- v-show="表达式"，表达式返回布尔值，隐藏效果与displa：none一样
- v-if、v-else-if、v-else组合使用，判断是否加载，即隐藏后DOM不渲染该节点
- v-if可以和template组合使用，template不影响页面结构

### 13、列表渲染

- v-for指令遍历
- 遍历数组（item，index）in arr
- 遍历对象（value，属性名）in obj
- 遍历字符串（字符，index）in string
- 遍历数字（从0开始，index）in 5
- key是虚拟DOM的标识，当数据发生改变时，Vue会在虚拟DOM中进行相同key的数据对比，再渲染至页面。相同内容直接复用。所以用唯一标识id作为key很重要，既可以提高效率也可以防止错误出现

### 14、Vue.set()

- Vue.set方法可以给data中的对象添加响应式属性，但不能给vue实例添加属性，不能直接给data添加属性
- this.$set('对象名'，‘需要添加的属性’，值)

### 15、数据监听

- Vue通过get()、set()方法来监听数据变化
- 直接通过索引将数组进行修改，Vue不能监听到数组的变化，因为数组中的索引没有get()、set()方法。
- 只有通过数组的push、pop等能改变数组的方法来修改数组才可以修改数组，Vue才能监听到数据变化，也可以用Vue.set()方法修改（不常用）
- Vue中的push经过包裹，即在数组调用push等方法时，Vue会再重新渲染虚拟DOM，然后在加载到真实DOM中

### 16、表单

- 对于单选框来说，需要设置value
- 对于多选框来说，需要将绑定的属性设置成数组，并设置多选框的vaule
- v-model修饰符有：trim去掉首尾空格、lazy失去焦点再响应输入的内容、number限制内容为数字

### 17、过滤器

- 对要显示的数据进行格式化再显示，适用于一些简单逻辑处理
- 全局注册Vue.filter(name, callback)
- 局部注册new Vue({filters:{}})
- 使用在插值语法{{修改的值 | 过滤器名}}或v-bind:="修改的值 | 过滤器名"
- 可以传多个参数，没有改变原数据

## 二、生命周期函数

### 1、beforeCreate()

- 在vue实例创建时调用，此时还没有获取data、methods等元素，即还未开始数据代理

### 2、create()

- 在Vue执行了数据代理、数据监测后调用

### 3、beforeMount()

- 在虚拟DOM和真实DOM之间，即在虚拟DOM渲染完成后，真实DOM渲染前调用
- 在此函数下，对真实DOM的操作，最终都不奏效

### 4、mounted()

- mounted在页面第一次加载完毕后执行，即在Vue把初始化页面挂载完毕后调用mounted。
- 一般在此函数内进行初始化操作，但尽量避免操作DOM

### 5、beforeUpdate()

- 数据发生更新时调用次函数，但此时数据是新的，页面上的数据是旧的，即新数据还未与页面同步

### 6、update()

- 数据发生更新时调用，此时页面已经更新了新的数据

### 7、beforeDestroy()和destroy()

- vm销毁函数，在此销毁前的data、methods、指令等都还可以用，一般在销毁前做一些关闭定时器、取消订阅消息等操作。不适合做一些数据更新操作

## 三、组件

### 1、单文件组件和非单文件组件

- 非单文件组件中包含多个组件，html文件类型
- 单文件组件只有一个组件，vue文件类型

### 2、创建组件

- Vue.extend({})用于创建组件，可不写，不写的话源码会自动添加
- data必须写成普通函数的形式
- template设置html模板

### 3、注册组件

- new Vue({})中配置components，用于局部注册组件
- Vue.component(‘组件名’，组件定义的名字)
- 编写组件标签

### 4、组件命名

- 一个单词全小写，或首字符大写
- 多个单词全小写，每个单词用-隔开，或每个首字母大写（需要在cli环境下才能生效）

### 5、组件嵌套

- 组件中可以再注册组件

### 6、VueComponent

- 组件的实例对象是VueComponent，不是Vue，但其结构和Vue的实例对象一样，除了el配置项。
- VueComponent的原型对象的隐私原型对象是Vue的原型对象，即VueComponent实例对象可以访问Vue原型对象的属性和方法

### 7、单文件组件

- template组件结构，即html结构
- script编写脚本，需要暴露出去，
  - 1）export default默认暴露，适合单个组件；导入用impor XXX from XXX
  - 2）export分别暴露，放在组件前；导入用impor {xxx} from XXX
  - 3）export{}统一暴露，适合多个组件一起暴露；导入用impor {xxx} from XXX
- style样式

## 四、Vue CLI

### 1、全局安装和运行

- npm install -g @vue/cli
- 进入项目文件夹，运行：vue create 项目名称
- 进入项目，运行：npm run serve

### 2、脚手架结构

- .gitignore：git忽略，即哪些文件或文件夹不想接受git的管理，则在此配置
- babel.config：babel的配置文件，babel拥有ES6转ES5
- package-lock：包管理控制，安装包时，以这个配置文件指定的版本
- package：包的说明
- README：项目说明
- main.js：程序入口
- App.vue：所有组件的父组件
- components：存放组件
- assets：存放静态资源（图片、视频等）

### 3、render函数

- render传入一个createElement函数，创建App的标签。
- 脚手架默认导入的vue是阉割版的，没有模板解析器，所以无法在Vue里配置template

### 4、vue.config.js

- vue的配置文件，可以配置入口文件等

### 5、ref

- ref可以给html打上标签，通过this.$refs可以获取这些元素

### 6、props父组件向子组件传数据

- props用于接收父组件传过来的参数
- 父组件传过来的参数不能修改，只能通过在子组件定义新的属性接收父组件的参数值，进行需求上的修改

### 7、mixin混入

- 多个组件共享一个配置，如共用一个方法
- 建一个js文件，在里面写公共方法export const mixin = {}
- 在组件上引用import {xxx} from ''
- 在Vue.extend中配置mixins:[]
- 在main.js里引用Vue.mixin()为全局引用

### 8、插件

- 插件用于增强Vue，即在插件里定义全局使用的方法、混入等
- 定义插件export default {insatll(Vue){...}}
- 在main.js中引入，并Vue.use(插件.js)

### 9、scoped

- 让样式在局部生效，防止不同组件的class名称冲突

### 10、项目流程

- 抽取组件
- 创建抽取好的组件
- 在App或父组件上引入组件
- 写代码

### 11、子组件向父组件传数据

- 父组件定义一个函数传到子组件
- 子组件接收到函数，向函数中传入数据返回给父组件
- 父组件传过来的数据，子组件不能修改，需要在父组件上写一个函数传入子组件，子组件将想要修改的数据传给父组件再进行修改

### 12、本地数据存取

- localStorage关闭浏览器后数据还存在本地，sessionStorage关闭浏览器后本地数据清空，容量大约5M左右

- localStorage.setItem('key',value)保存到本地，value会自动转成字符串
- localStorage.getItem('key')返回一个字符串
- localStorage.removeItem('key')清除指定数据
- localStorage.clear()清除全部数据

### 13、自定义事件

- 自定义事件绑定在子组件的实例对象上
- 用（@自定义事件='要触发的函数'）绑定的自定义事件，需在子组件中以this.$emit('自定义事件')，可用于子组件向父组件传入数据
- 在mounted中绑定自定义事件，在子组件标签中设置ref，在mounted中获取this.$refs.ref设置的名称.$on('自定义事件'，this.要触发的函数)，需在子组件中以this.$emit('自定义事件')，可用于子组件向父组件传入数据
- 自定义事件解绑，需在子组件中调用this.$off('自定义事件')，或this.$off(['自定义事件1','自定义事件2'])
- 若需要在组件标签上直接使用原生事件，则需加上native，如@click.native=""

### 14、事件总线

![image-20211231172132202](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20211231172132202.png)

- 全局总线定义在Vue的原型对象上，这样所有的vc、vm都可以访问到了
- 在main.js上的Vue中的beforeCreate函数上定义Vue.prototype.$bus = this
- 在需要创建自定义事件的组件中定义：this.$bus.$on('事件名',(data)=>{})
- 在需要触发事件传入数据的组件中定义：this.$bus.$emit('事件名',data)
- 用全局总线创建的自定义事件，需要在组件销毁时主动解绑
- 全局总线定义的自定义事件，有可能有命名冲突，需要做一些处理

### 15、消息订阅与发布

- 用于组件之间的通信
- 引入第三方库：如npm i pubsub-js
- 在需要接受数据的组件中订阅消息pubsub.subscribe('消息名'，回调函数)
- 在需要提供数据的组件中发布消息pubsub.publish('消息名'，数据)
- 订阅消息后，在组件销毁时，需要手动在钩子函数中销毁订阅的消息pubsub.unscribe(pid)

### 16、$nextTick(回调函数)

- 用于在下一次DOM更新后执行

### 17、动画过渡切换

- 将需要动画过渡的标签用<transtion>包裹
- 在css中创建关键帧
- 选择器.name-enter-active进入
- 选择器.name-leave-active离开
- 在transtion标签上加上name标签命名默认是v-enter-active，appear标签页面加载执行进入动画

![image-20220101122745612](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220101122745612.png)

### 18、跨域问题

- 跨域问题即请求的地址和本机地址的http、服务器地址、端口不一样，就会发生跨域问题
- 解决跨域的方法有三种1、用Nginx；2、jsonp；3、vue脚手架自带的

### 19、插槽

- 插槽主要用于，在父组件中向子组件传入特定的html标签
- 默认插槽：在组件标签里加入html标签，在组件中添加<slot\>，组件标签内的html标签就会默认插入到<slot\>中
  - 具名插槽：给\<slot>加上name，则组件标签内的html标签需加上v-slot:进行绑定，v-slot:简写为#

- 作用域插槽：数据在子组件身上，父组件上的组件标签在传html标签时需要用子组件的数据，则在子组件插槽上设置\<slot :name="name"></slot\>，在父组件上的组件标签中套上\<template scope="{name}">html标签</template\>

## 五、VueX

- 多组件共享同一状态时，可将这状态放在vuex中
- ![image-20220101204152969](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220101204152969.png)

### 1、创建Vuex

- 在src中新建文件夹store
- 在store中新家js文件index.js
- 在js文件中引入Vue、Vuex
- 使用Vue.use(Vuex)
- 创建store：export default  new Vuex.Store({})
- 在main.js中引入store，在Vue实例中配置

### 2、使用Vuex

- 在vc方法中使用this.$store.dispatch('name'，data)
- 在store中的action中设置name(context,data){context.commit('NAME',data)},向mutation中传入指令
- 在mutation中设置NAME(state,data){}
- 使用this.$store.commit('NAME',data)直接跟mutation交互
- getter用于给state中的数据加工，类似computed

### 3、mapState和mapGetters

- 借助这两个函数可帮助自动生成$store.state/getters中的属性值
- 导入import {mapState,mapGetters} from ‘vuex‘
- 在computed中写...mapState([''])，就可读取state中的属性值

### 4、mapMutations和mapActions

- 借助这两个函数可帮助自动生成store.commit/dispatch
- 导入import {mapMutations,mapActions} from ‘vuex‘
- 在methods中写...mapMutation({事件名：’mutation中的方法名‘})，需要在@click中传入参数

### 5、模块化+命名空间

- 在store文件夹下建立其他类别的vuex模块，需要开启namespaced：true
- 在index文件中引入
- 在vuex实例中用modules注册
- 手动读取模块化vuex时：this.$store.state.namespaced.dataname；this.$store.getters['namespaced/dataname']；this.$store.dispatch('namespaced/dataname',data)
- 用map函数：...mapState('namespaced',['dataname1',dataname2])；...mapGetters('namespaced',['dataname'])；...mapActions('namespaced',{function:'actionF',})

## 六、路由router

### 1、路由的创建

- 安装npm i vue-router

- 在src下建立router文件夹，在router下建index.js文件

- 在js文件中配置代码，引入vue-router，引入需要跳转的组件

- 创建new VueRouter({

  routes:[

  ​	{path:'/router-link'，component：}
  ]
  })

- 在父组件中加入<router-link to='/router-link' active-class="">跳转</router-link>

- 在需要显示子组件的区域加入<router-view></router-view>

### 2、二级路由配置

- 在一级路由下添加children:[{path:'不写斜杠'，component：}]

### 3、路由的query参数

- 在跳转路由时需要携带参数：:to="\`路径?${}\`"
- 或者：:to="{path:'路径',query:{id:001}}"
- 接受：$route.query.

### 4、命名路由

- 在路由配置中添加name：’‘，在配置to的时候可以不写路径，直接写name，但只能用对象的方式写

### 5、props的配置

- 将路径参数返回给vue组件

- ![image-20220102143629792](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220102143629792.png)
- 结构赋值的连续写法{query:{id,title}} 等价于 $router.query.id/title

### 6、编程式路由导航

- 不借助router-link，使用$router自带的push、replace、forward、back、go等函数实现路由跳转

![image-20220102145435570](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220102145435570.png)

### 7、缓存路由组件

- 让不展示的路由组件保持挂载，不被销毁
- 在需要展示的router-view中包裹上\<keep-alive include="组件名"\>
- 缓存多个组件:include="['组件名1'，'组件名2']"

### 8、activated()和deactivated()

- 这两个是路由的生命周期钩子函数
- activated在路由组件被激活时调用，deactivated在路由组件失活时被调用

### 9、路由守卫

- 前置路由守卫router.beforeEach((to,from,next)=>{})
- to是切换时的下一个组件，from是切换时的上一个组件，next是是否允许切换到下一个组件

![image-20220102152858149](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220102152858149.png)

- 后置路由守卫，没有next。可以在切换路由后做一些逻辑操作

![image-20220102152947529](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220102152947529.png)

- 组件内的守卫，在组件中定义函数

![image-20220102154017739](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220102154017739.png)

### 路由的两种工作模式

![image-20220102155850204](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220102155850204.png)
