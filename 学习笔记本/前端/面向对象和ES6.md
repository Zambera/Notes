# 面向对象OOP和ES6

Object Oriented programming

面向对象和面向过程的对比

|      | 面向对象                                                     | 面向过程                                                     |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 优点 | 易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护 | 性能比面向对象高，适合跟硬件联系紧密的东西，例如单片机就采用的面向过程编程 |
| 缺点 | 性能比面向过程低                                             | 没有面向对象易维护、易复用、易扩展                           |

创建对象的三种方式

~~~~js
//1.new Object()
var obj1=new Object()
//字面量
var obj2={}
//构造函数
function Star(uname,age){//构造函数中的属性和方法称为成员
    this.uname=uname;
    this.age=age;
    this.sing=function(){
}
    //实例成员是构造函数内部通过this添加的成员，uname，age，sing
    //实例成员只能通过实例化的对象来访问
    //静态成员是在构造函数本身上添加的成员
    //静态成员只能通过构造函数来访问，而不能通过对象调用
}
var ldh=new Star('cas',45);//首字母大写，new搭配使用
//new执行时
/*
在内存中创建一个新的空对象
让this指向新的对象
执行构造函数里的代码，给新对象添加属性和方法
返回新对象，（构造函数里不需要return
*/
//构造函数存在内存浪费的问题
~~~~

### 构造函数原型prototype

~~~~js
//构造函数通过原型分配的函数是所有的对象共享的
//每一个构造函数都有一个prototype属性指向另一个对象，这个对象的所有属性和方法为构造函数所拥有
Star.prototype.sing=function(){
    //调用ldh.sing()
    //对象原型，自动添加_proto_指向构造函数原型对象
    //_proto_是非标准属性，不可使用
    
    //方法查找规则
    //先查找对象的方法
}


//可以通过原型对象扩展内置对象
//只能通过.追加
Array.prototype.sum=function(){
    var sum=0;
	for(var i=0;i<this.length;i++){
        sum+=this[i];
    }
    return sum;
}


//一般，公共的属性定义到构造函数里，公共的方法我们放到原型对象身上
~~~~

### constructor构造函数

~~~~js
//原型对象和对象的原型都有constructor
//constructor指向构造函数本身
//当给原型对象赋值了一个对象时，原型对象被覆盖，就失去constructor属性
//需要手动利用constructor指回原来的构造函数
Star,prototype={
    constructor:Star,//指回构造函数
    sing:function(){},
    movie:function(){}
}
~~~~

### 继承call

~~~~js
//ES6之前没有extends，通过构造函数+原型对象模拟继承，称为组合继承
//借用父构造函数继承属性

function Father(){
    this.uname=uname;
    this.age=age;
}
function Son(){
    Father.call(this,uname,age);//更改父构造函数this指向
}

//继承父构造函数的方法
//Son.prototype=Father.prototype不可用，修改了子原型对象，父原型对象也会变化
Son.prototype=new Father();//Son的原型对象指向Father实例对象，实例对象有_proto_指向Father原型对象
Father的实例对象覆盖了Son的原型对象，this会指向Father
需要通过constructor修改指向
Son.prototype.constructor=Son;
~~~~

#### call()函数

~~~~js
//call可以改变函数的指向
fun.call()//调用函数
fn.call(o,1,2)//call里面第一个参数是改变函数this指向
~~~~

### ES5的新增方法

~~~~js
//数组方法
//1.迭代（遍历）方法
//forEach()
arr.forEach(function(value,index,array){
    //value每一个数组元素
    //index元素索引号
    //array数组本身
})
//filter()
//filter()方法创建新数组，用于筛选数组
var newArr=arr.filter(function(value,index,array){
    return value>=20;//返回大于20的数组元素的新数组 
})
//some()用于检测数组中是否有满足条件的元素，返回布尔值
var flag=arr.some(function(value,index,array){
    return value>=20;//是否有大于等于20的元素
    //查找到第一个符合条件的值就终止
    return true;//终止遍历
})
//map()、every()

//字符串方法
str.trim()//去除两端空格

//对象方法
Object.keys(obj)//获取对象的属性名数组
Object.defineProperty(obj,prop,descriptor)//定义新属性或修改原有属性
/*
obj目标对象
prop属性
descriptor属性特性以对象的形式书写
value:属性值
writable:可写true，false，默认false
enumerable:是否可枚举遍历，默认false
configurable:是否可以删除，是否可以再修改特性，默认false
*/
obj.defineProperty(obj,"prop",{
	value:1000
})
~~~~

### 函数进阶

~~~~js
//函数的定义和调用

//定义
//1.命名函数function	2.匿名函数	3.构造函数var f=new Function('canshu','canshu','函数体');f();效率较低
//所有的函数都是Function的实例对象，函数也是对象
a instanceof b//a是否属于b 

