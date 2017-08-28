# Python 中的异常及处理
>   **异常**：异常即是一个事件，该事件会在程序执行过程中发生，影响了程序的正常执行。一般情况下，在Python无法正常处理程序时就会发生一个异常。
异常是Python对象，表示一个错误。
当Python脚本发生异常时我们需要捕获处理它，否则程序会终止执行。
### 常见标准异常
| 异常名称 | 描述 |
| :------: | :------: |
|BaseException|所有异常的基类|
|SystemExit|解释器请求退出|
|KeyboardInterrupt|用户中断执行（通常是输入^C）|
|Exception|常规错误的基类|
|StopIteration|迭代器没有更多的值|
|GeneratorExit|生成器（generator）发生异常来通知退出|
|StandardError|所有的內建标准异常的基类|
|ArithmeticError|所有数值计算错误的基类|
|FloatingPointError|浮点计算错误|
|OverflowError|数值运算超出最大限制|
|ZeroDivisionError|除（或取模）零（所有数据类型）|
|AssertionError|断言语句失败|
|AttributeError|对象没有这个属性|
|EOFError|没有內建输入，到达EOF标记|
|EnvironmentError|操作系统错误的基类|
|IOError|输入/输出操作失败|
|OSError|操作系统错误|
|WindowsError|系统调用失败|
|ImportError|导入模块/对象失败|
|LookupError|无效数据查询的基类|
|IndexError|序列中没有此索引（index）|
|KeyError|映射中没有这个键|
|MemoryError|内存溢出错误|
|NameError|未声明/初始化对象（没有属性）|
|UnboundLocalError|访问未初始化|
|ReferenceError|弱引用（weak reference）试图访问已经垃圾回收了的对象|
|RuntimeError|一般的运行时错误|
|NotImplementedError|尚未实现的方法|
|SyntaxError|Python语法错误|
|IndentationError|缩进错误|
|TabError|Tab和空格混用|
|SystemError|一般的解释器系统错误|
|TypeError|对类型无效的操作|
|ValueError|传入无效的参数|
|UnicodeError|Unicode相关的错误|
|UnicodeDecodeError|Unicode解码时错误|
|UnicodeEncodeError|Unicode编码时错误|
|UnicodeTranslateError|Unicode转换时错误|
|Warning|警告的基类|
|DeprecationWarning|关于被弃用的特征的警告|
|FutureWarning|关于构造将来语义会有改变的警告|
|OverflowWarning|旧的关于自动提升为长整形（long）的警告|
|PendingDeprecationWarning|关于特性将会被废弃的警告|
|RuntimeWarning|可疑的运行时行为（runtime behavior）的警告|
|SyntaxWarning|可疑的语法的警告|
|UserWarning|用户代码生成的警告|

### 异常处理
捕获异常可以使用 `try/except` 语句
`try/except` 语句用来检测`try`语句块中的错误，从而让`except`语句捕获异常信息并处理
如果不想在异常发生时结束程序，只需在`try`里捕获它

语法：
```Python
try:
<语句>			#运行别的代码
except <名字>:
<语句>			#如果在try部分引发了'name'异常
except <名字>,<数据>:
<语句>			#如果引发了'name'异常，获得附加的数据
else:
<语句>			#如果没有异常发生
```
try的工作原理:当开始一个try语句后，Python就在当前程序的上下文中作标记，这样当异常出现时就可以回到这里，try子句先执行，接下来会发生什么依赖于执行时是否出现异常。

* 如果当try后的语句执行时发生异常，Python就跳回到try并执行第一个匹配该异常的except子句，异常处理完毕，控制流就通过整个try语句（除非在处理异常时又引发新的异常）

* 如果在try后的语句里发生了异常，却没有匹配的except子句，异常将被递交到上层的try，或者到程序的最上层（这样将结束程序，并打印缺省的出错信息）

* 如果在try子句执行时无异常发生，Python将执行else语句后的语句（如果有else语句），然后控制流通过整个try语句

##### 实例1：打开一个文件，在该文件中的内容写入内容，且未发生异常
```Python
#!/usr/bin/python
#-*- coding: UTF-8 -*-

try:
	fh =  open("testfile","w")
	fh.write("这是一个测试文件，用于测试异常！")
except IOError:
	print ("Error: 没有找到文件或读取到文件失败！")
else:
	print ("内容写入文件成功！")
	fh.close()

```
### 使用except而不带任何异常类型
```Python
try:
	正常的操作
	......
except:
	发生异常，执行这块代码
else:
	如果没有异常执行这块代码
# 此种方式try-except语句捕获所有发生的异常。	
```
### 使用except而带有多种异常类型
```Python
try:
	正常的操作
	......
except(Exception1[,Exception2[,...ExceptionN]]]):
	发生以上多个异常中的一个，执行这块代码
else:
	如果没有异常执行这块代码
```
### try-finally语句
try-finally语句无论是否发生异常都将执行最后的代码

```Python
try:
	<语句>
finally:
	<语句>			#退出try时总会执行
raise
```
### 异常的参数
一个异常可以带上参数，可作为输出的异常信息参数
```Python
try:
	正常操作
except ExceptionType,Argument:
	可以在这输出Argument的值
```
##### 实例
```Python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

def temp_convert(var):
	try:
		return int(var)
	except ValueError,Argument:
		print ("参数没有包含数字\n",Argument)
temp_convert("xyz")
```

### 用户自定义异常
通过创建一个新的异常类，程序可以命名它们自己的异常。异常应该是典型的继承自Exception类，通过直接或间接的方式。
##### 实例
```Python
class NetworkError(RuntimeError):
	def __init__(self,arg):
		self.args = arg
try:
	raise NetworkError("bad hostname")
except NetworkError,e:
	print e.args
	
```
##### 实例
```Python
#!/usr/bin/python
# -*- coding: UTF-8 -*-
try:
	1/0
except Exception as e:
	'''异常的父类，可以捕获所有的异常'''
	print ("0不能被除")
else:
	''' 保护不抛出异常的代码'''
	print ("没有异常")
finally:
	print("最后总是要执行")
```
