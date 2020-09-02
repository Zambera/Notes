# Bootstrap

> 不适用于设计稿，仿站

### 全局CSS样式

- 标题
  + h1-h6 .h1-.h6
  + 副标题 `<small>` `.small`
  + 字体大小 `14px` 行高 `1.248` 应用到 body
  + `<p>` 1/2行高，10px的底部外边距
  + `.lead` 突出显示 `<mark>` 
  + `<del><ins><u>` 
  + 文本的对齐
    * `.text-left` `.text-right` `.text-center`
    * `text-lowercase` `text-uppercase` `text-capitalize`
    * 缩略语 `<abbr title='attribute'>content</attr>`
  + 地址
    ```
    <address>
        <strong>dsada</strong><br>
        xx市xx区<br>
        xx街，xxx号<br>
        <abbr title='Phone'>P:4468 461</abbr>
    </address>
    ```
  + 列表
    
    * `.list-unstyled` 无样式的列表 `ul` 

### 栅格系统

- `.container` 
- 分为 `12` 列，需要 container 承载
- 不同屏幕的前缀
  + 手机 `.col-xs-`
  + 平板 `.col-sm-`
  + 小显示屏 `.col-md-`
  + 大显示屏 `.col-lg-`
- 偏移 `.col-md-offset-2`
- 排序 `col-md-push-3` `col-md-pull-3`

### code 代码

- 内联样式
```
<!-- code-->
    For example <code>&lt;section&gt;</code> as inline;
    <kbd>cmd</kbd>
```
- 代码块
  + `pre` 标签包裹
- 变量 
  + `var` 标签包裹
- 输出   
  + `samp` 标签包裹

### 表格

- 基本表格
  + `<table class='table'>` 
- 斑马线表格
  + `<table class='table-striped'>` 
- 边框表格
  + `<table class='table-bordered'>` 
- 鼠标悬停表格
  + `<table class='table-hover'>` 
- 紧凑型表格
  + `<table class='table-condensed'>` 
- 表格状态类 
  + `active` `success` `info` `warning` `danger` 
- 响应式表格
  + `table-responsive` 加在div

### 表单

- 基本表单格式
  + `<form role='form'>`
  + `div.form-group` <label><input>
  + `input.form-control`
- 内联表单
  + `<form role='form' class='form-inline'>`
  + 隐藏label `<label class='sr-only'>`
- 水平排列的表单
  + `<form role='form' class='form-horizontal'>`
- 支持的控件
 + 文本框 `<input type='text' class='form-control'>`
 + 文本域 `<textarea class='form-control' rows='5'></textarea>`
 + 复选框 `.checkbox>label>input[type='checkbox']` 
 + 单选框 `.radio>label>input[type='radio']` name相同
 + 下拉列表 `select.form-control>option*` multiple
- 静态控件
  + `p.form-control-static`
- 状态
  + 焦点状态  
    * `input`
  + 禁用状态
    * disabled
    * `fieldset disabled`
  + 只读状态
    * readonly
  + 校验状态
    * `.has-success` 
    * `.has-warning` 
    * `.has-error`
- 控件尺寸
- 辅助文本

### 起步

~~~~js
/*
1.使用h5声明
2.移动设备优先
*/
~~~~

#### 容器

~~~~js
/*
为页面内容和栅格系统包裹 .container 容器
.container
.container-fluid 宽度百分百
两者不可嵌套
*/
~~~~

#### 栅格系统

~~~~js
/*
.container|.container-fluid>.row>col
row有-15px的左右外边距
分为十二列
行中只能有列元素
.col-xs-n
.col-sm-n
.col-md-n  可叠加
.col-lg-n  可嵌套
-offset-n  可偏移   通过 margin 实现
如果没有设置当前屏幕分辨率的列偏移，根据已有的列偏移生效
清除浮动
.col-md-push-*  列排序  通过定位实现（相对
.col-md-pull-*	
向上兼容  如果设置的分辨率词缀小于当前分辨率 排序生效，反之不可
<div class='clearfix visible-lg-block'></div>
==>clearfix:清除两侧浮动
//控制显示隐藏 / 响应式工具类
==>visible-lg-block :仅在大屏显示  其他屏下，div消失，清除浮动还原
*/
/*
栅格系统自定义
@grid-columns 12 ...
*/
.row左右外边距为-15px抵消col-,对齐元素
~~~~

#### 排版

~~~~js
/*
.h1-.h6
.lead	段落突出显示
<mark>	标记
<del> <s>	删除线
<ins> <u>	下划线
.small <small>	小
<strong> b
<em>	i斜体

code 高亮显示代码
kbd  高亮显示按键内容
pre  原样输出内容

对齐
.text-left
.text-center
.text-right
.text-justify	两端对齐
.text-wrap	不换行
.text-lowercase
.text-uppercase
.text-capitalize
<abbr title='attribute'> attr </attr>
<address></address>		地址

<blockquote>
<footer>	----前缀
	<cite></cite>	斜体
</footer>
</blockquote>

reverse
*/
~~~~

#### 表格

~~~~js
table.table		
table-striped		隔行换色
table-bordered		边框
table-hover		悬浮换色
table-condensed		紧凑型
table-responsive		响应式表格，滚动条
~~~~

#### 按钮

~~~~js
//颜色
btn-default		默认 白
btn-primary		首选 蓝
btn-success		成功 绿
btn-warning		警告 黄
btn-danger		错误 红
btn-info		提醒 蓝

//尺寸
btn-lg
btn-md
btn-sm
btn-xs
~~~~

#### 图片

~~~~js
//========>img-responsive	响应式显示
img-circle		圆形显示
img-rounded		圆角显示
img-thumbnail	缩略图形式显示
~~~~

#### 辅助类

~~~~js
//文字颜色
text-primary
text-info
...
//背景颜色
bg-primary
bg-info
...
//浮动
pull-left		左浮
pull-right		右浮
center-block	中	
clearfix	清除浮动
~~~~

#### 响应式类

~~~~js
visible-* :lg,md,sm,xs
hidden-*
    
~~~~



### 组件

~~~~html
//字体图标
<span class='gclass'></span>
//下拉菜单
.dropdown|position:relative		up上拉菜单
//按钮组
<!--.btn-group  <.btn-toolbar	分页按钮-->
.btn-group.btn-group-justified两端对齐按钮组 占全行
按钮下/上拉菜单 | 分裂式按钮下拉菜单
//输入框组
//标签页
//禁用 disabled
//导航条
//路径导航 
//分页  active激活态
标签label label-primary
//徽章  badge 未读消息==
//巨幕 .jumbotron
//警告框alert alert-primary
//进度条 progress>progress-bar[-success ] progress-bar-striped条纹 active(文件上传)
//媒体对象media  (评论回复，在线聊天室)
//列表组list-group[-item]  list-group-item-success
//面板.panel.penal-default>penal-heading|body|footer>penal-title
~~~~

#### 插件

~~~~js
模态框
下拉菜单

滚动监听 scrollspy.js 
在滚动的包裹元素夹
1.position:relative
2.data-spy='scroll' data-target='#导航ul包裹元素div的id'
3.添加锚点id

工具提示 tooltip
弹出框
警告框
手风琴
轮播图
~~~~

