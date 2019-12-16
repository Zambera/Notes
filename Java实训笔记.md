# Java实训笔记

## 1.1 javabean(MVC)

#### 数据Bean(pojo)

- 表单Bean(收集表单数据)

  1. 包声明

  2. 类声明

  3. 属性声明（private）

  4. Getter和Setter方法（public）

  5. 无参构造方法

     > 将.java文件放在放在WEB-INF\classes
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
	2.创建zs（setAttribute()）实例化对象
	3.将zs交给page内置对象管理（getAttribute()）
*/
<jsp:useBean id="zs" scope="page" class="cn.zte.pxb.SimpleBean"/>
~~~~

#### setProperty--表单自动收集

~~~~jsp
/*
	1.在page内置对象中寻找属性名为zs的对象
	zs.setPassword(request.getParameter("password"));
	名字，个数和类型必须一致
*/
<jsp:setProperty name="zs" property="*"/>
~~~~



  
