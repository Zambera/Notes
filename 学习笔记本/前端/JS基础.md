# JS基础

## ECMAScript

使用方式

> 写在body尾部，同一script标签只能嵌入或是导入

1. 直接写在HTML标签内
2. 嵌入script写在body尾部
3. 引入外部文件.js

 

~~~~js
/*
Number整型，浮点型
数值.toFixed(n)四舍五入方法，n保留小数位数
parseInt()第一个字符不是数字，空字符串NaN
parseFloat()第一个小数点有效，只解析十进制，会返回整数
new Number()强转，参数Data返回毫秒数
NaN，任何数除以非数值（字符串，undefined，object）返回NaN
NaN不等于任何值包括本身
isNaN()参数为数字false(空值null数字符串会转化)，其他true
isFinite()(可转化)有限数字true，NaN，±无穷大false
布尔值无初始值或0 -0 null "" false undefined NaN=>false

*/
/*
StringObj
.length属性
.trim()方法删除首尾空格，不改变原本字符串，返回字符串
.charAt(index),超出范围返回空字符串
.indexOf(串,开始位置),返回字符串首次出现位置
.lastIndexOf(串,开始位置)返回最后出现位置，从后往前
.search()检索子串或正则表达式，返回起始位置，找不到则-1
.substring(start,end),参数为正 负值视0，返回s到e-1的串
.arr1.concat(arr2,arr3)连接数组，返回新的数组副本，不改变原数组
.substr(start,length)从start下标处返回指定长度字符串
.replace(''|正则,rep)替换一次或全局匹配，返回替换后的字符串
.toLowerCase()
.toUpperCase()

obj.toString()返回字符串，null和undefined不行
String(obj)

*/
~~~~

### 数组

~~~~js
var arr=new Array();
var arr=new Array("saab","volvo");
var arr=["saab","volvo"]
/*
arr.length返回元素个数
arr.join(",")元素放入字符串，分隔符分割
arr.sort()对数组排序，根据UniCode，返回新数组
arr.push(1,2,3)数组尾部添加新元素，返回新的长度
arr.pop()删除并返回最后一个元素
arr.shift()删除返回第一个元素
arr1.concat(arr2,arr3)连接数组，返回新的数组副本，不改变原数组
arr.reverse()将数组倒序，会改变原数组
arr.toString()返回数组的字符串形式
arr.indexOf(值,[fromindex])返回第一个匹配项的索引，无-1
*/

//真数组和伪数组的转换
//1.真数组转伪数组
[].push.apply(obj,arr)
//2.伪数组转真数组
[].slice.call(obj)
~~~~

### 函数

~~~~js
//普通定义
function f(){}
//构造函数(二次解析，新建了函数对象)
var f=new Function('canshu','canshu','方法体');
//匿名函数（ifelse）
var f=function(){}
~~~~



弹窗

~~~~js
alert 无输入框，单个参数，无返回值，仅确认按钮
prompt有输入框，可两个参数，确认返回string输入字符串，取消返回null
comfirm无输入框，单个参数，确认返回true，取消返回false
~~~~

错误

~~~~js
Error.message//错误信息
Errir.name//异常名
Error.toString()

rangeError//范围错误
referenceError//引用错误
SyntaxError//语法错误

object instanceof 
try{
    //可能产生异常的语句
}catch(Error){
    //处理异常
}finally{
    //出口，必定执行
}
~~~~



## BOM

~~~~js
//BOM的顶级元素window
~~~~

### window对象

~~~~js
//全局变量和函数都是window的属性和方法
//window本身有name属性

//窗口加载事件
window.onload//可以将js代码随意放置，传统方式实现最后一个注册事件
window.addEventListener('load',function(){
    //等页面内容全部加载完毕，包括DOM元素，图片，flash，css
})
document.addEventListener('DOMContentLoaded',function(){
    //ie9以上支持
    //仅当DOM加载完成触发，不包括样式表，图片，flash
    //当页面的图片较多，用户访问到onload触发可能需要较长时间
    //交互效果就难以实现，影响用户体验，DOMContentLoaded较合适
    //速度比load块
})

//窗口改变大小事件
window.addEventListener('resize',function(){
    //响应式布局
    window.innerWidth//当前屏幕宽度
})
~~~~

#### 定时器

~~~~js
window.setTimeout(fn,ms);//定时器到期后调用函数
//window可以省略
//setTimeout('调用函数',等待毫秒数);
clearTimeout();
var myTime=setTimeout("disptime()",5*60*100);
//setInterval('函数',毫秒数);
clearInterval();
~~~~

#### history对象

> 有关客户访问过的url的信息

~~~~js
//OA系统可能用到
back();//前一个
forward();//后一个
go();//指定-1back，1forward
length
~~~~

