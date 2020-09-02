# jQuery基础

> 是一个JS库，library，是封装好的特定的集合（方法和函数），区别于原生JS
>
> 为了快速方便的操作dom

**常见的JS库**

~~~~js
//jQuery,Prototype,YUI,Dojo,Ext JS,移动端的zepto
~~~~

**jQuery的优点**

~~~~js
/*
1.轻量级，核心文件在几十kb，不会影响页面加载速度
2.跨浏览器兼容，基本兼容了现在主流的浏览器
3.链式编程，隐式迭代
4.对事件、样式、动画支持，大大简化了DOM操作
5.支持插件扩展开发，有丰富的第三方插件：树形菜单，日期控件，轮播图
6.免费，开源
*/
~~~~

### jQuery的使用

~~~~js
//jQuery的入口函数  两种写法一样
//相当于原生js的DOMContentLoaded
//写多个入口函数，不会覆盖，原生js会
$(function(){
    //入口函数
})
$(document).ready(function(){
	//传统方式
})
~~~~

>  jQuery的顶级对象$,$是jQuery的别称，在代码中可以使用jQuery代替$，但为了方便通常直接使用$

### jQuery核心函数$()

~~~~js
//1.接收一个函数（入口函数

//1.接收字符串选择器
$('#id');
//2.接收字符串代码片段
$('<p>一个p</p>');

//3.接收一个DOM元素
把原生DOM对象包装成jQuery对象
~~~~



### jQuery对象和DOM对象

~~~~js
/*
1.用原生js获取的对象即 DOM对象
2.用jQuery获取的对象即 jQuery对象，本质是利用$对DOM对象包装后产生的对象，以伪数组形式存储
3.jQuery对象只能使用jQuery方法，DOM对象使用原生JS属性和方法
*/
/*
DOM对象和jQuery对象之间可以相互转化
原生js比jQuery大，原生的一些属性和方法jQuery没有封装，可以将jQuery对象转换为DOM对象

1.DOM转jQuery
获取DOM对象
==>  $(DOM对象)

2.jQuery转DOM
$('div')[index]
$('div').get(index)
*/
~~~~

### jQuery常用API

#### jQuery选择器

~~~~js
//jQuery基础选择器
$('选择器')//直接写css选择器，要带引号
$("#id")
$("*")
$(".class")
$("div")
$("div,p,a")
$("li.current")

//子代 后代选择器
$("ul li")
$("ul>li")

//jQuery筛选选择器
:first//获取第一个元素
:last//获取最后一个元素
:eq(index)//选择到索引号的元素
:odd//选择到索引号为奇数的元素
:even//选择到索引号为偶数的元素
:checked//筛选选中的元素
:empty//内容为空的元素
:parent//有文本内容，有子元素的元素
:contains('neirong')//包含指定文本内容的
:has('span')//包含指定子元素的元素

//jQuery筛选方法
parent()//查找父级
parents()//祖先
children(selector)//相当于>,最近一级子元素
find(selector)//相当与后代选择器
siblings(selector)//查找兄弟节点，不包括自己本身
nextAll([expr])//查找当前元素之后的所有同辈元素
prevtAll([expr])//查找当前元素之前的所有同辈元素
hasClass(class)//检查当前元素是否含有某个特定的类，有返回true
eq(index)//相当于:eq(index)
~~~~

#### jQuery样式操作

~~~~js
//简单样式修改，必须带引号，值是数字可以不带
$('div').css('属性')//不给值则返回当前属性的值
//jQuery设置 单个样式

$('div').css('属性','值')//隐式迭代：遍历内部DOM元素（伪数组）的过程
//jQuery设置 多个样式
$('div').css({
    width:400,
    height:400,
    backgroundColor:'red',//复合属性 驼峰，值不是数字须带引号
    'font-size':'20px'
});

//通过设置类更改样式，用双引号
$('div').addClass('className')//不需要加.,添加类
$('div').removeClass('className')//删除类
$('div').toggleClass('className')//切换类，有删无加
~~~~

#### jQuery动画效果

~~~~js
/*
一般情况下不带参数
speed:'slow' 'normal' 'fast' 毫秒数：1000
easing:默认慢快慢'swing',匀速linear
fn:回调函数，动画完成时执行，每个元素执行一次
*/
//显示隐藏
.show([speed],[easing],[fn])//让元素显示
.hide([speed],[easing],[fn])//让元素隐藏
.toggle([speed],[easing],[fn])//显示<==>隐藏

//滑动
.slideDown([s],[e],[fn])//下滑动
.slideUp([s],[e],[fn])//上滑动
.slideToggle([s],[e],[fn])//切换滑动

//淡入淡出
.fadeIn([s],[e],[fn])
.fadeOut([s],[e],[fn])
.fadeToggle([s],[e],[fn])
.fadeTo(s,opacity,[e],[fn])//修改透明度

