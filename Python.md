 # `Python` #
 ***
 ***2022.11.05***
 ***
 **运算符**方面大体与 `C` 相同
 有所不同的是"`/`" 表示浮点数除法而"`//`"表示整数除法
 "`**`"可以表示乘方
 <br>比如
 ```python
 3 / 2 = 1.5     #此处是float
 3 // 2 = 1      #此处是int
 2 ** 3 = 8      #2的3次方
 ```
 小技巧：不同于c语言，Python在两个变量交换内容的时候不需要“第三者”
 ```python
 a = 2
 b = 3
 [a,b]=[b,a]
 print(a,b)
 
 #输出：
 3 2
 ```

 **数学库**
 ```python
 #使用前要引用math "import math"
 import math
 math.e
 math.pi
 math.log(x[base])
 math.pow(x,y)
 math.sqrt(x)
 math.fabs(x)
 math.round(x[,n])
 math.divmod(x,y)
```
Tips
```python
print(":.2f".format(y))  
#保留两位小数的样例
```
**`if` 语句**用法基本同C: if ,else if ,else
```python
if condiction :
    #code
elif condiction :
else :
    #code
```
**`for in` 语句**
```python
for variable in [] :
    #code

#举例：
for i in [1,2,3,4] :
    print(i,end=',')

#输出：
1,2,3,4,
```
**`range`函数**<br>
`range函数可以生成连续的数字`
```python
range(start,stop,step) 
#从start（默认为0）开始至stop结束（不包括stop）
#step默认为1

#举例：
print(list(range(9)))
print(list(range(0,9)))
print(list(range(0,9,2)))

#输出：
[0,1,2,3,4,5,6,7,8]
[0,1,2,3,4,5,6,7,8]
[0,2,4,6,8]
```
**`sum`函数** : 求和<br>
eg：
```python
print(sum(range(0,9)))

#输出：
36
```
**列表**<br>
`
列表是python 最常用数据类型之一;
由零个或多个元素组成，元素之问用逗号分开，整个列表被方括号所包裹;
元素类型可以相同也可以不同;
通过序号可以引用列表中的元素;支持加法、乘法、比较、索引、切片等操作`<br>

**列表推导式**
```python
a = [expression for item in iterable]

#举例
num = sum([number for number in range(1,6)])

#输出
30
```
***
2022.11.06
***
**切片**
```python
#举例
s1 = [1,2,3,4,5,6]
print(s1[0:2])
print(s1[0:])
print(s1[:2])
#输出
[1,2]
[1,2,3,4,5,6]
[1,2]
```
Tips
```python
a,b,c = input().split() #使用“split“函数实现在同一行输入
```
```python
print("请输入: %d"%var) 
#实现在一个“print”函数中输出文字及变量
```
今日学习中遇到的问题<br>
1. `if 语句中条件结束后有“:”`<br>
2. `class 是一个不合法的变量名（Class)`
***
**`len`函数**
```python
#使用len函数求长度
s1 = 'This is a Python Programm'
print(len(s1))

#输出
25
```