#### location对象

> 有关当前url的信息

~~~~js
protocal://host[:port]/path/[?query]#fragment
/*
protocol通信协议
host主机（域名）
port端口号http默认80
path路径由/隔开，主机上一个目录或文件地址
query参数，以键值对形式，用&分割
fragment片段，常见于链接锚点
*/
/*location的重要属性和方法*/
.href//返回完整URL
.host//返回主机域名和端口号
.hostname//返回主机名
.pathname//返回路径
.search//返回参数
.hash//返回片段
.assign('www.cc.com');//页面重定向方法，记录浏览历史可后退
.replace('www.cc.com');//不记录浏览历史，不可以后退
.reload();//重新加载页面，相当于刷新，默认false，true强制刷新
~~~~

#### navigator对象

~~~~js
//访问设备识别
.userAgent//浏览器和系统信息 
~~~~



window.open("弹出窗口url","窗口名称","窗口特征")方法

~~~~js
window.open("弹出窗口url","打开方式","窗口特征")//方法
/*
窗口名称==
跳转方式：_self默认
窗口特征：
height=,width=
left,top
toolbar=yes|no|1|0浏览器工具栏
scrollbars滚动条
location
status
menubar菜单栏
resizable尺寸调节
titlebar标题栏
fullscreen全屏
*/
window.close();
window.setTimeout();
window.set
~~~~

#### document对象

**link**

~~~~js
document.referrer前一个url
document.URL
document.domain
~~~~

~~~~js
.getElementById()
.getElementsByName()
.getElementsByTagName()
.write()
~~~~

### Date对象

~~~~js
var today = new Date();
console.log(today);
var tdate = new Date("september 1,2013,14:58:12");
console.log(tdate);
getDate()//返回日期1-31
getDay()//返回星期0-6
getHours()//返回小时数0-23
getMinutes()//返回分钟0-59
getSeconds()//返回秒数0-59
getMonth()//返回月份0-11
getFullYear()//返回年份
getTime()//返回毫秒数
~~~~

Math对象

~~~~js
ceil();//向上取整
floor();//向下取整
round();//四舍五入为最接近的数
random();//返回(0-1)间的随机数
~~~~


## DOM

~~~~js
DOM的顶级元素document
~~~~

~~~~js
parentNode()
childNodes
firstChild
lastChild
nextSibling
lastSibling
节点名nodeName
节点类型nodeType
节点值nodeValue
元素1属性2文本3
~~~~

~~~~js
//创建
//document.write
//innerHTML
createElement(tegName)
//增
A.appendChild(b)
insertBefore(A,B)
cloneNode()
//删
nodeParent.removeChild(node)
replaceChild(newNode,oldNode)

//查
getElementById
getElementsByTagName

querySelector
querySelectorAll

parentNode
children
previousElementSibling
nextElementSibling
//属性操作
setAttribute('属性名','属性值')
getAttribute('属性名');
removeAttribute

//样式
element.style.
document.defaultView.getComputedStyle(ele,伪类).属性//firefox
.currentStyle.属性

//属性
offsetLeft
offsetTop
offsetHeight
offsetWidth
offsetParent
scrollTop
scrollLeft
clientWidth
clientHeight
~~~~

### 事件

~~~~js
//鼠标事件(也是属性)
onclick
//鼠标经过事件
onmouseover//经过自身盒子，和子盒子也触发（会冒泡
onmouseenter//只经过自身盒子触发（不会冒泡

onmouseout
onmouseleave//不会冒泡
onfocus
onblur
onmousemove
onmouseup
onmousedown

//禁止复制网页文本，使用e.preventDefault()阻止事件默认行为
//鼠标右键菜单
contextmenu
//选中文字
selectstart


//键盘事件
//up,down不区分字母大小写，press区分
onkeyup//按键弹起
onkeydown//按键按下
onkeypress//按键按下，不识别功能键，如ctrl，shift alt，左右箭头
keydown->keypress->keyup//执行顺序
~~~~

### 事件高级

#### 注册事件

~~~~js
//传统方式注册事件
//注册事件的唯一性，给相同元素注册同一类型事件，后者覆盖前者
ele.onclick=function(){}
//方法监听注册事件,ie9前attachEvent，按注册顺序依次执行
eventTarget.addEventListener(type,listener[,useCapture])
/*
type:事件类型字符串：click...
listener:事件处理函数，事件发生时调用
useCapture:可选参数，布尔，默认false
*/
//==>
//addEventListener内的函数不需要调用，不用加括号
bt.addEventListener('click',function(){
    alert('');
})

//不推荐使用，仅ie9前可用
eventTarget.attachEvent(eventNameWithOn,callback)
/*
eventNameWithOn:事件类型字符串，onclick
callback:回调函数，事件处理函数
*/

