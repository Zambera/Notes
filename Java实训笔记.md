# Java实训笔记

## 1.1  Javabean(MVC)

#### 数据Bean(pojo)

- 表单Bean(收集表单数据)

  1. 包声明

  2. 类声明

  3. 属性声明（private）

  4. Getter和Setter方法（public）

  5. 无参构造方法

     > 将.java文件放在放在WEB-INF\classes目录的目录结构下
     >
     > javac -b xxxx.java

- 结果Bean

#### 逻辑Bean

- 业务Bean
- 持久Bean

~~~~jsp
<%@page contentType="text/html;charset=utf-8" %>          //静态编码
~~~~

```java
public class SimpleBean{
	private String name ;
	private String password ;	 
	public SimpleBean(){
		System.out.println("** public SimpleBean() .") ;
	}
	public void setName(String name){
		this.name = name ;
	}
	public void setPassword(String password){
		this.password = password ;
	}
	public String getName(){
		return this.name ;
	}
	public String getPassword(){
		return this.password ;
	}
}
```


### JavaBean的优点

- 便于开发与维护，降低了耦合性

- 代码的复用性

- 分布式应用

### Jsp页面标签

#### useBean

~~~~jsp
/*
	1.判断page内置对象是否有属性名为zs的属性值
	2.new Bean()创建值为zs的SimpleBean对象（setAttribute()）
	3.将zs交给page内置对象管理（getAttribute()）
*/
<jsp:useBean id="zs" scope="page" class="cn.zte.pxb.SimpleBean"/>
~~~~

#### setProperty--表单自动收集

~~~~jsp
/*
	1.在page(scope)内置对象中寻找属性名为zs的对象
	2.给zs中的所有属性设值（同名收集）
	zs.setPassword(request.getParameter("password"));
	名字，个数和类型必须一致
*/
<jsp:setProperty name="zs" property="*"/>
<jsp:getProperty name="name" property="name"/>	//获取
//===>   ${zs.name}		el表达式
//表单提交空数据时，request数据为空串，而不是null
//标签不会把空串和null收集到对象
~~~~

### 内置对象作用域范围

#### page

~~~~jsp
<jsp:useBean id="zs" scope="page" class="cn.zte.pxb.SimpleBean"/>
~~~~

> 只在一个页面有效，页面跳转即销毁，存放临时数据
>
> 不能用来传Bean

#### request

~~~~jsp
<jsp:useBean id="zs" scope="request" class="cn.zte.pxb.SimpleBean"/>
~~~~

> 最常见的，服务端跳转(安全)，请求结束即销毁
>
> 客户端跳转不能传request

#### session

~~~~jsp
<jsp:useBean id="zs" scope="session" class="cn.zte.pxb.SimpleBean"/>
~~~~

> 用户下线（浏览器关闭）销毁，只应存放认证信息

#### application

~~~~jsp
<jsp:useBean id="zs" scope="application" class="cn.zte.pxb.SimpleBean"/>
~~~~

> tomcat启动时创建

##   1.2 Servlet

> 概念：由Java编写的，线程安全(不允许改变对象的值)的Web组件(由tomcat调用的)

> 作用：1.CGI：通用网关接口(注入和依赖查找)  ==>  从Web容器中取得数据(内置对象)的能力
>
> ​		   2.创建表单Bean，封装表单参数
>
> ​		   3.分析请求，分发给业务层
>
> ​		   4.根据业务层的转向信息，转到视图组件

### Servlet

1. HTTP request	