//调用和this的指向
//1.普通函数fn();	this==>window
//2.对象的方法，obj.fn();		this==>对象
//3.构造函数，newStar();		this==>实例对象
//4.绑定事件的函数btn.click()		this==>btn
//5.定时器调用，定时器自己调用		this==>window
//6.立即执行函数(function(){})(); 不需要调用	this==>window

//改变this的指向
fn.call(thisArg,ar1,ar2)//1.第一个参数函数内this指向的对象，2.调用函数，3.实现继承

fn.apply(thisArg,[argsArray])//同call，参数必须通过数组的方式传递，主要应用，利用apply借助于数学内置对象求最大值
var arr=[1,486,45,5,87];
Math.max.apply(Math,arr);

var f=fn.bind(thisArg,ar1,ar2)//不会调用函数，可以改变this指向，
//返回原函数改变this之后产生的新函数（拷贝
//如果有的函数我们不需要立即调用，但又要改变函数内部this的指向，用bind
//例如，按钮点击后禁用3秒后再启用
var btn=document.querySelector('button');
btn.onclick=function(){
    this.disabled=true;
    //解决方案1，var that=this;下面使用that
    setTimeout(function(){
        //this.disabled=false;//定时器函数中的this指向window。不可直接写
        this.disabled=false;
    }.bind(this),3000)//在定时器函数外绑定bind更改函数内的this指向，可以解决多个按钮的点击事件
}
~~~~

### JS的严格模式

~~~~js
//ie10+,低版本忽略，按正常模式运行
/*
1.消除了js语法中不合理，不严谨之处
2.消除代码运行的一些不安全之处，保证代码运行的安全
3.提高编译器效率，增加运行速度
4.禁用了ECMAScript的未来版本中可能会定义的一些语法，比如一些保留字：class，enum,export,import,super等不能做变量名
*/

//开启严格模式
//严格模式可以应用到整个脚本或者个别函数
//1.为整个脚本开启严格模式
'use strict';//以下的代码按照严格模式执行
(function(){
    'use strict'
})();
//2.为单个函数开启严格模式
function fn(){
    'use strict';
    //仅用于函数内部
}

//严格模式的变化
/*
1.变量规定
变量必须先声明后使用
严禁删除已经声明的变量，delete不可用

2.this的指向问题
普通模式下，普通函数this指向window
严格模式下，全局作用域中函数this指向undefined
普通模式下，构造函数可以不用new直接当普通函数调用，this指向window
严格模式下，构造函数必须用new调用，this指向实例对象
严格模式下，定时器的this指向window，事件、对象this指向调用者

3.函数
函数不能有重名的参数
函数必须声明在顶层，严格模式下，不允许在非函数的代码块内声明函数，if for的{}
*/
~~~~

### 高阶函数

~~~~js
//高阶函数是对其他函数操作的函数，它接受函数作为参数（回调函数）或将参数作为返回值输出（闭包

~~~~

## 闭包

> 闭包（closure）指有权访问另一个函数作用域中变量的函数
>
> ==一个作用域可以访问另外一个函数内部的局部变量

~~~~js
//闭包的主要作用：延伸了变量的作用范围
function fn(){
    var num=10;
    function fun(){
        console.log(num);//产生闭包，fun函数作用域 访问了fn函数内的局部变量
    }
fun();
}

//函数作为返回值产生闭包
function fn(){
    var num=10;
    //function fun(){
    //}
    //return fun;
    return function(){
        
    }
}
var f=fn();//类似于var f=function fun(){}
~~~~

### 递归

> 递归函数：函数内部自己调用自己，这个函数就是递归函数

~~~~js
//递归很容易发生栈溢出(stack overflow)，必须要加退出条件return
//栈溢出 Maximum call stack size exceeded

//经典递归1--阶乘
function fn(n){
    if(n==1)return 1;
	return n*fn(n-1);
}

//经典递归2--斐波那契数列-兔子数列
function fb(n){
    if(n==1||n==2)return 1;
	return fb(n-1)+fb(n-2);
}
~~~~

### 深拷贝和浅拷贝

~~~~js
//浅拷贝只拷贝一层，更深层次对象级别的只拷贝引用，拷贝的是地址，原数据改变，拷贝的数据也会变，相互影响
//深拷贝拷贝多层，每一级别的数据都会拷贝

//for循环浅拷贝
var o={};
for(var k in obj){
    o[k]=obj[k];
}
//ES6新增的浅拷贝
Object.assign(o,obj);//o拷贝后对象，obj要拷贝的对象

//函数递归深拷贝
function deepCopy(newobj,oldobj){
	for(var k in oldobj){
        //获取属性值
        var item=oldobj[k];
        //判断是否是数组
        if(item instanceof Array){//数组也是object，如果对象在上，数组就当对象解析
            newobj[k]=[];
            deepCopy(newobj[k],item);
        }
        //判断是否是对象
        if(oldobj[k] instanceof object){
            newobj[k]={};
            deepCopy(newobj[k],item);
        }else{
        	//简单数据类型
            newobj[k]=item;
        }
    }
}
~~~~

