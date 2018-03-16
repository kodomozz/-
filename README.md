## 概要
- 记录了一些常见的问题，都是干货，虽然有点乱
- 要更多的原理性问题，如果模拟实现一些基础的api

```
说说盒子模型？
react 生命周期？
requirejs 实现？
居中布局方法？ 怎么居中？
跨域方式？
webpack runtime babel 区别？
require 是提前加载的吗， cmd amd commonjs
require import 的区别
babel-polyfill 和runtime 的区别https://github.com/youngerPlant/-
npm 步骤## 标题文字 ##
react 父元素调用子元素的方法
dispatch 的实现
webpack 是如何异步处理的
dva start的后处理的逻辑
loading dva
react component element 的区别
react render 返回的是什么
```
redux 数据流 [地址](https://segmentfault.com/a/1190000010407887)
webpack 原理？ 如何工作？
```
**原理：**
一切皆为模块，由于webpack并不支持除.js以外的文件，从而需要使用loader转换成webpack支持的模块，plugin用于扩展webpack的功能，在webpack构建生命周期的过程在合适的时机做了合适的事情。

**先了解一下Webpack从构建到输出文件结果的过程：**
1.解析配置参数，合并从shell传入和webpack.config.js文件的配置信息，输出最终的配置信息
2.注册配置中的插件，好让插件监听webpack构建生命周期中的事件节点，做出对应的反应
3.解析配置文件中entry入口文件，并找出每个文件依赖的文件，递归下去
4.在递归每个文件的过程中，根据文件类型和配置文件中loader找出相对应的loader对文件进行转换
5.递归结束之后得到每个文件最终的结果，根据entry配置生成代码chunk
6.输出所有chunk到文件系统

```
jsonp实现原理？
```
首先在客户端注册一个callback, 然后把callback的名字传给服务器。 

此时，服务器先生成 json 数据。 
然后以 javascript 语法的方式，生成一个function , function 名字就是传递上来的参数 jsonp. 

最后将 json 数据直接以入参的方式，放置到 function 中，这样就生成了一段 js 语法的文档，返回给客户端。 

客户端浏览器，解析script标签，并执行返回的 javascript 文档，此时数据作为参数，传入到了客户端预先定义好的 callback 函数里.（动态执行回调函数）
```
### css渲染机制？
```
1、Create/Update DOM And request css/image/js：浏览器请求到HTML代码后，在生成DOM的最开始阶段（应该是 Bytes → characters 后），并行发起css、图片、js的请求，无论他们是否在HEAD里。

_注意：发起js文件的下载request并不需要DOM处理到那个script节点，比如：简单的正则匹配就能做到这一点，虽然实际上并不一定是通过正则：）。这是很多人在理解渲染机制的时候存在的误区_

2、Create/Update Render CSSOM：CSS文件下载完成，开始构建CSSOM

3、Create/Update Render Tree：所有CSS文件下载完成，CSSOM构建结束后，和 DOM 一起生成 Render Tree。

4、Layout：有了Render Tree，浏览器已经能知道网页中有哪些节点、各个节点的CSS定义以及他们的从属关系。下一步操作称之为Layout，顾名思义就是计算出每个节点在屏幕中的位置。

5、Painting：Layout后，浏览器已经知道了哪些节点要显示（which nodes are visible）、每个节点的CSS属性是什么（their computed styles）、每个节点在屏幕中的位置是哪里（geometry）。就进入了最后一步：Painting，按照算出来的规则，通过显卡，把内容画到屏幕上。

以上五个步骤前3个步骤之所有使用 “Create/Update” 是因为DOM、CSSOM、Render Tree都可能在第一次Painting后又被更新多次，比如JS修改了DOM或者CSS属性。

Layout 和 Painting 也会被重复执行，除了DOM、CSSOM更新的原因外，图片下载完成后也需要调用Layout 和 Painting来更新网页。
```

### react 中事件调用的时候，为什么需要bind()
```
如果你不绑定this.handleClick方法，那么在事件发生并且精确调用这个方法时，方法内部的this会丢失指向。
2.这不是React的原因，这是JavaScript中本来就有的。如果你传递一个函数名给一个变量，然后通过在变量后加括号()来调用这个方法，
　此时方法内部的this的指向就会丢失</pre>
```

### 从浏览器打开到页面渲染完成，发生了什么事情。
```
浏览器解析->查询缓存->dns查询->建立链接->服务器处理请求->服务器发送响应->客户端收到页面->解析HTML->构建渲染树->开始显示内容(白屏时间)->首屏内容加载完成(首屏时间)->用户可交互(DOMContentLoaded)->加载完成(load)

```

### 网络安全问题
```
xss：跨站脚本攻击，如果不过滤执行了js代码，可能导致cookie泄露等。防止：过滤
csrf：跨站请求伪造，挟制用户在当前已登录的Web应用程序上执行非本意的操作。防止：设置token、写操作用post、JSON API禁用CORS、禁用跨域请求、检查referrer
```

### 浏览器缓存问题
```

某些服务器不能精确得到资源的最后修改时间，这样就无法通过最后修改时间判断资源是否更新。

Last-modified 只能精确到秒。

一些资源的最后修改时间改变了，但是内容没改变，使用 Last-modified 看不出内容没有改变。

Etag 的精度比 Last-modified 高，属于强验证，要求资源字节级别的一致，优先级高。如果服务器端有提供 ETag 的话，必须先对 ETag 进行 Conditional Request。
```

### let const 区别
```
let不存在变量提升，暂时性死区， 不允许重复性声明
const 一旦声明就几必须初始化，不能留到后面声明
```

### promise setTimeout 异步 [js事件循环机制](http://web.jobbole.com/90951/)
### push, pop实现， promise 的实现？
### js 双向数据绑定实现？ [地址](双向数据绑定实现)
### call apply bind 的原生实现？ [地址](https://segmentfault.com/a/1190000009257663)
```
function objectFactory() {

    var obj = new Object(),

    Constructor = [].shift.call(arguments);

    obj.__proto__ = Constructor.prototype;

    var ret = Constructor.apply(obj, arguments);

    return typeof ret === 'object' ? ret : obj;

}
```

### [各种机制原理](https://github.com/mqyqingfeng/Blog)
```
Function.prototype.call2 = function (context, ...args) {
    context = context || window
    context.__fn__ = this
    let result = context.__fn__(...args)
    delete context.__fn__
    return result
}
```

```
Function.prototype.call2 = function (context) {
    var context = context || window;
    context._fn_ = this;

    var args = [];
    for(var i = 1, len = arguments.length; i < len; i++) {
        args.push('arguments[' + i + ']');
    }

    var result = eval('context._fn_(' + args +')');

    delete context._fn_
    return result;
}
```

### [浏览器缓存机制](https://mp.weixin.qq.com/s/qSN5yaNmuMysG71229qC-Q)

### e.target e.currentTarget 区别 [事件委托](https://www.jianshu.com/p/1dd668ccc97a)
```
  let ul = document.querySelectorAll('ul')[0] 
  let aLi = document.querySelectorAll('li')             ul.addEventListener('click',function(e){ 
  let oLi1 = e.target 
  let oLi2 = e.currentTarget 
})
```

### link @import 的区别？
### CommonJS，AMD，CMD，ES6模块规范? [地址](http://blog.csdn.net/qq_26878975/article/details/72803231)


### [同上](http://blog.csdn.net/jackwen110200/article/details/52105493)

### css 布局？ [css布局]([css实现左侧宽度自适应，右侧固定宽度](https://segmentfault.com/a/1190000008411418)

### 天生的inline-block 元素
```
5.行内元素和块级元素的具体区别是什么？行内元素的padding和margin可设置吗？

   块级元素（block）特性：

    总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示。

    width、height、padding（内边距）、margin(外边距)都可控制。

    内联元素（inline）特性：

    宽度、高度、内边距的padding-top/padding-bottom和外边距的margin-top、margin-bottom都不可改变（也就是padding和margin的left和right是可以设置的）。

    这里还有其他问题。浏览器还有默认的天生inline-block元素（拥有内在尺寸，可设置高宽，但不会自动换行），有哪些元素是天生inline-block元素？

    它们是<input>、<img>、<button>、<textare>、<label> 。
```

###  什么是bfc， 特性， 应用？[bfc](https://www.jianshu.com/p/11e764268c0d)

### 你了解http协议吗？ [http](https://www.cnblogs.com/ranyonsue/p/5984001.html)

### propert attribute 区别？

```
*   property是DOM中的属性，是JavaScript里的对象；
*   attribute是HTML标签上的特性，它的值只能够是字符串；
```
### 网络安全？
```
xss：跨站点攻击。xss攻击的主要目的是想办法获取目标攻击网站的cookie，因为有了cookie相当于有了session，有了这些信息就可以在任意能接进互联网的PC登陆该网站，并以其他人的身份登陆做破坏。预防措施防止下发界面显示html标签，把</>等符号转义。

csrf：跨站点伪装请求。csrf攻击的主要目的是让用户在不知情的情况下攻击自己已登录的一个系统，类似于钓鱼。如用户当前已经登陆了邮箱或bbs，同时用户又在使用另外一个，已经被你控制的网站，我们姑且叫它钓鱼网站。这个网站上面可能因为某个图片吸引你，你去点击一下，此时可能就会触发一个js的点击事件，构造一个bbs发帖的请求，去往你的bbs发帖，由于当前你的浏览器状态已经是登陆状态，所以session登陆cookie信息都会跟正常的请求一样，纯天然的利用当前的登陆状态，让用户在不知情的情况下，帮你发帖或干其他事情。预防措施，请求加入随机数，让钓鱼网站无法正常伪造请求。
```

### hasOwnPropertyNames, for in, Object.keys(), hasOwnProperty, propertyIsEnumerable 区别？
```
    Object.hasOwnPropertyNames：检查自身的包括可枚举，不可枚举， 不包括symble属性(只是属性，不包括方法)
    for in： 所有的包括可枚举和不可枚举，原型上的方法和属性都会遍历
    Ojbect.keys()：自身可枚举的属性
    obj.hasOwnProperty(): 检查是否是自身的属性，包括可枚举,不可枚举的，(只是属性，不包括方法)
    obj.propertyIsEnumerable()是用来检测属性是否属于某个对象的,如果检测到了,返回true,否则返回false. 
    - 这个属性必须属于实例的,并且不属于原型. 
    - 这个属性必须是可枚举的,也就是自定义的属性,可以通过for..in循环出来的. 
```

### 双向数据绑定demo

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<input type="text" id="demo">
<p id="display"></p>
<script>
    var obj={};
    var bind=[];
    //触发obj对象set和get方法的时候，趁机来输出或修改bind数组的内容
    Object.defineProperty(obj,'s',{
        set:function(val){
            bind['s']=val;
        },
        get:function(){
            return bind['s'];
        }
    })
    var demo=document.querySelector('#demo');
    var display=document.querySelector('#display');
    //#demo的value值与bind['s']绑定，#display的innerHTML也与bind['s']绑定。
    demo.onkeyup=function(){
        obj['s']=demo.value;//触发了obj的set方法，等于#demo的value值赋值给bind['s']。
        display.innerHTML=bind['s'];
    }

</script>
</body>
</html>
```