***
***2022.11.07***
***
小技巧<br>
`在字符串中需要单引号时，可以用双引号来表达字符串`<br>
`同样，需要双引号可以用单引号表达` <br>
`也可以用转义字符 \ 来表示`
***
"r"<br>
`“r”可以防止字符转义`
```python
#举例
s1 = r'This\nis a Python Programm'

#输出
This\nis a Python Programm
```
**`lower`函数**<br>
`lower函数可以将字符串中的大写字母都变成小写`
```python
#举例
s1 = 'Stephen Curry'
print(s1)
s2 = s1.lower()
print(s2)

#输出
Stephen Curry
stephen curry
```
***
***！！！注意 ！！！***<br>
**`函数并不会改变字符串本身，只会对于已有的字符串进行运算从而得出一个新的字符串`**
***
**`find`函数**<br>
`find函数可以用于查找子字符串在字符串中所在的位置`
```python
#举例
s1 = 'Stephen Curry'
print(s1)
s2 = s1.find('Cu')
print(s2)
s3 = s1.find('e',4)
#在存在多个子字符时“,”后可表示从字符串第几位查找
print(s3)

#输出
Stephen Curry
8
5

#相比于“ ‘Cu’ in s1 ”仅能知道是否存在 find函数可以查找更多信息
```
`replace`函数
`replace函数可以用于替换字符串中的字符`
```python
#举例
s1 = 'Stephen Curry'
print(s1)
s2 = s1.replace(' ','-')
print(s2)
s3 = s1.replace(' ','')
print(s3)
print(s1) #验证s1是否被 replace函数所改变

#输出
Stephen Curry
Stephen-Curry
StephenCurry
Stephen Curry #可见 s1 并未被改变
```
***
***2022.11.08***
***
`list`函数
`list函数可以将（）内转化为列表`
```python
#举例
s1 = 'Stephen-Curry'
print(list(s1))

#输出
['S', 't', 'e', 'p', 'h', 'e', 'n', '-', 'C', 'u', 'r', 'r', 'y']
```
列表变量与其他变量的不同<br>
```python
#普通变量
a1 = 1
a2 = a1
print(a1,a2)
a1 = 2
print(a1,a2)
#输出
1 1
2 1

#列表变量
l1 = [1,2,3]
l2 =l1
print(l1,l2)
l1[0] = 2
print(l1,l2)
#输出
[1, 2, 3] [1, 2, 3]
[2, 2, 3] [2, 2, 3]
```
***
***2022.11.10***
***
**列表的函数**
```python
l1 = [1,2,3]
l1.append(4) #在列表后方插入一元素
print(l1)
l1.extend([4,5,6]) #将括号内列表连接
print(l1)
l1.insert(1,1.5) #在“1”前插入“1.5”
print(l1)
l1.remove(1.5) #移除掉括号内的元素
print(l1)
print(l1.pop()) #可以删除指定位置的元素
print(l1)
l1.pop(0)
print(l1)
l1.reverse() #可以颠倒列表中元素的顺序
print(l1)
print(l1.index(5)) #可以查找括号内元素在列表中的位置
l2 = [2,14,3,5,3,5,12]
l2.sort() #有大到小排序
print(l2)


#输出
[1, 2, 3, 4]
[1, 2, 3, 4, 4, 5, 6]
[1, 1.5, 2, 3, 4, 4, 5, 6]
[1, 2, 3, 4, 4, 5, 6]
6
[1, 2, 3, 4, 4, 5]
[2, 3, 4, 4]
[5, 4, 4, 3, 2]
0
[2, 3, 3, 5, 5, 12, 14]
```
**字符串与列表**
```python
s1 = 'hello world'
print(s1.split()) #以空格为断点将字符串变为列表
print(list(s1)) #与split 不同将每一个字符作为一个元素
s2 = 'Stephen-Curry'
print(s2.split())
print(s2.split('-')) #split括号内作为断点
l1 = s2.split('-')
print(' '.join(l1)) #使用引号里内容将列表中每一元素连接起来

#输出
['hello', 'world']
['h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd']
['Stephen-Curry']
['Stephen', 'Curry']
Stephen Curry
```
**元组**<br>
元组本身和列表差不太多，在表达方面元组的定义是`t = (1,2,3)`但要注意元组本身不可修改！！！列表是可以修改的，关于列表的函数，只要不是对元组有修改的函数均可以使用 <br>
元组的作用：有些时候，我们希望有一组数据，但我们又不希望，拿到这组数据的人去修改它，这时候我们可以采用元组 tuple
```python
#元组的转换：tuple函数
s1 = [1,2,3]
t = tuple(s1)
print(s1,t)

#输出
[1,2,3] (1,2,3)
```
在Python中即使不定义元组在有逗号的情况下也会默认为元组
```python
a = 1,2,3
print(type(a))

#输出
<class 'tuple'>
```
**随机库**
```python
import random #引入随机库
t = [1,3,5,34,6,32]
t.sort() #回顾一下排序
print(t)
random.shuffle(t) #随机打乱
print(t)
random.shuffle(t) #第二次打乱
print(t)
print(random.choice(t)) #随机从t中选出一元素
print(random.random()) #随机生成一个0～1之间的浮点数
print(random.randint(1,100)) #随机生成一个1~100之间的整形数

#输出
[1, 3, 5, 6, 32, 34]
[3, 6, 1, 32, 5, 34] #不一定
[1, 3, 5, 32, 6, 34]
5
0.36219124115058743
73
```
`if` 语句 用法基本同C: if ,else if ,else
```python
if condiction :
    #code
elif condiction :
else :
    #code
    #code
#if 语句是可以写多行的，当缩进不同时if语句结束
#所以，有一个良好的缩进习惯非常重要
```


