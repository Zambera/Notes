# CSS3

> 层叠样式表，Cascading Style Sheet

**语法结构**

~~~~html
h1 {
    font-size:12px;
    color:#F00;
}
<!--
选择器 {
	声明1；
	声明2；......
}
-->
~~~~



### 使用方式

**行内样式**

~~~~html
<div style="color:red;"></div>
~~~~



**内联样式**

~~~~html
<head>
    <style type="text/css">
        div {;}
    </style>
</head>
~~~~



**外联样式**

~~~~html
<!--链接式-->
<head>
<link type="text/css" rel="stylesheet" href="mycss.css">
</head>
<!--导入式，不建议使用CSS2.1-->
<style type="text/css">
@improt url("style.css");
</style>
~~~~

### 选择器

#### 简单选择器

**通用选择器（不常用）**

~~~~css
* {
    font-size : 16x;
    padding:0%;
    margin:0%;
}
~~~~

**标签选择器**

~~~~css
p {
    font-size : 16x;
}
~~~~

**类选择器**

~~~~css
p.class {/*交集选择器*/
    font-size : 16x;
}
~~~~

**ID选择器**

~~~~css
#id {
    font-size : 16x;
}
~~~~

**并集选择器（,隔开）**

#### 高级选择器

> 伪元素::
>
> 伪类:

##### 伪元素选择器

~~~~css
::first-line{/*块级首行*/
    color:red;
}
::first-letter{/*块级首字符*/
    color:red;
}
::before{/*文本前插入*/
    content:"";
}
::after{/*文本后插入*/
    content:"";
}
~~~~

**状态伪类选择器**

~~~~css
:enabled{/*启用状态的元素*/}
:disabled{/*禁用状态的元素*/}

input:valid{/*输入合法*/}
input:invalid{/*输入不合法*/}

:requried{/*必填项*/}
:optional{/*非必填项*/}

:checked{/*选择状态的元素*/}
:default{/*默认状态的元素*/}
~~~~



**层次选择器**

E　F后代选择器

~~~~css
body p {/*所有p*/}
~~~~

E＞Ｆ子选择器

~~~~css
body>p{/*子代p，标签，类，id可混用*/}
~~~~

Ｅ＋Ｆ

~~~~css
#id+p {/*相邻兄弟选择器，本身不生效*/}
~~~~

Ｅ～Ｆ

~~~~css
#id~p {/*通用兄弟选择器，本身不生效*/}
~~~~

##### 结构伪类选择器

~~~~css
E F:first-child{}
E F:last-child{}
E F:nth-child(n){/*先找位置*/}
E F:nth-of-type(n){/*先找标签类型*/}
E F:first-of-type{/*类型的第一个元素*/}
E F:last-of-type{/*类型的最后一个元素*/}
F:only-of-type{/*找到父元素中有且仅有一个F的位置*/}
F:only-child{/*只有一个子元素的元素，判断子元素是否为F*/}
~~~~

##### 属性选择器

~~~~css
E[attr]
==> a[id]{/*选中a标签中有id属性的元素*/}
E[attr=""]
==> input[type="text"]{/*属性值等于*/}
E[attr*=""]
==> a[href*="http"]{/*属性值包含*/}
E[attr^=""]/*yi开头*/
E[attr$=""]/*yi结尾*/
~~~~

### 页面美化元素

##### **字体样式和文本样式**

~~~~css
/*常用span标签*/
span {
    font-family:'楷书';
    font-size:24px;2em;/*绝对单位in,cm,mm,pt,pc相对单位em，px，ex,rem,%*/
    font-style:normal;/*italic斜体;oblique倾斜的字体;*/
    font-weight:bold;/*700;100-900;normal400;bolder;lighter*/
    font:normal bold 22px "微软雅黑"/*风格,粗细,大小,类型*/;
}
p {
    color:#FFFFFF;/*RGB;RGBA加透明度(0-1);十六进制;HS%L;HS%L%A(0-1)*/
    word-spacing:normal;/*英文单词间距2px*/
    letter-spacing:normal;/*字符间距4px*/
    text-align:right;/*水平对齐方式left;center;justify两端对齐*/
    vertical-align:middle;/*垂直对齐方式top;bottom;*/
    text-indent:20px;/*首行缩进*/
    line-height:25px;/*文本的行高;normal;数值;%;*/
    text-decoration:underline;/*文本装饰none;overline;line-through*/
    text-transform:none;/*大小写转换uppercase;lowercase;capitalize首字母大写*/
    /*文本阴影*/
    text-shadow:color x-offset(px) y-offset(px) blur-radius(px);
}
~~~~

##### 超链接样式

~~~~css
/*超链接伪类*/
a:link{/*未点击样式*/}
a:visited{/*点击后样式*/}
a:hover {/*鼠标悬停样式*/}
a:active{/*点击未释放*/}

