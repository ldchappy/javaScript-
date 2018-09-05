

### 新建一个vue项目 webpack-simple
~~~
假设已经安装了node.js和webpack
1.cd 一个文件夹
2.vue init webpack-simple 工程名(不能中文)
3.Target directory exists. Continue? (Y/n) 直接回车默认(然后会下载 vue2.0模板，这里可能需要连代理)
4.Project name (vue-test) 直接回车默认
5.Project description (A Vue.js project) 直接回车默认
6.Author 写你自己的名字



安装项目依赖：
一定要从官方仓库安装，npm 服务器在国外所以这一步安装速度会很慢。
npm install
不要从国内镜像cnpm安装(可能会导致后面缺了很多依赖库)
cnpm install
~~~
### 为什么在vue中使用css不起作用
~~~
要加scoped
~~~
### Cannot read property 'get' of undefined
~~~
1.没有引用vue-resource、vue-router
2.在main.js中导入、引用
~~~
### Failed to execute 'open' on 'XMLHttpRequest': Invalid URL
~~~
因为域名'127.0.0.1:3000/',不是localhost:3000/
~~~
### Error in created hook: "TypeError: Cannot read property 'get' of undefined"
~~~
created (){
    this.getGedan()
}
~~~
### 明明已经npm sass-loader node-sass,却报没有找到
~~~
npm install sass-loader node-sass webpack --save-dev
~~~
### module.default/module.exports
~~~
module.default 只能使用一次
module.exports 可以使用多次

------------
使用export default命令，为模块指定默认输出，这样就不需要知道所要加载模块的变量名
let sex = "boy";
export default sex（sex不能加大括号）
//原本直接export sex外部是无法识别的，加上default就可以了.但是一个文件内最多只能有一个export default。
其实此处相当于为sex变量值"boy"起了一个系统默认的变量名default，自然default只能有一个值，所以一个文件内不能有多个export default。
------------
var x = 5;
var addX = function (value) {
  return value + x;
};
module.exports.x = x;
module.exports.addX = addX;
~~~
### 指令
npm install --save-dev style-loader css-loader
npm install vue-router --save-dev



### 博客园看到的vue解决跨域的方法
~~~
要想本地正常的调试，解决的办法有三个：

一、后台更改header
header('Access-Control-Allow-Origin:*');//允许所有来源访问 
header('Access-Control-Allow-Method:POST,GET');//允许访问的方式 　　
这样就可以跨域请求数据了。

二、使用JQuery提供的jsonp  (注：vue中引入jquery，自行百度)
methods: { 
  getData () { 
    var self = this 
    $.ajax({ 
      url: 'http://f.apiplus.cn/bj11x5.json', 
      type: 'GET', 
      dataType: 'JSONP', 
      success: function (res) { 
        self.data = res.data.slice(0, 3) 
        self.opencode = res.data[0].opencode.split(',') 
      } 
    }) 
  } 
} 
通过这种方法也可以解决跨域的问题。

三、使用http-proxy-middleware 代理解决（项目使用vue-cli脚手架搭建）
例如请求的url:“http://f.apiplus.cn/bj11x5.json”

1、打开config/index.js,在proxyTable中添写如下代码：
proxyTable: { 
  '/api': {  //使用"/api"来代替"http://f.apiplus.c" 
    target: 'http://f.apiplus.cn', //源地址 
    changeOrigin: true, //改变源 
    pathRewrite: { 
      '^/api': 'http://f.apiplus.cn' //路径重写 
      } 
  } 
}
2、使用axios请求数据时直接使用“/api”：
getData () { 
 axios.get('/api/bj11x5.json', function (res) { 
   console.log(res) 
 })
通过这中方法去解决跨域，打包部署时还按这种方法会出问题。解决方法如下：
let serverUrl = '/api/'  //本地调试时 
// let serverUrl = 'http://f.apiplus.cn/'  //打包部署上线时 
export default { 
  dataUrl: serverUrl + 'bj11x5.json' 
}
~~~
###  解决本地跨域请求？？试过可以
~~~
1.生成一个build文件夹，里面新建dev-server.js
var proxyMiddleware = require('http-proxy-middleware')
var server = express()

server.middleware = [
        proxyMiddleware(['/personalized'], {target: 'http://localhost:3000', changeOrigin: true}),
];

server.use(server.middleware);
2.生成一个config文件夹，里面新建index.js
dev: {
    env: require('./dev.env'),
    port: 8080,
    proxyTable: {
      '/api': {
        target: 'http://localhost:3000',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
~~~



###Vue-cli开发环境跨域请求
~~~
在 config/index.js 配置文件中

dev: {
    env: require('./dev.env'),
    port: 8080,
    autoOpenBrowser: true,
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    //proxyTable: {},
    //核心代码
    proxyTable:'/apis': {
	    // 测试环境
	    target: 'http://api.veblen.com',  // 接口域名
	    changeOrigin: true,  //是否跨域
	    pathRewrite: {
	        '^/apis': 'apis'   //需要rewrite重写的,
	    }              
	},
    cssSourceMap: false
  }

~~~

### Uncaught ReferenceError: regeneratorRuntime is not defined
~~~
解决方法：
$ npm i --save-dev babel-plugin-transform-runtime

在 .babelrc 文件中添加：
"plugins": [[
    "transform-runtime",
    {
      "helpers": false,
      "polyfill": false,
      "regenerator": true,
      "moduleName": "babel-runtime"
    }
  ]]
~~~
~~~
webstorm里使用vue 工具不识别es6
在script标签里：type="text/ecmascript-6"
~~~
~~~
父组件传值给子组件
在父组件中：
1.注册了子组件  
  import myHeader from "./components/header/header"；
  components:{
    myHeader
  }
2.子组件的别名中绑定所要传的数据 如： :seller = "seller"
  <myHeader :seller="seller"></myHeader>

在子组件中接收：
export default{
  props:{
    seller : Object
  }
}
~~~
~~~
子组件向父组件派发事件
1.子组件中使用$emit派发
  this.$emit('add',event.target)  add是父组件中的事件名
2.父组件中使用v-on:接收
  @add="addFood"   addFood是子组件中的方法

~~~
~~~
获得元素
1.在html中使用ref="xxx"
2.在js中使用$refs.xxx来获得
~~~
~~~
让元素异步渲染
this.$nextTick( () =>{ //$nextTick表明元素已经渲染好
  之后的代码
});
~~~
~~~
transition动画
<transition @:befor-enter="beforEnter" @enter="Enter" @after-enter="afterEnter">
  <div v-show="ball.show" class="ball">
    <div class="inner inner-hook"></div>
  </div>
</transition>
在methods中定义动画动态：
beforEnter(){}
Enter(){}
afterEnter(){}
~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~~~~

~~~

~~~

~~~~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~
~~~

~~~