//自定义动画
animate(params,[speed],[easing],[fn])
/*
params:以对象的形式传递
*/
$("div").animate({
    left:500,
    top:200,
    opacity:0.5,
    width:500//关键字hide toggle
},500 )

//动画排队
stop()//结束上一次动画，写在动画前面
//第一参数是否停止后续，第二参数是否继续当前
/*false(false false)立即停止当前动画，进行后续动画
true(true false)停止后续所有动画*/
/*false true立即完成当前动画，继续后续动画*/
/*true true立即完成当前动画，停止后续动画*/
delay(2000)//延迟
~~~~

#### jQuery属性操作

~~~~js
//获取元素固有的属性，truefalse：checked，selected，disabled
.prop("属性")//能操作属性和属性节点
//设置元素固有的属性
.prop("属性","属性值")

//获取设置元素自定义属性
.attr("属性")
.attr("属性","属性值")

//数据缓存，存放在元素的内存里
.data("username","andy")
.data("username")
//可以直接获取H5的data-xxx属性，去掉data-
~~~~

#### jQuery内容文本值

~~~~js
//普通元素内容，相当于innerHTML
html()//获取
html("值")//修改

//普通元素文本内容，相当于innerText
.text()
.text("zhi")

//获取修改表单值
.val()
.val("zhi")
~~~~

### jQuery静态方法

##### each(obj,[callback])

~~~~js
//each()遍历元素
$("div").each(function(index,domEle){//获取的时DOM对象
    xxx;
})
//$.each()遍历元素，主要用于遍历数据，处理数据
$.each($("div"),function(i,ele){
    //i索引，ele元素
   //遍历数组，遍历对象 
    //不支持在回调函数加工数据，return数组
});
//返回值为遍历的数组本身
~~~~

##### map(arr|obj,callback)

~~~~js
$.map(obj,function(value,index){
    return ;//默认返回值为空数组，可以通过return返回加工后的数据数组
})
~~~~

##### 其他静态方法

~~~~js
//去除两端空格
$.trim(str)//返回新字符串
//判断是否是window对象
$.isWindow()//返回布尔值
//判断是否是真数组
$.isArray()
//判断是否是函数
$.isFunction()
//暂停入口函数的执行
$.holdReady(true);//true暂停
~~~~



#### jQuery元素操作

~~~~js
//创建元素
var li =$("<li>sjad</li>")
 
//添加元素1.内部添加
$("ul").append(li);//appendChild
$("ul").prepend(li);//insertBefore

li.appendTo('ul');//appendChild
li.prepend('ul');//insertBefore
//添加元素2.外部添加
$(".test").after(div);//在元素后添加
$(".test").before(div);//在元素之前添加

li.after($(".test"));//在元素后添加
li.before($(".test"));//在元素之前添加

//删除元素
$("ul").remove('.#')//删除指定的元素，自杀
$("ul").empty()//删除指定的元素的所有子节点，不删除本身
$("ul").html("")//同empty

//克隆节点
$().clone();//true深,false浅
//浅复制仅复制元素，深复制复制元素和元素绑定的事件
//替换节点，先新建，后替换
$(tihuan).replaceWith();
replaceAll(tihuan)
~~~~
### jQuery尺寸、位置操作

~~~~js
width()/height()//元素的宽高，只算width，height
innerWidth()/innerHeight()//包括padding
outerWidth()/outerHeight()//包括padding，border
outerWidth(true)/outerHeight(true)//包括padding，border，margin

//参数为空，即获取，返回数字型
//有参为数字，则修改，不带单位


//位置
offset()//相对于窗口文档的偏移距离
position()//相对于有定位的父级的偏移距离,       只能获取不能设置
scrollTop()/scrollLeft()//元素被卷去的头部和左侧

$(".son").offset()
$(".son").offset().top
$(".son").offset({
    top:200,
    left:200
})

//返回顶部，获取网页偏移位body,html,浏览器兼容+
$("body,html").stop().animate({
    scrollTop:0
})
~~~~
### jQuery事件

#### jQuery事件

~~~~js
//单个注册事件
$("div").click(function(){/*事件处理程序*/})

//多个事件的绑定
//事件处理on()绑定事件
element.on(events,[selector],fn)
/*
events:一个或多个用空格分割的事件类型
selector:元素的子元素选择器
fn:回调函数，绑定在元素上的侦听函数
*/
$("div").on({
    mouseenter:function(){
        $(this).css("background","skyblue"); 
    },
    click:function(){
        $(this).css("background","purple");
    },
    hover:function(){},function(){}
})

//优点：1.可以绑定多个事件
//2.可以进行时间委派操作。把原来加给子元素的事件绑定在父元素身上，即把事件委托给父元素
$("ul li").click(function(){});
$("ul").on("click","li",function(){
//处理程序,绑定在ul,触发在li
})
//bind(),live(),delegate()是旧版本的方法，最新版本使用on

