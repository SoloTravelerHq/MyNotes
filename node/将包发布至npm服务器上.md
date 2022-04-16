## 将包发布至npm服务器上

### 1、在npm官网注册账号

- [npm官网]: https://www.npmjs.com/

<img src="C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220226131948726.png" alt="image-20220226131948726" style="zoom:50%;" />

- 之后再填入邮箱中的密码，注册成功

### 2、在终端发布包

- 在终端输入**npm config get registry**检查当前使用的是否是npm服务器

![image-20220226132627029](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220226132627029.png)

- 若当前使用的不是npm服务器，在终端输入**nrm use npm**转到npm服务器。若没有装nrm，在终端输入npm i nrm -g，全局安装nrm
- 在终端输入**npm login**登录，然后输入之前注册的账号、邮箱、密码

![image-20220226133843292](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220226133843292.png)

- 终端切换到包的根目录，输入npm pulish发布包
  - 在发布之前需要检查包名是否重复，在npm官网上搜索你要发布的包名，若存在，则需要重新修改包名再发布。

![image-20220226140425179](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220226140425179.png)

- 在个人主页上可以看到，我们已经发布成功了

![image-20220226140510534](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220226140510534.png)

### 3、删除已发布的包

- 在终端输入**npm unpublish 包名  --force**，删除指定的包

![image-20220226141142212](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220226141142212.png)

- 上传的包只能在72小时内删除，超过这个时间就不能删除了
- 删除的包需要在24小时后才能重新发布
- 这边希望大家不要在npm上发布没有意义的包，作为练手的包发布后应当及时删除