## **jQuery** **事件**

### **jQuery**事件注册

> 语法：element.事件(function(){})

```
$(“div”).click(function(){  事件处理程序 }) 
```

> 其他事件和原生基本一致。
>
> 比如mouseover、mouseout、blur、focus、change、keydown、keyup、resize、scroll 等

### **事件处理** **on()** **绑定事件**

> on() 方法在匹配元素上绑定一个或多个事件的事件处理函数

> 语法：element.on(events,[selector],fn)

```
1. events:一个或多个用空格分隔的事件类型，如"click"或"keydown" 。

2. selector: 元素的子元素选择器 。

3. fn:回调函数 即绑定在元素身上的侦听函数。 
```

**on() 方法优势1：**

1、可以绑定多个事件，多个处理事件处理程序。 

```
同处理程序： $('div').on('mouseenter click',function () {
			console.log(123);
		});

不同处理程序： $(“div”).on({

  mouseover: function(){}, 

  mouseout: function(){},

  click: function(){}  

});       
```

**on() 方法优势2：**

> 可以事件委派操作。事件委派的定义就是，把原来加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素。

```
$('ul').on('click', 'li', function() {

    alert('hello world!');

}); 

```

> 在此之前有bind(), live(),delegate()等方法来处理事件绑定或者事件委派，最新版本的请用on替代他们。  

**on() 方法优势3：**

> 动态创建的元素，click()没有办法绑定事件，on() 可以给动态生成的元素绑定事件

```
 $(“div").on("click",”p”, function(){

     alert("俺可以给动态生成的元素绑定事件")

 });
```

### 案例：发布微博案例

> ①点击发布按钮， 动态创建一个小li，放入文本框的内容和删除按钮， 并且添加到ul 中。
>
> ②点击的删除按钮，可以删除当前的微博留言。

### **事件处理** **off()** **解绑事件**



> off() 方法可以移除通过 on() 方法添加的事件处理程序。

```
$("p").off() // 解绑p元素所有事件处理程序

$("p").off( "click")  // 解绑p元素上面的点击事件 后面的 foo 是侦听函数名

$("ul").off("click", "li");   // 解绑事件委托
```

> 如果有的事件只想触发一次， 可以使用 one()来绑定事件。

JQ注册事件：on

$（元素）.on('事件类型', ['子元素'], function () {});【好处：绑定多个，事件委派，动态创建的元素也有事件】

解绑：$（元素）.off();

### **自动触发事件trigger()** 

> 有些事件希望自动触发, 比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发

> element.click()  // 第一种简写形式

> element.trigger("type")//第二种自动触发模式

```
$("p").on("click", function () {

  alert("hi~");

}); 

$("p").trigger("click"); // 此时自动触发点击事件，不需要鼠标点击

$('div').triggerHandler('click');// 自动触发事件【这种触发事件不会触发默认行为】
```

## **jQuery**事件对象

> 事件被触发，就会有事件对象的产生。
> 【event==》事件对象】

```
element.on(events,[selector],function(event){})       
```

```
阻止默认行为：event.preventDefault()   或者 return  false 

阻止冒泡： event.stopPropagation()      
```

事件注册：

​	$（元素）.click(function () {});

​	$（元素）.on('click','子元素',function () {});

​	$（元素）.off();

​	自动触发事件：$（元素）.click();

​				  $（元素）.trigger('click');

​				  $（元素）.triggerHandler('click');

​	事件对象：$（元素）.click(function (e) {e});

## **jQuery** **其他方法**

> jQuery 插件

### **jQuery**插件

jQuery 功能比较有限，想要更复杂的特效效果，可以借助于 jQuery 插件完成。 

注意: 这些插件也是依赖于jQuery来完成的，所以必须要先引入jQuery文件，因此也称为 jQuery 插件。

**jQuery** **插件常用的网站：**

1.  jQuery 插件库  http://www.jq22.com/     

2.  jQuery 之家   http://www.htmleaf.com/  

**jQuery** **插件使用步骤：**

1.  引入相关文件。（jQuery 文件 和 插件文件）    

2.  复制相关html、css、js (调用插件)。

### 图片懒加载或者（BOOTSTRAP插件）

（图片使用延迟加载在可提高网页下载速度。它也能帮助减轻服务器负载）

当我们页面滑动到可视区域，再显示图片。

我们使用jquery 插件库  EasyLazyload。 注意，此时的js引入文件和js调用必须写到 DOM元素（图片）最后面

注意：

​	1、要引入JQuery

​	2、插件JS【js引入文件和js调用必须写到 DOM元素（图片）最后面】

​	3、将图片 src 替换为 data-lazy-src

​	4、调用lazyLoadInit(）

### BOOTSTRAP插件

<https://www.bootcss.com/>

​	1、引入CSS、引入JQ、引入JS

​	2、.container

​	3、复制粘贴

# Zepto 

**Zepto**是一个轻量级的 **针对现代手机端浏览器的 JavaScript 库**。

因为 Zepto 封装了移动端的手势模块，直接把很多手机端手势直接封装成了事件，我们可以直接使用。

Zepto 中文官网地址：https://www.html.cn/doc/zeptojs_api/

## 浏览器支持情况

手机端支持良好，PC端最好不要使用.

### 使用 zepto 步骤

1. 引入 `zepto.js` 核心库。
2. 引入 `zepto.touch.js` 移动端手势模块。
3. 新建 `<script>` 标签写业务代码。

将之前的移动端banner , 实现一遍

# justdoit

$('a').trigger('click')并不能触发a标签中内容的点击事件，只是相当于触发了a本身的onclick，而不是像用户点击一样的事件。如果想要触发click事件，得把trigger绑定到a标签的子元素sapn上面，如：

<a><span>链接</span><a>

