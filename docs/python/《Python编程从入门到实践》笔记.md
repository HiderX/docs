# 《Python编程从入门到实践》笔记

> ⚠️本文仅记录了本人认为需要记录的内容，大多是python独有的特性，存在排版随意、知识点不全面等问题，不可作为教程使用！本文的顺序与原书不完全一致
>
> 如果你有其他语言的基础，本文可用作python速通


## 字符串

```python
t="test string"
print(t.title())	#Test String
print(t.upper())	#TEST STRING
print(t.lower())	#test string
```

```python
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"	#f means format
print(f"Hello, {full_name.title()}")
```

```python
t=" test string "
print(t.lstrip())	#test string[space]
print(t.rstrip())	#[space]test string
print(t.strip())	#test string
```

```python
t="https://amadeus.ink"
print(t.removeprefix("https://")) #amadeus.ink
```

关于[Python-单引号、双引号和三引号的作用和区别](https://www.cnblogs.com/yeyuzhuanjia/p/17395819.html)

## 数

任意两个数相除，结果总是浮点数

python没有内置的常量类型

```python
import this
3**2	#3^2 = pow(3,2)
14_000_000_000 #数很大可以用_分割，python会自动忽略
```

## 列表

`test[-1]`返回`test`的最后一个元素

```python
test.append('xxx') #增加一个元素
test.insert(idx,'xxx')	#在idx处插入一个元素，后面的元素自动后移
del test[idx]	#删除idx处的元素
last=test.pop()	#删除末尾元素，同时存入last
t=test.pop(idx)	#删除idx处的元素，同时存入t
t.remove('xxx')	#根据名字删除元素，注意只会删第一个，若要全删，需使用循环
```

排序

```python
test.sort()	#永久排序
test.sort(reverse=True)	#倒序排序
print(test.sorted())	#临时排序
```

```python
test.reverse()	#逆转
len(test)	#获取长度
```

遍历

```python
for t in test:
  print(t)
```

```python
for v in range(1,5):	#[1,5)
  print(v)
for v in range(1,9,2):	#step=2
  print(v)	#1,3,5,7
```

```python
numbers=list(range(1,6))	#range(a,b)	a b都必须是int
print(numbers)	#1,2,3,4,5
print(sum(numbers))	#只能对数值list使用
print(max(numbers))	#也可以对字符串使用
print(min(numbers))
```

切片：列表的部分元素

```python
test=[1,2,3,4,5]
print(test[0:3])	#[0,3)
print(test[:4])	#[0,4)
print(test[3:])	#[3,last]
print(test[-3:])	#最后三个元素
#可以在括号内指定第三个值，表示step
```

```python
t1=[1,2,3,4,5]
t2=t1	#t2和t1指向同一块内存
t2=t1[:]	#创建一份t1的副本，相互独立
```

元组：不可变的列表

```python
test=(1,2,3,4,5)	#圆括号
for t in test:
  print(t)
```

```python
test=(1,2,3)
test[0]=1	#非法，不可以修改
test=(1,2)	#不能修改，但可以重新赋值
```

## 字典

字典是一系列键值对，值可以是数、字符串、列表、字典

一个对象能不能作为字典的key，就取决于其有没有hash方法。所以所有python自带类型中，目前我已知的除了list、dict、set和内部带有以上三种类型的tuple之外，其余的对象都能当key

>https://blog.csdn.net/lnotime/article/details/81192207

```python
test={'color':'red',
     'point':5,
     'name':'test'}
print(test['name'])
test['x']='xx'	#添加key-value pair
test['y']='yy'
print(test)	#{'color': 'red', 'point': 5, 'name': 'test', 'x': 'xx', 'y': 'yy'}
test['point']=1	#修改键值对
del test['point']	#删除键值对
```

字典也可以定义为空，之后再加入内容

```python
test={}
test['x']='xxx'
```

```python
test={'color':'red',
     'point':5,
     'name':'test',
     'color':'blue'}	#blue会覆盖red
```

当键值对不存在时，直接使用访问会报错，可以使用`get()`

```python
test={'color':'red',
     'point':5,
     'name':'test'}
print(test['hhh'])	#KeyError
print(test.get('hhh'),'No value')	#第二个参数为当指定的键不存在时的返回值，可选（默认返回None）
```

遍历

```python
for k,v in test.items():	#key-values
  print(f"{k}:{v}")
 
for k in test:	#keys
   print(f"{k}")

for k in test.keys():	#keys 返回一个包含所有key的list，因此也可以用in和not in，也可以排序
  print(f"{k}")

for k in sorted(test.keys()):
  print(f"{k}")
  
for v in test.values():	#values 返回包含所有value的list
  print(f"{v}")
  
for v in set(test.values()):	#set用于去重	s={1,2,3,4,5}	set也使用花括号
  print(f"{v}")
```

套娃

```python
test0={'color':'red',
     'point':0,
     'name':'test0'}
test1={'color':'blue',
       'point':1,
       'name':'test1'}
test2={'color':'green',
       'point':2,
       'name':'test2'}
test=[test0,test1,test2]
for i in test:
    print(i)
```

```python
test={'color':['red','blue','green'],
     'point':0,
     'name':'test0'}
for c in test['color']:
    print(c)
```

```python
test = {
    'test0': {
        'color': 'red',
        'point': 0,
        'name': 'test0'
    },
    'test1': {
        'color': 'blue',
        'point': 1,
        'name': 'test1'
    },
    'test2': {
        'color': 'green',
        'point': 2,
        'name': 'test2'
    }
}
for k,v in test.items():
    print(f"{k} has the following attributes:")
    for kk,vv in v.items():
        print(kk, vv)
    print()	#换行
```

## if-else

```python
if condition:
  do()
elif condition:
  do()
else:	#if、elif后不一定有else
  do()
```

python可以检查元素是否在列表中

```python
'a' in test
'a' not in test
```

当列表名用作条件表达式时，如果非空就返回`true`，空就返回`false`

```python
test=[]
if test:
	print("empty!")
```

在比较运算符两边各加一个空格可以让代码读起来更容易

## while操作列表

删除列表中的特定值

```python
pets=['dog','cat','dog','cat','cat','cat']

while 'cat' in pets:	#'cat' in pets也是一个expression
    pets.remove('cat')

print(pets)
```

我们不用for来修改列表，因为

1. 迭代原理： for循环在迭代过程中会按顺序访问列表的元素。如果在循环中修改了列表，可能会导致迭代器失效，造成意外行为或错误的结果。
2. 引用机制： Python中的变量是对象的引用，而不是直接存储对象本身的值。**当你通过for循环遍历列表时，实际上是在使用列表的迭代器，而不是直接访问列表的元素。**如果在循环中修改了列表，可能会影响到迭代器的行为，导致不可预测的结果。
> https://www.zhihu.com/question/49098374/answer/3329610198

如果不修改列表的长度，我们可以使用`enumerate()`

```python
my_list = ['fql', 'jiyik', 'com']

for index, item in enumerate(my_list):
    # 👇️ only updating values in the list
    my_list[index] = item + str(index)

print(my_list)  # 👉️ ['fql0', 'jiyik1', 'com2']
```

如果改变了列表长度，可以使用倒序遍历或者拷贝一份

```python
lst = [1, 3, 2, 5, 7, 9]

for i in reversed(lst):
    if i % 2 == 1:
        lst.remove(i)

print(lst)

#等价写法
num_list = [1, 2, 3, 4, 5]
print(num_list)

for i in range(len(num_list)-1, -1, -1):
    if num_list[i] == 2:
        num_list.pop(i)
    else:
        print(num_list[i])

print(num_list)
```

```python
#浅拷贝
import copy
lst = [1, 3, 2, 5, 7, 9]

for i in copy.copy(lst):
    if i % 2 == 1:
        lst.remove(i)

print(lst)

#等价写法，也是浅拷贝，使用copy.deepcopy()进行深拷贝
num_list = [1, 2, 3, 4, 5]
print(num_list)

for item in num_list[:]:
    if item == 2:
        num_list.remove(item)    else:
        print(item)

print(num_list)
```

> https://www.cnblogs.com/bananaplan/p/remove-listitem-while-iterating.html

## 函数

还是从最简单的函数开始

```python
def greet(username,year):	#形参
    print(f"Hello, {username}, {year}")

greet("Amadeus",2024)	#位置实参
```

```python
def greet(username,year):	#形参
    print(f"Hello, {username}, {year}")

greet(username="Amadeus",year=2024)	#关键字实参
```

```python
def greet(username,year=2024):	#形参可以设定默认值
    print(f"Hello, {username}, {year}")

greet(username="Amadeus")	#关键字实参
```

```python
def greet(username,year=2024):	#形参可以设定默认值
    print(f"Hello, {username}, {year}")
    return username.title()	#返回值

print(greet(username="amadeus"))
```

传递任意数量的实参

```python
def build_profile(first, last, **user_info):	#**表示字典，*表示元组
   user_info['first_name'] = first
   user_info['last_name'] = last
   return user_info

user_profile = build_profile('albert', 'einstein', location='princeton', field='physics')
print(user_profile)
```

导入模块中的函数

```python
import module_name	#整个模块
from module_name import function_1,function2,function3	#指定函数
from module_name import function as f	#别名
import module_name as m	#别名
import module_name import *	#所有函数
#如果导入的是包，要使用module_name.function()调用函数，导入了函数则可以直接用function()调用，但是可能会出现重名问题
```

## 类

不同于之前学过的语言，python有个很新奇的东西叫`self`，作用和C++的`this`差不多，但也有不同

1. `self`是类的`__init__`方法必须有的形参，必须在其他形参的前面，python调用类的方法时自动传入`self`实参，它是一个指向实例本身的引用
2. 经过测试，发现其他方法不传入`self`也不会有问题，只要不使用实例的属性

一般来说，我们规定类的名字首字母必须大写，但不大写也不会报错

```python
class Test:
    def __init__(self) -> None:	#->显式地规定了返回值类型
        pass	#pass 是空语句，是为了保持程序结构的完整性。占位
    def test():
        print("Hello World")

Test.test()
```

```python
class Character:
    def __init__(self, name, skill, hometown,description):
        self.name = name
        self.skill = skill
        self.hometown = hometown
        self.lv = 0 #默认值
        self.description = description
    def __str__(self):
        return f"{self.name},{self.description},普攻：{self.skill[0]},元素战技：{self.skill[1]},元素爆发：{self.skill[2]}"
    def upgrade(self):
        self.lv += 1
        return f"{self.name} is now level {self.lv}!"
    
ayaka=Character("神里绫华",["神里流·霜灭","神里流·倾","神里流·冰华"],"稻妻","稻妻「社奉行」神里家的大小姐。端庄而文雅，聪慧又坚韧。")
print(ayaka)
```

```python
class Character:
    def __init__(self, name, skills, hometown,description):
        self.name = name
        self.skills = skill(skills) #使用skill类，便于复用skill
        self.hometown = hometown
        self.lv = 0 #默认值
        self.description = description
    def __str__(self):
        return f"{self.name},{self.description},{self.skills.listskill()}"  #调用skill类的方法
    def upgrade(self):
        self.lv += 1
        return f"{self.name} is now level {self.lv}!"

class whitehair(Character):
    def __init__(self, name, skill, hometown,description):
        super().__init__(name, skill, hometown,description)
        self.hair = "white"
    def upgrade(self):  #重写父类的方法
        print("already lv90")

class skill:
    def __init__(self, skills):
        self.skills = skills
    def listskill(self):
        return f"普攻：{self.skills[0]},元素战技：{self.skills[1]},元素爆发：{self.skills[2]}"

ayaka=whitehair("神里绫华",["神里流·霜灭","神里流·倾","神里流·冰华"],"稻妻","稻妻「社奉行」神里家的大小姐。端庄而文雅，聪慧又坚韧。")
print(ayaka)
ayaka.upgrade()
```

可以把类放进单独的模块，然后在调用的时候import即可

```python
import module_name	#整个模块
from module_name import class1,class2,class3	#指定类
from module_name import class0 as c	#别名
import module_name as m	#别名
import module_name import *	#所有类
#如果导入的是包，要使用module_name.class0()调用类，导入了函数则可以直接用class0()调用，但是可能会出现重名问题
```

## 文件和异常

文件

```python
from pathlib import Path

path=Path("hhh.txt")
content=path.read_text()
lines=content.splitlines()	#分行
for line in lines:
    if(line==""):
        continue
    print(line)
```

hhh.txt：

```
在一个平凡的小镇上，有一家闻名遐迩的小餐馆，名叫“双份快乐”。这家餐馆有一个独特的传统：无论顾客点什么菜，都会得到两份。最初，这个传统让许多初次来访的顾客感到困惑，但很快，他们就明白了其中的乐趣和意义。

故事的主角是一对双胞胎兄弟，杰克和汤姆。他们自从小的时候就经常来到“双份快乐”吃饭，对这家餐馆有着特别的情感。一天，兄弟俩决定来到这里庆祝他们的成年生日。

杰克和汤姆坐下后，便开始浏览菜单。他们决定各自点一道自己最喜欢的菜，然后交换其中的一份，这样两人都能品尝到对方最喜欢的菜。杰克点了一份意大利面，而汤姆点了一份墨西哥辣鸡。当服务员按照餐馆的传统，给他们每人上了两份时，他们对彼此的选择满是期待。

然而，这顿饭不仅仅是一次美食的分享，还是一次深刻的情感交流。吃着对方挑选的菜肴，杰克和汤姆回忆起了他们一起成长的点点滴滴。每一口食物都似乎带着过去的味道，让这个简单的行为充满了意义。

餐后，他们意识到，尽管各自的生活道路可能会有所不同，但这种分享和相互理解的传统会继续下去。他们承诺，无论未来发生什么，每年的这一天，都会回到“双份快乐”来庆祝他们的兄弟情谊。

故事的结尾，留给了兄弟俩未来无限的可能。这不仅仅是关于食物的分享，更是关于生活中无论顺境还是逆境，都能相互扶持，共同前进的承诺。在“双份快乐”的见证下，杰克和汤姆的故事，就像他们所分享的那份美味一样，变得更加丰富和珍贵。
```

```python
from pathlib import Path
from character import Whitehair

path=Path("hhh.txt")
ayaka=Whitehair("神里绫华",["神里流·霜灭","神里流·倾","神里流·冰华"],"稻妻","稻妻「社奉行」神里家的大小姐。端庄而文雅，聪慧又坚韧。")
path.write_text(str(ayaka))	#写入内容必须是字符串，str(ayaka)等价于ayaka.__str__
#注意，write_text会完全覆写原文件！
```

```python
from pathlib import Path
import json

def get_stored_username(path):
    if path.exists():
       contents=path.read_text()
       username=json.loads(contents)
       return username
    else:
        return None

def greet_user():
    username=input("your name plz")
    path=Path(f"{username}.json")
    data=get_stored_username(path)
    if data:
        print(f"Welcome back, {username}!")
    else:
        a=input("What is your age")
        t={"name":username,"age":a}
        path.write_text(json.dumps(t))
        print(f"We'll remember you when you come back, {username}!")

greet_user()
```

异常

```python
a,b = map(lambda x:int(x),input("请输入两个数：").split())	#lambda表达式

try:
    ans=a/b
except ZeroDivisionError:
    print("Division by zero is not allowed")	#也可以直接写pass，静默失败
else:
    print(ans)
```

## 测试代码

先安装pytest

```bash
python -m pip install --user pytest
```

然后在你需要测试的文件所在的目录运行`pytest`

注意，测试函数和测试文件都必须以`test_`开头

```python
#test_cal.py
from cal import collatz
import random

def test_collatz():
    for i in range(1, 100):
        assert collatz(random.randint(i*32768, i*65536)) == 1
```

结果：

```bash
% pytest 
======================================================================== test session starts =========================================================================
platform darwin -- Python 3.11.5, pytest-7.4.0, pluggy-1.0.0
rootdir: /Users/yicheng/PycharmProjects/pytest
plugins: anyio-4.2.0
collected 1 item                                                                                                                                                     

test_cal.py .                                                                                                                                                  [100%]

========================================================================= 1 passed in 0.05s ==========================================================================
```

也可以通过`pytest filename`指定要测试的文件

*夹具：应用了装饰器`@pytest.fixture`的函数

```python
import pytest
from survey import AnonymousSurvey

@pytest.fixture
def language_survey():
  question="what do u speak"
  language_survey=AnonymousSurvey(question)
  return language_survey

def test_store_single_response(language_survey):
  language_survey.store_response('Eng')
  assert 'Eng' in language_survey.responses
  
def test_store_three_responses(language_survey):
  responses=['Eng','Chi','Jap']
  for response in responses:
    language_survey.store_response(response)
    
  for response in responses:
    assert response in language_survey.responses
```

我们将装饰器`@pytest.fixture`用于`language_survey()`函数。当测试函数的一个形参与应用了装饰器`@pytest.fixture`的函数（夹具）同名时，将自动运行夹具，并将夹具返回的值传递给测试函数。