## ES6

> 每年6月发布新的语法规范，ES6泛指2015年之后

#### let&const

~~~~js
var 变量提升，可以先使用后声明

let 声明的变量只在所处的块级有效
不存在变量提升，必须先声明后使用

const 声明的常量具有块级作用域，且必须赋初始值，赋值后不可修改，复杂数据类型不可更改内存地址 
~~~~

#### 解构赋值

~~~~js
let [a,b,c]=[1,2,3]//数组解构，允许按照一一对应的关系从数组中取值
//解构不成功，undefined
let person={name:'zj',age:3};
let{name,age}=person;
//对象解构允许使用变量的名字匹配对象的属性，匹配成功则将对象属性的值赋值给变量
let{name:myName,age:myAge}=person;//给对象属性取别名，属性值赋值给别名变量
~~~~

#### 箭头函数

~~~~js
//如果函数体中只有一句代码，代码的执行结果就是返回值，可以省略大括号
//如果形参只有一个，可以省略小括号
//箭头函数中，this指向箭头函数定义位置的this，箭头函数没有自己的this
对象不能产生作用域
const fn=(canshu)=>{}
箭头函数中没有arguments，接受参数需要按照剩余参数语法
const sum=(...args)=>{
    let total=0;
    args.forEach(item=>{
        total+=item;
    })
    return total;
}
~~~~

#### 剩余参数

> 剩余参数语法允许我们将一个不定数量的参数表示为一个数组

~~~~js
//剩余参数+解构
let students=['zs','zj','zht'];
let [s1,...s2]=students;
~~~~

#### 扩展运算符...

~~~~js

~~~~

#### 字符串扩展

~~~~js
str.includes()//判断字符串中是否包含指定的字串有true，参数1匹配的字串，参数2从第几个开始
str.startWoth()//判断字符串是否以特定的字符串开始
str.endWith()//判断字符串是否以特定的字符串结束
~~~~

#### 模板字符串

~~~~js
//反引号表示模板，模板中可以有格式，通过${表达式}填充数据
`<div>
	<span>${obj.uname}</span>
	<span>${obj.age}</span>
	<span>${obj.gender}</span>
</div>`;
~~~~

#### 函数扩展

~~~~js
/*
1.参数默认值
2.参数解构赋值
3.rest参数
4....扩展运算符
*/

//1.
function foo(param='nihao'){
    //无参则默认
}
//2.
function foo({uname='ls',age=13}={}){
    
}
~~~~

#### set数据结构

~~~~js
const s1=new Set();//set中不存重复值
s1.size//大小属性
s1.add().add();//向s1中添加某个值
s1.delete();//从s1中删除某个值
s1.has();//返回布尔值，判断s1中有没有某个值
s1.clear();//没有返回值，清空set

//遍历set
s1.forEach(value => console.log(value))
~~~~



### 类的声明

~~~~js
class Star{//类名一般大写开头
    //类的共有属性放到constructor内
	contructor(uname,age){
        this.uname=uname;
        this.age=age;
    }//不需要逗号隔开
    sing(song){//类中声明方法不需要function关键字
        console.log(this.uname+song);
    }
}
//创建对象
var ldh=new Star("ldh",18);
~~~~

### 类的继承

~~~~js
class Fatehr{}
class Son extends Father{}
//向父类传递参数
class Fatehr{
    constructor(x,y){
        this.x=x;
        this.y=y;
    }
    sum(){
        console.log(this.x+this.y);//sum方法中的this关键字指向父类
    }
}
class Son extends Father {
	constructor(x,y){
        //super调用父类的函数
        //super必须在子类this之前调用
		super(x,y);//必须使用super关键字将子类得到的参数传递给父类
    }
}
var son=new Son(1,2);
son.sum();

//继承中，子类对象调用一个方法时，子类有该方法就调用子类的，没有就在父类中查找并执行（就近原则） 

//注意！
//1.在ES6中类没有变量提升，必须先定义类，再实例化
//2.类里面共有的属性和方法一定要加this使用
//类里面this的指向问题 constructor里面的this指向实例对象，方法内的this指向的是方法的调用者，可以定义变量存储this
~~~~

tab栏切换

~~~~js
//1.在构造函数中获取元素
//动态添加的元素都需要重新获取，元素改变就需要获取
//2.在init()函数中绑定事件
//ele.insertAdjacentHTML('beforeend',li)可以直接把字符串格式元素追加到父元素,beforeend在父元素的最后


//编辑功能
//禁用双击选中文字
window.getSelection?window.getSelection().removeAllRanges():document.selection.empty();
//双击文字，在里面生成文本框，失去焦点或按下回车把文本框输入的内容给原本的元素
input.select()
~~~~

