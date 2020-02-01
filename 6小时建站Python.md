# 6小时建站Python

## Python 基本语法

### 1.1 方括号用法

~~~~python
course = "Python for Beginners"
print(course[-1])
#===>	s
print(course[:])
#===>	Python for Beginnners
print(course[0:])
#===>	Python for Beginnners
print(course[:6])
#===>	Python	[0,6)
print(course[1:-1])
#===>	ython for Beginner
print(course[-1:1])
#===>	空串

# 可截取字符串进行赋值
copy = course[:6]
~~~~

### 1.2 格式化输出与占位符

~~~~python
first = 'Amber'
last = 'Chow'
msg = f'{first} [{last}] is a coder'
print(msg)
# f ==> format
# {} ==> 占位符
#===>	Amber [Chow] is a coder
~~~~

### 1.3 String Method

~~~~python
course = 'Python for Beginners'
print(len(course))
#===>	20
# 输出字符串的长度
print(course.upper())
#===>	PYTHON FOR BEGINNERS
# 全部大写输出字符串
print(course.lower())
#===>	python for beginners
# 全部小写输出字符串
print(course.title())
#===>	Python For Beginners
# 首字母大写输出字符串
print(course.find("on"))
#===>	4
# 输出目标字符串在原字符串中第一个字符的索引值，未找到返回-1
print(course.replace('Beginners','absolute Beginners'))
#===>	Python for absolute Beginners
print(course)
#===>	Python for Beginners
# 调用方法输出时不会改变原字符串，而是创建了新的
is_exist = 'python' in course
print(is_exist)
#===>	False
# 字符串中有返回True，无返回False，大小写敏感
~~~~

1.4 Arithmetic Operations

~~~~python
print(10 + 3)	# 13
print(10 - 3)	# 7
print(10 * 3)	# 30
print(10 / 3)	# 3.333333
print(10 // 3)	# 3 整除
print(10 % 3)	# 1 取余
print(10 ** 3)	#1000 幂运算
# x = x + 3		==>		x += 3
~~~~