//兼容性结局方案
//封装兼容函数
function addEventListener(element,eventName,fn){
    //判断当前浏览器是否支持addEventListener方法
    if(element.addEventListener){
        element.addEventListener(eventName,fn);//第三参数默认
    }else if(element.attachEvent){
        element.attachEven('on'+eventName,fn);
    }else{
        //相当于element.onclick=fn;
        element['on'+eventName]=fn;
    }
}
//兼容性处理原则，优先大多数 浏览器，再处理特殊浏览器
~~~~

删除事件

~~~~js
//传统方式解绑事件
ele.onclick=null;
//方法监听方式解绑事件,不能使用匿名函数
eventTarget.removeEventListener(type,listener[,useCapture]);
//ie9
eventTarget.detachEvent(eventNameWithOn,callback)
~~~~

DOM事件流

~~~~js
//onclick和attachEvent只能获取冒泡阶段
eventTarget.addEventListener(type,listener[,useCapture])
useCapture=true//捕获
//onblur,onfocus,onmouseenter,onmouseleave等事件没有冒泡
~~~~

事件对象

~~~~js
//事件对象写在function(e)里，e可自己命名
//事件对象系统创建，不需要传参
//事件对象是事件一系列相关数据的集合，例如鼠标坐标，键盘键入
//ie678==>window.event
e=e||window.event//兼容性处理

//常见的事件对象的属性和方法
e.target//触发事件的对象，可能返回绑定元素的子元素
e.srcElement//ie678
this//绑定事件的对象，是不变的，两者不同
e.currentTarget==this;//有兼容性问题
e.type//返回事件的类型，不带on

//组织默认行为（事件），不让链接跳转，或按钮提交
e.preventDefault();//dom标准写法
e.returnValue//ie678
return false;//仅传统注册事件

//阻止冒泡
e.stopPropagation();//标准
window.event.cancelBubble=true//ie678
~~~~

**鼠标事件对象 **

~~~~js
//MouseEvent
e.clientX//距浏览器窗口可视区左边的距离
e.clientY//距浏览器窗口可视区上边的距离
e.pageX//相对于文档页面的X==>ie9
e.pageY//相对于文档页面的Y==>ie9
e.screenX//相对于电脑屏幕
e.screenY//相对于电脑屏幕

//KeyBoradEvent
key//不兼容性
keyCode//返回键的ACSII码

~~~~

事件委托

~~~~js
//不是每个子节点单独设置事件监听器，而是事件监听器设置在父节点上，利用冒泡原理影响每个子节点，只操作一次DOM
~~~~

## axios

~~~~js
//基于promise的HTTP库，可以用于浏览器和nodejs

1.从浏览器中创建XMLHttpRequests
2.从node中创建http请求
3.支持Promise API
4.拦截请求和相应
5.取消请求
6.自动转换JSON
7.客户端支持防御  XSRF:Cross-site request forgery跨站请求伪造

$('.getBtn').click(function() {
                axios.get('/role')
                    .then((res) => {
                        console.log(res);
                    }).catch((err) => {
                        console.log(err);
                    })
            })
            $('.postBtn').click(function() {
                axios.post('/role', {
                    roleName: '超人',
                    desc: 'superman'
                }).then((res) => {
                    console.log(res);
                }).catch((err) => {
                    console.log(err);
                })
            })
axios({
                    url: '/role',
                    method: 'put',
                    data: {
                        id: 1,
                        roleName: 'Xzhan',
                        desc: 'wui'
                    }
                }).then((r) => {
                    console.log(r);
                }).catch((err) => {
                    console.log(err);
                })
~~~~



## 网页特效

#### 元素偏移量offset

~~~~js
//主要用于获取元素位置
element.offsetParent//返回元素的父元素（有定位的，否则返回body
//获取带有定位的父元素的偏移量（不带单位
element.offsetTop;//元素距离父元素上边的距离
element.offsetLeft;//元素距离父元素左边的距离
//获取元素的宽高
element.offsetHeight;//元素的高度包括padding，border
element.offsetwidth;//元素的宽度包括padding，border
//只可读，不可写
~~~~

####  元素可视区client

~~~~js
//主要用于获取元素大小
element.clientTop;//上边框宽度
element.clientLeft;//左边框宽度
element.clientWidth;//元素的宽，不包含边框，包含padding
element.clientHeight;//元素的高，不包含边框，包含padding
~~~~

#### 元素滚动scroll

~~~~js
//用于获取滚动距离
//不包含边框，包含padding
scrollTop;//元素被卷去的头部
scrollLeft;//元素被卷去的左侧
==>window.pageXOffset;//页面被卷去的左部
==>window.pageYOffset;//页面被卷去的头部
scrollHeight;//实际内容高度,可能超出盒子
scrollWidth;//实际内容宽度
onscroll//滚动事件
~~~~

