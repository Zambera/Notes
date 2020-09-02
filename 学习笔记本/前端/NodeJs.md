#  Node.js

> Node.js是由ECMAScript及Node环境提供的一些附加API组成的，包括文件、网络、路径等等一些更强大的API


- Node.js® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://v8.dev/).
  - 构建于chromev8浏览器引擎之上 

  - Node.js不是一门语言
  - Node.js不是库、不是框架
  - Node.js是一个JavaScript运行时环境
  - 简单来讲，Node.js可以解析和执行JavaScript代码
  - 让JavaScript脱离浏览器运行
  - 在Node中为JavaScript提供了一些服务器级别的操作API
    - 文件的读写
    - 网络服务的构建
    - 网络通信
    - Http服务器等等。。。
- Node.js uses an event-driven,non-blocking I/O model that makes it lightweight and efficient.
  - event-driven 事件驱动
  - non-blocking I/O model 非阻塞I/O模型（异步）
  - 轻量、高效
- Node.js package ecosystem,npm is the largest ecosystem of open source libraries in the world.
  - npm是世界上最大的开源库生态系统
  - 绝大多数的JavaScript相关的包都存放在npm上，方便开发人员下载使用
  - npm install jquery 
**JS开发弊端**

~~~~js
//文件依赖
//命名冲突
~~~~

Node.js中的模块化开发规范

> Node.js规定一个Javascript文件就是一个模块，模块内部定义的变量和函数默认情况下在外部无法得到
>
> 模块内部可以使用exports对象进行成员导出，使用require方法导入模块

~~~~js
//a.js
let version=1.0;
const sayHi=name=>`$name`;
//导出1
exports.version=version;//exports相当于module.exports,两者通常指向同一个地址，指向不同对象时以module.exports为准
exports.sayHi=sayHi;//导出即 将变量和函数作为exports对象的属性和方法

//b.js
let a=require('./a.js');//require的返回值是a.js的exports对象,.js可以省略
a.sayHi();//调用
~~~~

### node.js一些资源

- 《深入浅出Node.js》朴灵，偏理论
- 《Node.js权威指南》API讲解
- Javascript 标准参考教程 http://javascript.ruanyifeng.com
- Node入门 http://nodebeginner.org/index-zh-cn.html
- 官方API文档 https://nodejs.org/dist/latest-v6.x/docs/api/
- CNODE社区 http://cnodejs.org
- CNODE新手入门 http://cnodejs.org/getstart

1. 

### 系统模块

#### 文件操作fs file system

~~~~js
const fs=require('fs');
//读取文件内容
//通过回调函数返回文件内容，读取硬盘数据需要时间
//相对于命令工具的工作目录。大多数使用绝对目录
//使用__dirname获取当前文件所在的绝对路径
fs.readFile(path.join(__dirname,'文件名'))//导入path
fs.readFile('文件路径/文件名称'[,'文件编码'],callback);//错误优先的回调
fs.readFile('./hello.js','utf8',(err,doc)=>{
    console.log(err);
    console.log(doc);
})
//写入文件内容
fs.writeFile('文件路径/文件名称','数据',callback);//文件不存在则自动创建
const content='<h3>正在使用fs.writeFile写入文件内容</h3>';
fs.writeFile('./index.html',content,err=>{
    if(err!=null){
		console.log(err);
        return;
    }
    console.log('文件写入成功');
})
~~~~

#### 路径操作path

~~~~js
//不同操作系统路径分隔符不同一Windows/\Linux/
//路径拼接
path.join('lujing','lujing',...)
const path=require('path');
const finalPath=path.join('public','uploads','avater');---public/uploads/avater根据操作系统斜杠

~~~~

#### http

~~~~js
//引入模块
const http = require('http')
//创建web服务器
const app = http.createServer();
//监听请求事件
app.on('request',(req，res)=>{
    res.end('dsa')
    req.headers //请求报文 ['key']
    req.url //请求地址
    req.method //获取请求方法
    
    res.write(400,{
        'content-type':'text/plain;charset=utf8'//text/html,
    })
    //http状态码 200成功 404 500服务器错误 400客户端请求有语法错误 
})
//监听端口
app.listen(3000)
~~~~



### 第三方模块（包）

~~~~js
//1.以js文件形式存在，提供实现项目具体功能的API接口
//2.以命令行工具形式存在，辅助项目开发
//获取第三方模块
npmjs.com第三方模块的存储和分发仓库
npm node package manager

//下载
npm install 模块名称//默认下载到当前命令行工作目录，自动创建目录
//卸载
npm uninstall 模块名称//自动删除空目录

