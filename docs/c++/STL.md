# STL

## 基本概念

* STL(Standard Template Library,**标准模板库**)
* STL 从广义上分为: **容器(container) 算法(algorithm) 迭代器(iterator)**
* **容器**和**算法**之间通过**迭代器**进行无缝连接。
* STL 几乎所有的代码都采用了模板类或者模板函数

## 六大组件

STL大体分为六大组件，分别是:**容器、算法、迭代器、仿函数、适配器（配接器）、空间配置器**



1. 容器：各种数据结构，如vector、list、deque、set、map等,用来存放数据。

   这些容器分为**序列式容器**和**关联式容器**两种:

   - 序列式容器:强调值的排序，序列式容器中的每个元素均有固定的位置。
   - 关联式容器:二叉树结构，各元素之间没有严格的物理上的顺序关系

2. 算法：各种常用的算法，如sort、find、copy、for_each等

   算法分为:**质变算法**和**非质变算法**。

   - 质变算法：是指运算过程中会更改区间内的元素的内容。例如拷贝，替换，删除等等

   - 非质变算法：是指运算过程中不会更改区间内的元素内容，例如查找、计数、遍历、寻找极值等等

3. 迭代器：扮演了容器与算法之间的胶合剂。

   | 种类           | 功能                                                     | 支持运算                                |
   | -------------- | -------------------------------------------------------- | --------------------------------------- |
   | 输入迭代器     | 对数据的只读访问                                         | 只读，支持++、==、！=                   |
   | 输出迭代器     | 对数据的只写访问                                         | 只写，支持++                            |
   | 前向迭代器     | 读写操作，并能向前推进迭代器                             | 读写，支持++、==、！=                   |
   | 双向迭代器     | 读写操作，并能向前和向后操作                             | 读写，支持++、--，                      |
   | 随机访问迭代器 | 读写操作，可以以跳跃的方式访问任意数据，功能最强的迭代器 | 读写，支持++、--、[n]、-n、<、<=、>、>= |

4. 仿函数：行为类似函数，可作为算法的某种策略。

5. 适配器：一种用来修饰容器或者仿函数或迭代器接口的东西。

6. 空间配置器：负责空间的配置与管理。

## string

### 构造

```cpp
string str1;
string str2（str1);
string str3(10,'a');
```

### 赋值

```cpp
string str1="hello";
string str2=str1;
string str3;
str3.assign(str2);
```

### 拼接

```cpp
string str1="I";
str1+="love";
str1.append("you");
string str2="ABCDEF";
str1.append(str2,3,2);	//从下标3开始截取2个字符拼接到末尾
```

### 查找和替换

```cpp
string str1="ABCDEFGEFG";
int pos;
pos=str1.find("EF"); //从左往右找，返回下标
pos=str1.rfind("EF"); //从右往左
str1.replace(1,3,"kkkk"); //从下标1开始替换3个字符，结果为"AkkkkEFGEFG","BCD"被替换。
```

### 比较

字符串比较是按字符的ASCII码进行对比

= 返回   0

\> 返回   1 

< 返回  -1

### 字符存取

```cpp
str[0] = 'x';
cout<<str[0];
str.at(1) = 'x';
cout<<str.at(1);
```

### 插入和删除

```cpp
string str="AAA";
str.insert(1,"kkk");
//相当于str.insert(1,3,'k')；
//AkkkAA
str.erase(1,3);
//AAA
```

### 字串

```cpp
string str = "abcdefg";
string subStr = str.substr(1, 3); //"bcd"
```

## vector

vector容器的迭代器是支持随机访问的迭代器

```cpp
v.begin()//1st element
v.end()// the next of last element
```

### 构造

```cpp
vector<T> v;
vector v1(v.begin(),v.end());
vector v2(n,elem);
vector v3(const vector &vec); //拷贝构造
```

### 赋值

```cpp
vector<T> v1,v2,v3;
v2=v1;
v3.assign(v2.begin(),v2.end());
```

### 容量和大小

```cpp
v.empty();  //is empty?
v.capacity(); //容量 会动态扩展
v.size(); //大小
v.resize(int num, elem)   //elem非必要，默认为0，重新指定容器的长度为num，以elem填充扩展出来的位置。若变短，删除超长的元素
```

### 插入和删除

```cpp
v.insert(const_iterator pos,int count,ele); //向位置pos插入count个ele count参数可选，默认为1
v.erase(const_iterator pos);   //删除pos位置的元素
v.erase(const_iterator start, const_iterator end); //删除[start,end)的元素
v.clear //清空
```

### 数据存取

```cpp
v.at(idx);
v[idx];
```

### 互换容器

```cpp
v1.swap(v2); //把v2和v1互换
```

收缩内存

```cpp
void test()
{
	vector<int> v;
	for (int i = 0; i < 100000; i++) {
		v.push_back(i);
	}

	cout << "v的容量为：" << v.capacity() << endl;
	cout << "v的大小为：" << v.size() << endl;

	v.resize(3);

	cout << "v的容量为：" << v.capacity() << endl;
	cout << "v的大小为：" << v.size() << endl;

	//收缩内存 （v）表示拷贝构造，即拷贝构造了一个匿名对象，然后v和匿名对象进行交换，最后释放匿名对象
	vector<int>(v).swap(v); //匿名对象：当前行执行完马上回收

	cout << "v的容量为：" << v.capacity() << endl;
	cout << "v的大小为：" << v.size() << endl;
}
```

### 预留空间

```cpp
v.reserve(int len);   //预留len个元素长度，但不会初始化，因此不可访问
```

e.g

```cpp
#include <vector>
#include <iostream>

using namespace std;

void test01()
{
	vector<int> v;

	//预留空间
	v.reserve(100000);

	int num = 0;
	int* p = NULL;
	for (int i = 0; i < 100000; i++) {
		v.push_back(i);
		if (p != &v[0]) { //v[0]表示当前空间的首地址，如果p!=v[0]，说明开辟了新空间
			p = &v[0];
			num++;
		}
	}
	cout << "num:" << num << endl;
}

int main() {
	test01();
	return 0;
}
```

