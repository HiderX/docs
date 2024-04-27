# Python中的参数和返回值

我们先来看最基本的python函数：

```python
def testfunction():
    print("hello world")

testfunction()
```

这个函数没有任何参数，没有任何返回值，现在我们做一些小升级：

```python
def testfunction1(a,b):
    return a+b

r=testfunction1(1,1)
print(r)	#2
```

实现了简单的加法计算。我们也可以设置默认值：

```python
def testfunction2(a,b=1):
    return a/b

r=testfunction2(9)
print(r)	#9
```

我们也可以传入任意数量的实参

```python
def testfunction3(a,*b):	#a is a list []
    print(a+" has")
    for i in b:
        print(i)

testfunction3('cat','leg','tail','head','hand')
```

或者任意数量的关键字实参

```python
def testfunction3(a,**b):	#b is a dict {}
    print(a+" has")
    for k,v in b.items():
        print(v,k+"s")

testfunction3('cat',leg=4,tail=1,head=1)
```

自python3.5开始，PEP484为python引入了类型注解(type hints)

- 类型检查，防止运行时出现参数和返回值类型、变量类型不符合。
- 作为开发文档附加说明，方便使用者调用时传入和返回参数类型。
- 该模块加入后并不会影响程序的运行，不会报正式的错误，只有提醒pycharm目前支持typing检查，参数类型错误会黄色提示

```python
def testfunction4(a:int,b:str)->str:	#类型注解 a:int,b:str
    return a+b

r=testfunction4(1,2)	#(1,2)可以正常执行，但是(1,"2")报错
print(type(r))	#int
```

虽然指定了传入值类型和返回值类型，但并不会报错，接下来尝试一下多返回值：

```python
def testfunction5(a,b):
    return a,b,"ddd"

r1,r2,r3=testfunction5(1,2)
print(r1,r2,r3)	#1 2 ddd
print(type(testfunction5(1,2)))	#<class 'tuple'>
```

return只能返回单值，python会自动创建一个元组