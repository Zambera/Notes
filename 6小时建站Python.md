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

### 1.4 Arithmetic Operations

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

1.5 **Operator Precedence(运算符优先级)**

~~~~python
# parenthesis ()
# exponentiation 2 ** 3
# multiplication or division
# addition or subtraction
~~~~

1.6 **Math Functions(数学函数)**

~~~~python
x = 2.9
print(round(x))		# 四舍五入 3
print(abs(-2.9))	# 求绝对值 2.9
~~~~

~~~~python
# 导入数学模块
import math
~~~~

> **google**:*python 3 math module*

1.7 **If Statements**

~~~~python
is_hot = True
is_cold = False

if is_hot:
    print("It's a hot day")
    print("Drink plenty of water")
elif is_cold:
    print("It's a cold day")
    print("Wear warm clothes")
else:
    print("It's a lovely day")
print("Enjoy your day")
# It's a hot day
# Drink plenty of water
# Enjoy your day
~~~~

1.8 **Logical Operators**

~~~~python
has_high_income = True
has_good_credit = True
has_criminal_record = False
# and 与 :
if has_good_credit and has_high_income:
    print("Eligible for loan")
# or 或 :
if has_good_credit and has_high_income:
    print("Eligible for loan")
# not 非 :
if has_good_credit and not has_crinimal_record:
    print("Eligible for loan")
~~~~

1.9 **Comparison Operators**

~~~~python
temperature = 30
# > < == !=
if temperature > 30:
    print("It's a hot day")
else:
    print("It's not a hot day")
~~~~

**while loops**

~~~~python
i = 1
while i <= 5:
    print('*' * i)
    i += 1
print("done")
# *
# **
# ***
# ****
# *****
# done
# 简单猜数字练习
# while + else; break后不执行else的内容
secret_number = 9
guess_count = 1
guess_limit = 3
while guess_count < guess_limit:
    guess = int(input("Guess: "))
    guess_count += 1
    if guess == secret_number:
        print("You win! ")
        break
else:
    print("Sorry, you failed! ")
~~~~

