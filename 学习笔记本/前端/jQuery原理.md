# jQuery原理

~~~~js
/*
1.jQuery的本质是立即执行函数
2.在函数中定义的变量外界访问不到，可以防止变量污染
3.window.jQuery=window.$=jQuery,让外界访问内部变量，把变量赋值给window
4.传参window，便于后期压缩代码，提升查找效率
5.传参undefined，IE9以下的浏览器undefined可以被修改，为了保证内部的undefined不被修改，需要接收一个正确的undefined
*/
(function(window, undefined) {
    var njQuery = function() {
        return new njQuery.prototype.init();
    }
    njQuery.prototype = {
        constructor: njQuery,
    }
    njQuery.prototype.init.prototype = njQuery.prototype;
    window.njQuery = window.$ = njQuery;
})(window)
~~~~

### jQuery入口函数传值测试

~~~~js
//传'',null,undefined,NaN,0,false
==>返回一个空的jQuery对象
//传入字符串
//1.代码片段
==>返回存储DOM元素的jQuery对象
//2.选择器
==>返回存储找到元素的jQuery对象
//传入数组（真/伪）
==>将数组中存储的元素依次存储带jQuery对象中返回
//传入对象
==>返回存储对象的jQuery对象
//传入DOM元素
==>返回存储DOM元素的jQuery对象
//传入基本数据类型
==>把传入数据存储到jQuery对象中返回
~~~~