/*光标样式*/
*{	cursor:default;/*默认箭头*/
    cursor:auto;/*默认，浏览器的设置*/
	cursor:pointer;/*小手*/
    cursor:help;/*问号*/
    cursor:crosshair;/*十字架*/
    cursor:wait;/*程序正忙，表或沙漏*/
    cursor:move;/*表示对象可能被移动*/
}
~~~~

##### 列表样式

~~~~css
<li>
list-style-type:none;/*去除效果、circle;square;disc;decimal(数字)*/
list-style-image:url();
list-style-position:outside;/*inside有图片时有效，项目标记放在文本以内*/
list-styel:
</li>
~~~~

##### 背景样式

~~~~css
background-color:#FFFFFF;/*transparent透明*/
background-image:url();/*背景图片*/
background-repeat:repeat;/*no-repeat;repeat-x;repeat-y*/
background-position:center;/*xpx ypx;x% y%;left center right top bottom*/
background-size:auto;/*cover完全填充容器截断;percentage相对元素百分比;contain保持宽高比适应容器*/
background:#c00 url() 205px 20px/*定位xy*/ no-repeat;
~~~~

##### 渐变效果

~~~~css
background:linear-gradient(position,color1,color2,..);/*线性渐变*/
/*
position:to top/bottom/right/left;to top left/right;to bottom left/right/-180deg~180deg
*/
radial-gradient(shape size position,start-color,...,last-color)/*径向渐变*/
/*
shape:circle;ellipse默认椭圆;
size停止位置:closest-side最近边;farthest-side;closest-corner最近角;farthest-cornor;
position起点位置:默认正中心,%
*/
/*颜色不均匀分配，在颜色后加百分比*/
/*ie:-ms-;chrome,safari:-webkit-;opera:-o-;firefox:-moz-*/
/*重复*/
repeating-linear-gradient()
repeating-radial-gradient()
~~~~

### 盒子模型

> CSS思维模型，内容，填充(内边距)，边框，空白边(外边距)

**元素尺寸**

~~~~css
/*百分比，父元素的比例*/
width:auto;/*固定尺寸*/
height:auto;/*高由内容决定，宽是父元素的最大值，默认*/

/*应对元素尺寸变大变小的问题，父元素或页面大小改变时，最大值和最小值会限制宽高*/
min-width:;
min-height:;
max-width:;
max-height:;
~~~~

**边框、边距**

> 网页居中对齐：margin:0px auto;	/*块元素，固定宽度*/

~~~~css
border-color:;
border-width:;thin,thick,medium
border-style:;
border:1px solid #3a6587;
/*solid实心线，double双实线，dashed短横线，dotted点线*/
margin:3px 5px 7px;/*同内边距padding*/
/*一个值4边，两个值上下，左右，三个值上、左右、下，四个值上右下左*/
~~~~

~~~~css
box-sizing:content-box;/*默认值，盒子的总尺度，border-box盒子的宽高等于元素内容宽高，inherit继承父元素盒子模型*/
~~~~

**元素可见性**

~~~~css
visibility:visible;/*默认，hidden元素不可见但占空间，collapse不可见，隐藏表格的行与列，不是表格则同hidden*/
~~~~

**边框圆角**

~~~~css
border-radius:20px 10px 50px 30px;/*顺序为左上右上右下左下*/
/*
圆形：宽高相同，圆角半径为宽度的一半，50%
半圆：宽高的比例为2:1
扇形：三同一不同，宽高圆角半径相同，圆角取值位置不同
*/
~~~~

**盒子阴影**

~~~~css
box-shadow:inset x-offset y-offset blur-radius color;
/*
inset：内阴影，默认外阴影，可不填
偏移量，模糊半径，颜色
*/
~~~~

### 浮动

> 行内元素宽高固定

~~~~css
display:block;/*块级默认;inline行内默认;inline-block行内块;none元素不显示*/
float:left;
/*

*/
~~~~

### 四种父级边框塌陷的清除浮动的方式

~~~~css
clear:both;/*left;right，
清除浮动对其它元素的影响none默认允许浮动元素出现在两侧*/
/*
1.浮动元素后加空div清除浮动设置高度
2.设置父容器高度
3.父级添加overflow属性
visible默认内容会在盒子外呈现
hidden内容被修剪，其余不可见
scroll内容被修剪，浏览器显示滚动条
auto如果内容被修剪，浏览器显示滚动条
*/
/*4.父级添加伪类after*/
<div id="father" class="clear"></div>
.clear:after{
    content:"";
    display:block;
    clear:both;
}
~~~~

### 定位

~~~~css
position:static;/*默认，*/
position:relative;/*相对定位，与绝对定位配合使用*/
position:absolute;/*绝对定位，下拉列表，左右导航栏*/
position:fixed;/*固定定位*/

z-index:3/*用于绝对定位层，默认是0；数值越大排越上*/
~~~~

#### z-index不生效

