# 预编译器less

less是css预处理语言 

~~~~less
@zero:0;
//定义混合
.juzhong(@w:500px,@h:500px,@bg){//设定默认值
	position:absolute;
    left:@zero;
    right:@zero;
    bottom:@zero;
    top:@zero;
    margin:auto;
    width:@w;
    height:@h;
    background:@bg;
}
#wrap{
    .juzhong(@bg);//不传，使用默认宽高
    &>box{
        .juzhong(@w:500px,@h:500px,@bg:pink)
    }
}
~~~~

~~~~less
//less 混合 用法
//结尾一定要加分号
//文件，文件夹不要叫 less
.hideBox(@box,@num,@w,@h,@mr){
    //@box 父容器选择器
    //@num 每行的列数，商品的个数
    //
    /* <div class="box">
        <div class="hideBox">
            <div class="item"></div>
            <div class="item"></div>
            <div class="item"></div>
        </div>
    </div> */
    .@(box){
        width:(@w * @num) + (@num - 1)*@mr;
        border:1px solid #000;
        margin:0 auto;
        overflow:hidden;
        .hideBox{
            width:(@w + @mr) * @num;
            .item{
                width:@w;
                margin-right:@mr;
                height:@h;
                border-bottom:30px;
                float:left;
                background:pink;
            }
        }
    }
}
~~~~

### 变量声明

~~~~less
@base-color:pink;
~~~~

#### 变量选择器

~~~~less
@remind:.alert;
@{remind}{
    height:50px;
    width:80%;
    margin:0 auto;
    background:#ccc;
}
~~~~

#### 变量拼接

~~~~less
@v1:lunbotu;
@v2:container;
@swiper-container:~'.@{v1}-@{v2}';
@{swiper-container}{
    height:100+100px;
    width:80%;
    margin:0 auto;
    background:@base-color;
}
~~~~

#### 变量运算

### 嵌套

~~~~less
.container{
	width:80%;
    height:300px;
    .item{
        width:25%;
        float:left;
    }
}
~~~~

### 媒体查询

~~~~less
header{
    @media (min-width:1200px){
        background:red;
    }
    @media (max-width:1200px) and (min-width:992px){
        background:yellow;
    }
    @media (max-width:992px) and (min-width:768px){
        background:blue;
    }
    @media (max-width:768px){
        background:green;
    }
}
~~~~

#### 混入（函数）

#### 基本混入

~~~~less
.center-show{
	margin:0 auto;
}

{
	.center-show();    
}
~~~~

#### 条件混入

~~~~less
.vip-show() when (@vip=1){
    
}
{
	.vip-show();
}
~~~~

#### 参数混入

~~~~less
.swiper-show(@color){
    background:@color;
}
.swiper-show(greenyellow);
~~~~

##### 标识符要求

~~~~less
/*
字母数字下划线
首字符不为数字
严格区分大小写
不能使用关键字
*/
~~~~

#### 输出带选择器的样式

~~~~less
.body-show(){
    body{
        background:#eee;
    }
}
.body-show();
~~~~

#### 嵌套混入

~~~~less
.mixin-a{
    .mixin-b{
        body{
            background:deepskyblue;
        }
    }
    .mixin-b();
}
.mixin-a();
~~~~

holder.js 图片占位插件

~~~~html
<!-- 1.引入文件 -->
<script src='http://cdn.bootcss.com/holder/2.9.6/holder.min.js'></script>
<!-- 2.img标签下 src 填写特定的路径 显示图片 -->
<img src='holder.js/100px100?text="中间描述文字" alt=''>
100p==100%
100===100px
~~~~