//3.on可以给未来动态创建的元素绑定事件

//单次事件绑定one()
 $("p").one("click",function(){})//只能触发事件一次

//自动触发事件
//1. 元素.事件()
$("div").click();
//2. 元素.trigger("事件")
$("div").trigger("click");//会触发元素默认行为和事件冒泡，a链接不可以触发默认事件
//3. 元素.triggerHandler("事件")，区别是不会触发元素默认行为和事件冒泡
$("div").triggerHandler("click");

//事件命名空间
//事件必须通过on绑定
//在事件后添加.zs
$('div').on('click.zs',function(){})
$('div').trigger('click.zs');
//利用trigger触发子元素带命名空间的事件，父元素带相同命名空间的事件也会触发
//利用trigger触发不带命名空间的事件，子元素和父元素所有相同类型的事件都会被触发
~~~~

#### 自定义事件

~~~~js
//通过on绑定事件
//事件自动触发trigger
~~~~

~~~~js
//事件解绑off()
$("div").off();//解除div身上的所有事件

//传一个参数，会移除所有指定类型的事件
$("div").off("click");//解除div身上的单个事件

//两个参数，会移除所有指定类型的指定事件
$("ul").off("click","li")//解绑事件委托
~~~~

#### jQuery事件对象，冒泡和默认行为

~~~~js
//事件被触发，就会有事件对象产生
ele.on(events,[selector],function(event){})

//阻止默认行为：event.preventDefault()或者return false;
//阻止冒泡：event.stopPropagation()或者return false;
~~~~

#### jQuery对象拷贝

~~~~js
$.extend([deep],target,obj1,[objN])//把obj给target
/*
deep:true深拷贝，拷贝完整的数据，有不重名的属性就合并，默认false浅拷贝，复杂数据类型只拷贝地址，修改对象会影响拷贝的
target:目标对象
object1:要拷贝的对象
*/
~~~~

### jQuery异步请求

~~~~js
$.ajax({
    url:,
    mothed:,
    data:{},
    success:function(){},
    error:function(){}
})
$.getJson('url',{},function(){})//json javascript 对象
$.get
$.post
~~~~



#### jQuery多库共存

~~~~js
//1.把里面的$符号同一改写为 jQuery
//2.jQuery变量规定新的名称：$noConflict()释放$ 
//var xx=$.noConflict();自定义符号
~~~~

#### jQuery插件

~~~~js
//jQuery插件库 http://www.jq22.com/
//jQuery之家 http://www.htmleaf.com/推荐

//1.下载插件
//2.打开下载文件中的示例页面查看源码
//3.复制css，js文件，复制引入链接，复制js调用代码
//4.复制html结构
//5.查看配置参数，按需修改
~~~~

#### 图片懒加载--提升性能

> 页面滑动到可视区再显示

~~~~js
//easylazyload.js
//图片的src替换成data-lazy-src
//js引入文件和js调用必须写到DOM元素（图片）最后面
~~~~

#### 全屏滚动fullpage.js

~~~~js
//github:https://github.com.alvarotrigo/fullPage.js
//中文翻译版:http://www.dowebok.com/demo/2014/77/
~~~~

#### bootstrap JS 插件

> bootstrap框架依赖jQuery开发的，里面插件的使用，必须引入jQuery文件

~~~~js
//http://v3.bootcss.com   
~~~~

#### todolist案例

~~~~js
//按下回车 把完整数据 存储到本地存储
  //读取本地存储的数据
//利用事件对象判断用户按下回车键13
//声明一个数组，保存数据
//先要读取本地存储原来的数据（声明函数getData()，放入数组
//把从表单获取的数据追加到数组
//把数组存储到本地存储（声明saveData()

//声明load函数，用于渲染加载，便于调用
//读取本地存储数据，（记得转化为对象格式
//遍历数据$.each(),生成li添加ol
//加载遍历之前清空，$("ol").empty(),否则会重复渲染

//点击删除键，不是删除li，而是删除本地存储对应的数据
//核心：获取本地数据，删除对应的数据，保存给本地存储，重新渲染列表li
//自定义属性记录索引号
//根据索引号删除相关数据--数组的splice(i,1)方法

//点击复选框，修改数据存储，再渲染（事件委托
//获取本地存储数据，修改属性，保存
//load加载函数中判断done属性

//统计已经完成的个数和未完成的个数
//要在load函数中统计
//声明两个变量todoCount代办doneCount已完成
//遍历本地存储数据，done为false，todoCount++，反之
//修改相应元素text()
~~~~



#### 电梯导航案例72

~~~~js
$(this).index()//得到当前元素的索引号
.change()//状态改变事件
.click()//给元素添加点击事件
.mouseover//添加鼠标经过事件
.hover([over,]out)//over鼠标移入触发函数，out鼠标移出触发函数，只写一个函数则经过离开都触发（toggle
.keyCode()//回车键13
~~~~