**`while`语句**
```python
while True:
    if condition :
        #code
    else :
        #code 
        break

#建议初学者都写成这种类型，使用一个无穷循环，需要的时候break就好
#建议不要上来就写while，先考虑一种情况，最后在考虑while
```
**`for in` 语句**
```python
for variable in [] :
    #code
    if condition:
        #code
        break
else :
    #如果程序正常结束，就会执行else语句
```
**`try-except` 语句**<br>
如果你要写一个程序，这个程序在执行过程中可能会出现错误，这个时候你可能需要用`if`语句去限定输入值的范围，但是Python提供了一个`try-except `语句，它会先去尝试执行这个语句，如果出现问题那么执行except。<br>
其实就是不用写条件的`if-else`
```python
#语法格式
try :
    #code
except 异常类型1 :
    #code
except 异常类型2 :
    #code
...
except 异常类型N :
    #code
except :
    #code
else :      #如果本次运行没有问题那么运行else，同 while-else
    #code
finally :       #无论是否有异常，都要执行的
    #code
```
```python
#举例
x = int(input())
l = [1,2,3,]
try:
    print(l[x])
except:
    print("There is no l[%d]" %x)
else :
    print("Successful")
finally :
    print("This is Finally")

#结果
9
There is no l[9]
This is Finally
2
3
Successful
This is Finally
```
Python常见异常
---
异常|描述
---|---
SystemExit|解释器请求退出
FloatingPointError|浮点计算错误
OverflowError|数值运算超出最大限制
ZeroDivisionError|除（或取模)零（所有数据类型）
Keyboardinterrupt|用户中断执行(通常是输入^C)
ImportError|导入模块/对象失败
IndexError|序列中没有此索引(index)
RuntimeError|一般的运行时错误
AttributeError|对象没有这个属性
IOError|输入/输出操作失败
OSError|操作系统错误
KeyError|映射中没有这个键
TypeError|对类型无效的操作
ValueError|传入无效的参数
---
`map`函数
可用于类型转换
```python
#举例
a,b = input().split()
print(a,b)
print(type(a),type(b))
c,d = map(int,input().split())
print(c,d)
print(type(c),type(d))

#结果
1 2
1 2
<class 'str'> <class 'str'>
3 4
3 4
<class 'int'> <class 'int'>
```
***
***2022.11.11***
***
**集合Set**<br>

集合是无序的，的数学中的概念一样<br>
集合默认从小到大
```python
set = {1,2,3,3,4,4,45}
print(set)
set = {1,4,2,5,0}
print(set)
set = [1,4,4,2,3]
print(set)

#输出
{1, 2, 3, 4, 45} 
{0, 1, 2, 4, 5}
[1, 4, 4, 2, 3]
```

`add`函数<br>
既然集合是一种“容器”，那么我们就可以向里面添加元素
```python
set = {1,2,3,3,4,4,45}
set.add(9)
print(set)

#输出
{1, 2, 3, 4, 9, 45}
```
我们可以使用前文提到过的`add`函数、`remove`函数、`min`函数、`max`函数、`len`函数、`sum`函数...对集合进行操作<br>
之前我们提到过，由于集合内元素是无序的，所以我们不能像访问列表那样通过list[](下标)去访问集合中的元素<br>

使用`for`循环遍历集合
```python
set = {1,2,3,4,5}
for s in set :
    print(s)

#输出
1
2
3
4
5
```
并集(|)&交集(&)
```python
set_1 = {1,2,3,4}
set_2 = {4,5,6,7}
set_3 = {2022,2023}
print(set_1 | set_2)
print(set_1 & set_2)
print(set_1 & set_3)
print(set_1 ^ set_2) #”对称差“ 并集 - 交集
print(set_1 - set_2) #“差集” 在set_1中去除掉1与2的并集中的元素

#输出
{1,2,3,4,5,6,7}
{4}
set()
{1, 2, 3, 5, 6, 7}
{1,2,3}
```
**字典 Dictionary**<br>
```python
dic = {
    'one' : 1,  # {键(Key) : 值(Value)}
    'two' : 2,
    'three' : 3
}
print(dic)
del(dic['two']) #删除'two'
print(dic)
dic['two'] = 22 #新增'two'
print(dic)
dic['two'] = 2  #如果存在一个键为'two',那么将其值修改
print(dic)

#输出
{'one': 1, 'two': 2, 'three': 3}
{'one': 1, 'three': 3}
{'one': 1, 'three': 3, 'two': 22}
{'one': 1, 'three': 3, 'two': 2}
```