//本地安装和全局安装
//一般 命令行工具进行全局安装 库文件进行本地安装
~~~~

#### nodemon

~~~~js
//辅助项目开发的第三方模块，命令行工具
//监控文件的保存操作，重新执行文件

//安装nodemon
npm install nodemon -g//全局安装
//使用
//用nodemon替换node
ctrl+c终止
~~~~

#### nrm

~~~~js
//命令行工具 npm registry manager npm下载地址切换工具
npm install nrm -g//下载安装
nrm ls//查询可用的下载地址列表
nrm use 下载地址名称//切换  taobao

~~~~

#### gulp

~~~~js
//基于node平台开发的前端构建工具
//1.项目上线，html,css,js文件压缩合并
//2.语法转换（es6、less
//3.公共文件抽离
//4.修改文件浏览器自动刷新
1.npm install gulp
2.在项目根目录下建立gulpfile.js文件
3.重构项目的文件夹结构src目录放置源代码文件dist目录放置构建后文件
4.在gulpfile.js文件中编写任务
5.在命令行工具中执行gulp任务

//项目源代码放到src文件夹
gulp.src();//获取任务要处理的文件
gulp.dest();//输出文件
gulp.task();//建立gulp任务.pipe()
gulp.watch();//监控文件变化

//引用gulp
const gulp=require('gulp');
//任务名称，回调函数
gulp.task('first',()=>{
    //1.使用gulp.src获取要处理的文件
    gulp.src('./demo.js');//取得要处理的文件
    .pipe(gulp.dest('dist/js'));
})

//执行任务
npm install gulp-cli -g//命令行工具
gulp 任务名

//gulp插件
/*
1.gulp-htmlmin:html文件压缩
2.gulp-csso:css压缩
3.gulp-babel:JavaScript语法转化
4.gulp-less:less语法转化
5.gulp-uglify:压缩混淆JavaScript
6.gulp-file-include:公共文件包含
7.browsersync:浏览器实时同步
*/
1.下载插件
2.引用插件require
3.调用插件

//构建任务
gulp.task('default',['renwu1','renwu2','renwu3'])//执行default可省略，只写gulp
~~~~

package.json文件

> 项目描述文件，记录当前项目信息，如项目名称，版本，作者，github地址，依赖的第三方模块 num init -y

~~~~json
//package.json
{
    "name":"description",
    "version":"1.0.0",
    "description":"",
    "main":"index.js",
    "script":{
        //别名npm run 别名
        "test":"echo \"Error: no test specified\" && exit 1"
    },
    "keywords":[],
    "author":"",
    "license":"ISC",
    "dependenceies":{
        //依赖的第三方模块
        --production//开发依赖
    }
    "devDependenceies":{
    --save-dev//安装时，开发依赖
}
}
//package-lock.json锁定包的版本，加速下载，记录下载地址，不需要再分析依赖
~~~~

## CMD 常用指令

- dir 列出文件列表
- cd 进入文件夹
- md 创建文件夹
- rd 删除文件夹
- d: 进入D盘

## 环境变量 Windows系统中的变量
- 更改环境变量需要重启命令行窗口

- path 
  + 在命令行窗口打开一个文件，或调用程序时
  + 首先在当前目录下寻找文件程序，找到则直接打开
  + 没有则在环境变量 path 路径中寻找， 找不到则报错

- 沿着原型链找变量，没有会报错

## 进程和线程

- 进程负责为程序的运行提供必备的环境
- 进程相当于工厂中的车间

- 线程是计算机中的最小的计算单位，线程负责执行进程中的程序
- 相当于工厂中的工人

单线程 js是单线程
多线程

# Node.js

~~~~

- Nodejs是一个能够在服务器端运行的 JavaScript 的开放源代码的 跨平台的JavaScript运行环境
- Node采用Google开发的V8引擎运行 js 代码，使用事件驱动
- Node 奇数版为开发版
- 模块化 在node中一个 js 文件就是一个模块
  + 通过 require() 函数引入外部的模块
  + 参数为文件路径，相对路径必须以.或..开头
  + 使用 require 引入模块，返回一个对象，代表的是引入的模块
  + 在 node 中，变量独立在模块内部
  + 向外部暴露属性或方法，通过给 exports 对象添加属性和方法

- global 
  + node 中有一个全局变量 global 类似于 window
    * 全局创建的变量和函数会作为 global 的属性和方法
  + arguments.callme 保存的是当前执行的函数对象
  + 在 node 执行的时候 会在代码顶部添加
    * function (exports,require,module,_filename,_dirname)
    * }底部
  + exports == module.exports
  + require 函数 用来引入模块
  + _filename 是当前模块的完整路径
  + _dirname 当前模块所在路径