#### 动画函数封装

~~~~js
//通过定时器不断移动盒子位置
//元素要加定位，有位移
//缓动动画 步长公式（目标-现在的位置）/10;当先位置等于目标时停止
~~~~

##### 立即执行函数

~~~~js
//立即执行函数独立创建了一个作用域
//解决命名冲突问题
(function(/*形参*/) {})(/*可传参*/)
(function() {}())
~~~~

### 完整网页轮播图案例

~~~~js
/*ul布局 
1.大盒子包裹
2.左右按钮
3.切换按钮
4.滚动
5.动画函数
*/
li需要浮动,在一行显示
ul增加宽度，大于父亲，用百分比
父元素overflow:hidden
/*鼠标经过显示隐藏按钮*/
display:none;
display:block
/*小圆圈动态生成*/
getli的个数
for循环生成，加入ol 
/*小圆圈的点击事件，排他思想 */
/*点击小圆圈滚动图片，引入animate动画函数，animate.js写在index.js之上*/
ul需要定位，ul移动不是li移动
移动距离是小圆圈的索引号（设置自定义属性setAttribute）*图片宽度
/*右侧按钮无缝滚动原理*/
在图片的最后复制第一张，滚动到最后的第一张图时，快速跳转到第一张图
cloneNode()
/*点击右侧按钮，小圆圈跟随变化*/
circle
/*自动播放，定时器*/
setInterval(function(){
	//手动调用点击事件
    btn.click();
},2000)
/*鼠标经过，停止定时器*/
clearInterval(timer);
timer=null;
/*节流阀，防止轮播图按钮连续点击播放过快*/
//当上一个函数动画内容执行完毕，再去执行下一个，让事件无法连续触发
回调函数
flag=false锁住
~~~~

### 移动端

~~~~js
//移动端的click事件有300ms的延时，因为要等待判断是否是双击事件
//解决方案

//1.禁用浏览器默认的缩放行为
<meta name='viewport' content='user-scalable=no'>
    
//2.利用touch事件封装
    /*1.手指触摸屏幕，记录触摸时间
     *2.手指离开屏幕，用离开的时间减去触摸时间
     *3.时间小于150ms，且没有位移，就定义为点击
     */
function tap(obj,callback){
    var isMove=false;
    var startTime=0;
    obj.addEventListener('touchstart',function(e){
      	startTime=Date.now();//记录触摸时间
    });
    obj.addEventListener('touchmove',function(e){
      	isMove=true;//是否滑动
    });
    obj.addEventListener('touchend',function(e){
      	if(!isMove&&(Date.now()-startTime)<150){//算点击 
            callback&&callback();
        }
        isMove=false;//取反重置
        startTime =0;
    });
}
//调用
tap(div,function(){})//一次只能解决一个元素的问题，不方便

//3.fastclick插件https://github.com/ftlabs/fastclick
~~~~

### Swiper轮播图插件

~~~~js
/*
https://www.swiper.com.cn/
*/
//1.引入插件相关文件js css
//2.按照规定语法使用 复制 

//superslide
/*
http://www.superslide2.com/
*/
//iscroll
/*
https://https://github.com/cubiq/iscroll
*/
//zy.media.js视频插件
 
/*
1.确认插件实现功能
2.官网查看使用说明
3.下载插件
4.打开demo示例文件，查看需要引入的相关文件引入
5.复制demo示例文件的结构html，样式css以及js代码
*/
~~~~

### 常用框架

~~~~js
bootstrap//js 依赖于Jquery
~~~~

### 本地存储

~~~~js
/*
1.数据存储在用户浏览器中
2.设置、读取方便、甚至页面刷新不丢失数据
3.容量较大，sessionStorage约为5M，localStorage约20M
4.只能存储字符串，可以将对象JSON.stringify()编码后存储
*/

//window.sessionStorage
/*
1.生命周期为关闭浏览器窗口
2.同一窗口页面数据共享
3.以键值对形式存储
*/
sessionStorage.setItem(key,value)
sessionStorage.getItem(key)
sessionStorage.removeItem(key)
sessionStorage.clear()//清除所有数据

//localStorage本地存储
/*
1.生命周期永久生效，除非手动删除
2.多窗口页面共享数据（同一浏览器）
*/
localStorage.setItem(key,value)
localStorage.getItem(key)
localStorage.removeItem(key)
localStorage.clear()//清除所有数据

//本地存储只能存储字符串的数据格式，要存对象需要把数组对象转换为字符串格式
//JSON.stringify()
//获取本地存储的数据 我们需要把里面的字符串转换为对象格式
//JSON.parse()
~~~~









