# Java实训笔记

## 1.1  Javabean(MVC)

#### 数据Bean(pojo)

- 表单Bean(收集表单数据)

  1. 包声明
2. 类声明
  3. 属性声明（private）
4. Getter和Setter方法（public）
  5. 无参构造方法

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
### 部署

将.java文件放在放在WEB-INF\classes目录的目录结构下

~~~~bash
javac -d xxxx.java
~~~~


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

> 概念：由Java编写的，线程安全(不允许改变对象的值)的**Web组件**(由tomcat调用的)

> 作用：1.CGI：通用网关接口(注入和依赖查找)  ==>  从Web容器中取得数据(内置对象)的能力
>
> ​		   2.创建表单Bean，封装表单参数
>
> ​		   3.分析请求，分发给业务层
>
> ​		   4.根据业务层的转向信息，转到视图组件

### Servlet流程

>![Servlet](C:\Users\ZhouJunTing\Desktop\Notes\img\servlet.png)

1. 启动Web服务器

2. 接受用户请求（HTTP:TCP表单）tcp建立信道

3. tomcat创建request、response

4. 把请求通过page给Servlet，调用doPost()

5. 分析交给业务组件

6. 把表单Bean传给持久层

7. sql查询数据库，创建结果Bean并封装，返回给业务层放到request

8. 向控制层返回转向信息，转到视图层

9. 视图组件通过EL表达式从request拿到数据

10. 进行渲染，response返回到浏览器进行显示	

### Servlet语法

~~~~java
import java.io.* ;			//IOException
import javax.servlet.* ;	 // ServletException
import javax.servlet.http.* ;// HttpServletRequest、HttpServletResponse、HttpServlet

public class SimpleServlet extends HttpServlet{
    //Servlet创建就执行init方法,优先执行有参init
    public void init(ServletConfig config) throws ServletException{}
	// 表示处理get请求
	public void doGet(HttpServletRequest req,HttpServletResponse resp) throws IOException,ServletException{}  //throws声明不处理异常
	public void doPost(HttpServletRequest req,HttpServletResponse resp) throws IOException,ServletException{}
    public void destroy(){}
} 
~~~~

### Servlet配置（必须）

> 只要是web.xml文件修改，则必须**重新启动服务器**。

~~~~xml
<servlet>
// 在web.xml文件内部起作用的名字 
	<servlet-name>simple</servlet-name> 
// Servlet程序所在的包.类名称 
	<servlet-class>cn.mldn.lxh.servlet.SimpleServlet</servlet-class>
    <load-on-startup>0</load-on-startup>  //tomcat启动时创建servlet对象，优先级最高为0
</servlet>
// Servlet映射地址
//不接收用户请求时，不需要配置servlet-mapping
<servlet-mapping> 
// 在web.xml文件内部起作用的名字，此名字与上面的一致 
	<servlet-name>simple</servlet-name> 
// 具体的映射路径，前面必须有一个/ 
	<url-pattern>/demo</url-pattern> 
</servlet-mapping>
~~~~

> JDK提供的是JAVA SE包，而JAVA EE包不在JAVA SE之中，需要单独配置包
>
> 把J2EE的servlet.jar包(tomcat\common\lib)放到jdk\jre\lib\ext

### Servlet生存周期

![Servlet的生存周期](C:\Users\ZhouJunTing\Desktop\Notes\img\life.png)

### Servlet初始化参数的获取

1. 

~~~~java

~~~~

### 表单访问Servlet

~~~~html
<form action="/*映射名*/" method="post">	//<url-pattern>
~~~~

~~~~xml
<form action="xxxxx.do" method="post">
<url-pattern>*.do</url-pattern>
~~~~

## 1.3 EL表达式