- module 和 module.exports
  + 简单数据类型在栈
  + 复杂数据类型在堆内存，对象在堆内存
  + 对象名存储的是地址，对象赋值给另一对象，两者指向的是同一对象
  + 不能给 exports 直接赋值一个对象
~~~~
## CommonJS 包结构

-  `package.json`  描述文件 必需
  + 包描述文件用于表达非代码相关的信息
  + 位于包的根目录下
-  bin  可执行二进制文件
-  lib js代码
-  doc 功能说明文档
-  test 单元测试

## npm Node Package Manager

- npm 命令
  + npm -v 查看npm版本
  + npm version 查看包版本
  + npm 帮助
  + npm search packagename 搜索包
  + npm install packagename / npm i
    * --save 安装的同时设为依赖
    * -g 全局安装包 ，一般是工具包
    * 不上传 node_modules
  + npm install 自动安装项目所依赖的包
  + npm remove packagename / npm r
  + npm init 创建 packsge.json
- 淘宝 npm 镜像 只读
  + npm install -g cnpm --registry=http://registry.npm.taobao.org
  + npm install 包名 -registry=地址  从镜像源安装
  + npm config set registry 地址  设置镜像源
- 通过 npm 下载的包都在 node_modules,直接通过包名引入
  + node 在使用模块名字引入模块时，首先在当前目录node_modules中寻找是否含有该模块，没有则向上查找，直到磁盘根目录

## buffer -file system

- buffer 的结构和数组相似，操作方法也和数组类似
- 存储二进制文件
  + var buf = Buffer.from(str) 将一个字符串保存到buffer
  + buf.length 占用内存大小
  + str.length 字符串长度
  + buffer 所有的构造函数都是不推荐使用
  + buffer 确定，大小不可更改，是直接操作底层内存
  + var buff = Buffer.alloc(10) 创建指定大小的 buffer
  + buff[0] = 88
  + buff[1] = 0xaa
  + buff.toString() 将缓冲区数据转化为字符串

## fs 文件系统

- 通过 node 操作系统的文件
- var fs = require('fs') 引入模块
- 所有操作都有 同步和异步
  + 同步会 阻塞 异步不会
- 写入文件步骤
  + 同步文件写入
    * var fd = fs.openSync('路径',w r操作类型) 返回值位数字3成功
    * fs.writeSync('文件描述符','str内容',position,encoding)  `写入`
    * fs.close('fd') `关闭`
  + 异步文件写入
    * fs.open('hello.txt','w',function(err,fd){})
    * 异步方法没有返回值，通过回调函数 arguments 返回
    * fs.writeFile('路径','内容',function(){}) 不需要 open close
    * 默认从头写
    * fs.writeFile('路径','内容', {flag:'a'},function(){})
  + 流式文件写入
    * 同步、异步、简单文件写入都不适合大文件的写入，性能较差，容易内存溢出
    * 创建一个可写流 var ws = fs.createWriteStream(path[,option])
    * ws.write('内容') * 99
    * 监听流的打开关闭 open close 用 once 绑定事件
    * 关闭流用 end 不用 close
- 文件读取
  + 简单文件读取,返回 buffer
    * fs.readFile(path[,option],function(err,data){})
    * fs.readFileSync(path[,option])  
  + 流式文件读取
    * 是用于读取大文件，可以分多次将文件读取到内存
    * 创建一个可读流
    * var rs = fs.createReadStream('lujing.xxx')
    * rs.once('open',function () {})
    * rs.once('close',function () {})
    * 如果要读取一个可读流中的数据，必须为可读流绑定data事件，data事件绑定完毕，会自动开始读取数据
    * rs.pipe(ws) 将可读流中的内容直接输出到可写流

## fs 模块的其他方法

- fs.existsSync(path) 查看路径是否存在 返回布尔值
- fs.stat(path,callback) 获取文件的状态 返回一个保存状态信息的对象
  + 第一个参数是 错误对象
  + isFile() 是否是文件
  + isDirectory() 是否是文件夹
  + size 文件大小
- fs.unlink(path,callback) 删除文件
- fs.readdir(path[,option],callback) 读取一个目录的目录结构
  + fs.read 
- fs.rename(oldPath,newPath,callback) 文件路径重命名，移动文件
- fs.rmdir()
- fs.watchFile(filename[,option],listener) 监视文件的修改