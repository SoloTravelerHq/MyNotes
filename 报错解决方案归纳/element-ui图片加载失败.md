## element-ui图片加载失败

如下使用el-image会导致图片加载失败，需要使用require

```html
<el-image style="width: 100px; height: 100px" src="../../assets/logo.png"></el-image>
```

加上require

```html
<el-image style="width: 100px; height: 100px" :src="require('../../assets/logo.png')"></el-image>
```

