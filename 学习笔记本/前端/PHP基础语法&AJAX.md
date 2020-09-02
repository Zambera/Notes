# php基础语法&AJAX

### 基础语法

~~~~php
<?php
//执行结果有中文，必须在php文件顶部设置
    header('content-type:text/html;charset=utf-8');
//返回XML文件
	header('content-type:text/xml;charset=utf-8');
//单行注释
/*多行注释*/

//定义变量
$num=10;//数字字母下划线，不宜数字开头

//打印
echo $num;

//定义数组
$arr=array(1,2,3);
//echo不能打印集合数组字典
print_r($arr);
//取出数组中的内容
echo $arr[2];
//换行
echo '<br>';

//定义字典
$dict = array("name"=>"zl","age"=>"48");
echo $dict['name'];

//分支
$age=18;
if($age>=18){
  echo '成年人';
}else{
  echo '未成年';
};
//三目
$res=($age>=18)? '成年人':'未成年';

//switch
switch($age){
  case 0:echo '0';break;
  case 18:echo '成年';break;
  default:echo 'sd';break;
}

//for
$arr=array(1,23,4);
for($i=0;$i<count($arr);$i++){
  echo $arr[$i];
}

//while
$index=0;
while($index<count($arr)){
  echo $arr[$index];

}
?>
~~~~

### get post请求的异同

~~~~php
/*
相同点
都将数据提交到远程服务器
不同点
GET将数据放到URL后面
POST将数据放到请求头中
GET提交数据有大小限制
POST提交数据没有大小限制

GET用于提交非敏感数据和小数据
POST用于提交敏感数据和大数据
*/
~~~~

### php文件上传

~~~~php+HTML
<!--
method='post' 
enctype='multipart/form-data'
-->
<form action='test.php' method='post' enctype='multipart/form-data'>
</form>
<?php
//获取上传文件对应字典
$fileInfo=$_FILES['upFile'];
//获取上传文件的名称
$fileName=$fileInfo['name'];
//获取上传文件保存的===临时路径
$filePath=$fileInfo['tmp_name'];
//保存上传的文件
move_uploaded_file($filePath,destination:'./source/'.$filePath);
?>


<?php
//web服务器对上传文件的大小有限制
//上传 大文件 需要修改web服务器配置 php.ini
file_uploads = On;//是否允许上传文件On/Off 默认On
upload_max_filesize =2048M;//上传文件的最大限制
post_max_size=2048M;//通过Post提交的最多数据

max_execution_time=30000;//脚本最长的执行时间，单位秒
max_input_time=30000;//接受提交数据的时间限制，秒
memory_limit=2048M;//最大的内存消耗
?>
~~~~

## AJAX

> AJAX是在**不重新加载**整个网页的情况下与服务器**交换数据**并**更新**部分网页的技术

~~~~js
//1.创建异步对象
var xmlhttp = new XMLHttpRequest();
//2.设置请求方式和请求地址
/*
method:请求的类型GET POST
url:文件在服务器上的位置
async:true异步,false同步,true
*/
xmlhttp.open('GET', './ajax.php', true);

/*POST*/
xmlhttp.open('POST','./ajax.php',true);
xmlhttp.setRequestHeader('Content-type','application/x-www-form-urlencoded');/*open==>send*/
xmlhttp.send('username=zs&userpassword=123456');

//3.发送请求
xmlhttp.send();
//4.监听状态的变化
xmlhttp.onreadystatechange = function(e) {
    /*
    readyStatus
    0:请求未初始化
    1:服务器连接已建立
    2:请求已接收
    3:请求处理中
    4:请求已完成，且相应已就绪
    */

    //5.处理返回的结果
    if (xmlhttp.readyState === 4) {//请求完成
        //判断请求是否成功
        if (xmlhttp.status >= 200 && xmlhttp.status < 300 || xmlhttp.status === 304) {
            console.log('接受到服务器返回的数据');
        } else {
            console.log('没有接受到服务器返回的数据');
        }
    }

}
~~~~

### AJAX在IE中的两个问题

~~~~js
//IE5&IE6使用ActiveXObject
var xmlhttp;
if(window.XMLHttpRequest){
	xmlhttp=new XMLHttpRequest();//主流
}else{
	xmlhttp=new ActiveXObject();//ie56
}

//AJAX在IE中的缓存问题
/*
在ie浏览器中，如果通过Ajax发送GET请求，那么IE浏览器认为
同一个URL只有一个结果
不能实时拿到运行的结果
需要每次访问的地址不同==>时间戳，随机数
*/
xhr.open('get','ajax.txt?t='+ +new Date(),true)

~~~~

### jQuery的AJAX

~~~~js
$.ajax({
    type:'GET',
    url:'./test.php',
    data:'name=zj&pwd=123456',
    success:function(){
        
    },
    error:function(){
        
    }
});
~~~~

### XML数据格式

~~~~xml
<?xml version='1.0' encoding='UTF-8' ?>
<doc>
    <name>zhangsan</name>
    <age>18</age>
</doc>
~~~~

~~~~php
<?php
header("content-type:text/xml;charset=utf-8");
echo file_get_contents("info.xml");
~~~~

### JSON数据格式

~~~~json
//JSON是JS对象的字符串表示法
{
    'name':'zhangsan',
 	'age':'18',
 	'sex':'女'
}
//js对象转JSON
JSON.stringify(jsobj);
//JSON转js对象
JSON.parse(jsonobj);
//ie8及以下，不可以使用原生JSON.parse()
json2.js框架
~~~~

~~~~php
<?php
echo file_get_contents("info.json");
eval('('+str+')');//将非标准的JSON转化为标准的JSON
~~~~

### Cookie

~~~~js
//cookie是一种会话跟踪技术（客户端
//session也是会话跟踪技术（服务端
//cookie 将网页中的数据保存到浏览器中
/*
默认不会保存任何数据
生命周期：默认浏览器关闭，=>一次会话
可以设置默认过期时间，过期立即删除，否则浏览器关闭也存在
document.cookie='key=value;expires='

cookie保存多条数据，只能分条设置
cookie有大小和个数的限制（20-50）最好不要超过20条，4kb
cookie作用范围：默认，同一浏览器同一路径(文件夹)，默认下一级路径（子文件夹）可以访问

*/
document.cookie
document.cookie='key=value;'
//过期时间
var date= new Date();
date.setDate(date.getDate()+1);//明天
document.cookie='key=value;expires='+date.toGMTString()+';'
//访问路径
document.cookie='key=value;path=/;';//将cookie保存到根路径
//访问域名
document.cookie='key=value;domain=xxx.com';//让二级域名可以访问cookie
~~~~

### hash

~~~~js
window.location.hash=xx;
//==>xxx.html/#xx
window.location.hash;
~~~~