~~~~css
/*
发生的条件：
1.父标签position属性为relative;
2.问题标签无position属性（不包括static）
3.问题标签含有浮动属性（float）
*/
/*
解决问题的办法（其一即可）：
1.position:relative改为absolute;
2.浮动元素添加position属性（relative,absolute）
3.清除浮动
*/
~~~~

##### **网页元素透明度**

~~~~css
opacity:x;/*值为0~1，值越小越透明*/
filter:alpha(opacity=x);/*IE,值为0~100，值越小越透明*/
~~~~

Flex

~~~~css
display:flex;
/*
flex-direction 	  - - -  控制项目排列方向
row左到右，row-reverse右到左，
column上到下，column-reverse下到上
flex-wrap        	  - - -  控制项目是否换行及如何换行
nowrap默认不换行，wrap换行，wrap-reverse反向换行
flex-flow 	  - - -  属性1 , 2 的简写方式
flex-flow:flex-direction flex-wrap
justify-content	  - - -  定义了项目在轴线上的对齐方式
flex-start起始对齐
flex-end尾端对齐
center居中对齐
space-between分散对齐
space-around两侧间隔相等
space-evenly兼容性差，间隔相等
align-items	  - - -  定义项目在交叉轴上如何对齐
flex-start交叉轴的起始位置
flex-end交叉轴终点位置
center交叉轴中间对齐
stretch未设置高度或auto 无效占满
baseline项目第一行文字对齐
align-content	  - - -  定义了多根轴线的对齐方式
*/

/*
flex项目属性
order		- - -  定义该项目的排列属性排列顺序
默认0，可为负
flex-grow  	- - -  定义项目的放大比例
flex-shrink        	- - -  定义项目的缩小比例
flex-basis	- - -  定义项目在分配多余空间之前占据的主轴空间
flex		- - -  前三个属性的简写模式
align-self      	- - -  项目单独设置的垂直对齐方式

*/

/*
宽高自适应，可设置不溢出
对齐方便
排列方便
align-self
*/
~~~~

### 动画

#### 变形动画

~~~~css
transform:
translate():/*平移函数*/
scale()/*缩放函数*/
rotate()/*旋转函数，取值度数*/
skew()/*倾斜函数，取值度数*/
~~~~

#### 过渡动画

~~~~css
transition:property duration timing-fuction delay;
/*transition: 要过渡的属性  花费时间  运动曲线  何时开始;*/
/*如果有多组属性，我们用逗号隔开
transition: width 1s ease 0s, height 1s ease 0s, background-color 1s ease 0s;*/
transition:width 1s , height 1s linear 1s, background-color 1s;
/*
支持过渡的样式属性，颜色的属性，取值为数值，transform，渐变，visibility， 阴影
transition-poperty:上面的css属性/all
transition-duration:过渡时长/s/ms
transition-timing-function:
          1.ease 默认值，慢-->快-->慢  慢速开始，快速变快，慢速结束
          2.linear 匀速
          3.ease-in 慢--->快  慢速开始,快速结束
          4.ease-out 快速开始，慢速结束
          5.ease-in-out 慢速开始，先加速再减速，慢速结束
transition-delay:   s/ms
过渡属性的编写位置
    1.将过渡放在元素声明的样式中（元素自己的样式里）过渡效果有去有回。
    2.将过渡放在元素的触发操作中(hover),过渡效果有去无回。
过渡的简写：
     transition:property duration timing-function delay;
*/
~~~~

media

#### 网页动画

~~~~css
/*
动画的实现步骤：
    1.声明动画及动画关键帧
      @keyframes  动画名称{
           //定义关键帧
           0%{ 动画开始的样式 }
            ........
           100%{动画结束时的样式}
        }
    2.调用动画
        animation-name:动画名称；
        animation-duration:动画播放一个周期的时间；
    3.动画的其他属性
        animation-delay
    4.动画的速度时间曲线函数
        animation-timing-function
        ease/linear/ease-in/ease-out/ease-in-out
    5.animation-iteration-count
         指定动画的播放次数
          取值，具体的数字/infinite无限次
    6.animation-direction:
          动画的播放方向
          取值  normal       正常            0%-100% 
              reverse     逆向播放    100%-0%
              alternate   轮流播放/ 奇数次正向播放/偶数次逆向播放
    7.简写方式：
          animation:name duration timing-function delay iteration-count direction;
    8.animation-fill-mode
          指定动画播放前后的显示状态
               1.none  默认值
               2.forwards 动画完成后，保持在最后一个关键帧上
               3.backwards(需要有delay)动画开始之前，保持在第一个关键帧上
               4.both,同时设置forwards和backwards
动画的兼容性：
               如果要兼容低版本的浏览器，需要在声明动画的时候加前缀
               @keyframes 动画名称{}
               @-webkit-keyframes
               @-moz-keyframes
               @-o-keyframes
*/
~~~~

