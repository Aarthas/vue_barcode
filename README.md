# vue 框架，一维码生成器




> vue 框架下一维码和二维码的使用，
二维码是vux自带组件，
因为jquery等js一维码库大多数根据dom节点来实现，所以不能用在vue框架上，现做一个canvas版本的一维码，code128格式，根据算法与h5 canvas api画出来的一维码。


### 优点

> 可扩展性好，可适配于react，angular，微信小程序等其他框架。
代码量少，一个js文件，2kb。

#### 扩展

* [ vue版本的一维码生成器 ](https://github.com/Aarthas/vue_barcode)

* [小程序版的一维码生成器](https://github.com/Aarthas/wxmini_barcode_qrcode)



![](https://raw.githubusercontent.com/Aarthas/vue_barcode/master/preview.jpeg)

#### 使用


``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
