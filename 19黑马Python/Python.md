# Python学习笔记

## 1.1 Python基本语法

**标识符**

> 标识符由**字母，下划线和数字**组成，且数字**不**能开头，不推荐保留字，区分大小写

**变量**

|变量类型|
| --------------- |
| Number(数字)：int(有符号整型，非常大),long,float,complex(复数) |
| 布尔类型：true，false |
| String(字符串)   |
| List(列表)  []  混合类型 |
| Tuple(元组)  () |
| Dictionary(字典)  键值对 |

~~~~python
type()		#查看变量类型
2 << 2		#移位运算，2^3=8
n = int(s)	#强转

~~~~

**命名规则**

> 1. 见名知意
> 2. 大小驼峰
> 3. 下划线连接，单词小写

**关键字**

~~~~python
#打印当前版本Python的关键字
import keyword
keyword.kwlist
'''
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
'''
~~~~

**注释**

~~~~python
# 这是一句单行注释
~~~~

~~~~python
'''
这里是多行注释
可以写多行内容
'''
~~~~

**格式符号**

| 格式符号 | 转换 | 格式符号 | 转换 |
| ------ | ---- | ------ | -------- |
| %c       | 字符 |%x|十六进制整数小写|
| %s       | 通过str()字符串格式化 |%X|十六进制整数大写|
| %i       | /有符号十进制整数 |%e|索引符号e|
| %d       | 有符号十进制整数 |%E|索引符号E|
| %u       | 无符号十进制整数 |%g||
| %o | 八进制整数 |%G||
| %f（%.2f） | 浮点实数(两位小数) |||


### python_print

~~~~python
print("直接打印输出")
print("我今年%d岁" % age)		#占位符输出
print("%s今年%d岁" % (name,age))	#多占位符输出，类型要对应
print("设置结束符",end='...')
print("设置结束符",end='\n')		#默认
print "字符串为", s		#逗号输出，保留空格
~~~~

### python_input

~~~~python
s = input("这里写提示信息：")	#将输入赋值给s,返回字符串类型
s = raw_input("这里写提示信息：")	#python2
~~~~

