# python的安装与使用

1. 如何安装 www.python.org
2. 如何使用python 命令行启动python编译器
窗口键 win
win+r cmd 
color f0/f1/f2... 一次性调整cmd颜色背景
输入python
exit() 退出
.py

# python的输出

life is short I use python 人生苦短我用python
根据代码量

使python输出如下格式内容
**********
   hello
**********

python中如何获取函数的帮助信息
换行功能实际上是print函数自带的
+ 拼接

# python 输入

复变量

input()函数实现输入

python2 输入 使用 raw_input()/input()

# if判断

if 条件：
    子语句（子语句一定要有缩进，默认4个空格，条件成立执行）
else:
    子语句（当条件不成立时执行）
```
== 等于（判断是否相等）
条件语句中的几个特殊语句
and 并且（两个条件必须同时成立） 
or  或者（两个条件只需要满足其中一个条件）
not 条件取反
短路
> 大于 < 小于 != 不等于 >= <=
```

多分支判断
elif

int(num) 转换类型

# 变量

变量 = 赋值
一次赋值 多次使用
变量名称定义：
1. 不能以数字开头
2. 变量名称中不能有特殊符号（_下划线除外）
3. 变量名称区分大小写
4. 关键字不能作为变量名称使用
keyword kwlist 可以查看关键字
5. 内建函数不要作为变量名称使用
查看python官方手册
下载自带 C:\Users\Diversifolious\AppData\Local\Programs\Python\Python36\Doc

# 字符串赋值

字符串中所包含的索引值
str = "python"
astr[0:1]  # 变量[脚标的起始位置：脚标的结束位置]显示结束位置之前的内容才会被显示
astr[-3]

# 常见的赋值类型

列表 list
列表的特点：[] 在中括号中可以写入不同类型的数据，每个值之间用,分割，支持脚标取值

元组的特点：() 取值方式基本和列表相同

字典：{} 字典没有索引值，靠键值对来取值 {"key":"value"}

# 赋值类型的属性

数字

字符串

元组

列表

字典

# 循环语句

random 随机数
random.randint(1,100)

while 条件：
    子语句
只要条件满足循环就会执行

循环语句中两个子语句
break; 立即退出循环 
continue;  当该语句被执行时会结束当前循环，继续下一次循环
+= *=

for 循环

根据变量赋值的次数进行循环

for i in items:
    子语句

range()

# 文件对象

python读取和写入文件内容
.open
.close

打开文件
写入文件内容
保存文件

eg:
f = open("c:\\users\\diversifolious\\testone.txt","wb")
f = writelines([b"one\r\n",b"two\r\n",b"three\r\n"])
f = close()
b:读取按2进制读

实现文件内容的复制
读出文件内容，写入到另一文件中

通过文件对象cmd.exe对命令行工具进行复制
避免文件读取量大，可设置一次读取量 data = sf.read(4096)
通过while循环进行配合

# 模块和函数

将常用代码储存方便调用
1. 定义模块名称不能以数字开头
2. 不能和默认的模块重名
"""
介绍模块的作用
里面包含的功能
作者的联系方式等
"""

# 函数的形参和实参

try:
    被捕获的子语句
except (异常类型，类型2,...)
    pass/处理

# 面向对象编程

面向过程(顺序)

OOP object oriented programming

类 对象

类的命名规则 驼峰式命名法PrintStar

属性 方法

