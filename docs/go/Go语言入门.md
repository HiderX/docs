# Go语言入门

## 语言处理系统

### 解释型

- python
- javascript

![image-20240218091032596](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218091032596.png)

### 编译型

- go
- c++

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218091125408.png)

### 混合体

- java

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218091315400.png)

## 变量与类型

### 变量的内涵

执行环境中的数据的存储区域

### 强类型与弱类型

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2009.35.59.png)

### 变量的声明与赋值

```go
var name type = expression
```

```go
name := expression	//只能在函数里用
```

### 变量名

Go变量名以数字、字母或下划线组成，允许任何被视为字母或数字的Unicode字符

所以$\pi$也可以

### 变量生命周期

和C++差不多，略

### 作用域

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2009.43.22.png)

函数外部和函数内部有同名变量时，就近原则

## 运算符优先级

运算符种类几乎和C++一样，略

![截屏2024-02-18 09.49.42](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2009.49.42.png)

## 程序控制结构

### 选择结构

#### if-else

```go
if exp{
	
}else if{

}else{

}
```

注意，else一定要跟在`}`后面

#### switch-case

```go
switch var1{
	case val1:
	case val2,val3:
	default:
}
```

```go
switch{
	case exp1:
	case exp2:
	default:
}
```

### 循环结构

#### 完整C风格for循环

```go
for i:=0;i<10;i++{
	fmt.Println(i)
}
```

#### 只有条件判断的for循环

```go
i:=1
for i<100{
	fmt.Println(i)
	i*=2
}
```

#### 无限循环

```go
for{
	xxx
}
```

#### for-range循环

```go
for i,v:=range Vals{
	fmt.Println(i,v)
}
```

### Break&Continue

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218103556289.png)

### Label

![image-20240218103659076](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218103659076.png)

## 函数

### 函数声明

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218104357592.png)

```go
func first(x int,_ int) int //预留参数
```

```go
func test(a,b int) (int,err){ //多返回值
	xxx
}
```

```go
func addSum(sum ... int)int{	//... 表示可变参数，可以传入无穷多个int，用for-range获取值
	var sum int
	for _,value := range nums{
		sum+=value
	}
	return sum
}
```

### 函数递归

```go
func f1(n int)int{
	if n==1{
		return 1
	}
	return f1(n-1)*n
}
```

斐波那契数列-尾递归

```go
func fib(n int) int{
	return fibter(1,0,n)
}
func fibter(a,b,count int)int{
	if count==0{
		return b	//不是返回上一层，而是直接退出函数
	}
	return fibter(a+b,a,count-1)
}
```

### 高阶函数

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218152101531.png)

### 闭包

内层函数可以访问外层变量

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218152405798.png)

## 复合类型

### 数组

```go
var arr [10]int
var arr2 [12]int{1,5:4,6,10:11,11}
var arr [13][13]int{}
```

### 切片

```go
var slice1 []int
var slice2 = []int{1,2,3,4}
var slice3 = []int{1,5:10,19:111}
var slice4 = make([]int,length,capacity) //capacity 可省略 容量爆了就翻倍2->4->8->16
slice2:=slice[1:4]	//截取，左闭右开，但cap=4，会复用相同底层结构，共享同一块内存
```

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218184003767.png)

### 哈希表

```go
hash = f(key)
index = hash % array_size
```

哈希碰撞-拉链法

 ![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2020.02.42.png)

哈希碰撞-开放寻址法

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2020.03.14.png)

哈希表使用实例

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218200619531.png)

## defer

- 延迟执行 ![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2020.10.37.png)

- 参数预计算

  ![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2020.12.08.png)

  a=2

- LIFO执行顺序

  ![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2020.12.47.png)

  start 5->start 1

## panic 函数

### panic特性

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2020.19.52.png)

执行结果：

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218202041399.png)

虽然发生了panic异常信息，还是输出了defer语句中的信息，这说明panic的发生，还是会执行defer操作；先把defer栈清空再panic（死也要清白地死）

### recover函数

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2020.22.52.png)

输出结果：

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218202322182.png)

关于panic、recover、defer的执行顺序：

> https://www.jb51.net/article/272258.htm

## 接口

### 多态

```go
package main

import "fmt"

type AnimalIF interface {
	Sleep()
	GetColor() string
	GetType() string
}

type Cat struct {
	color string
}

func (c *Cat) GetColor() string {
	return c.color
}

func (c *Cat) GetType() string {
	return "cat"
}

func (c *Cat) Sleep() {
	fmt.Println("Cat is Sleep")
}

type Dog struct {
	color string
}

func (d *Dog) Sleep() {
	fmt.Println("Dog is Sleep")
}

func (d *Dog) GetColor() string {
	return d.color
}

func (d *Dog) GetType() string {
	return "Dog"
}

func main() {
	var animal AnimalIF
	animal = &Cat{"Green"}
	animal.Sleep()
	animal = &Dog{"Red"}
	fmt.Println(animal.GetType())
	animal.Sleep()
}
```

### 嵌套

```go
package main

import "fmt"

type Flyer interface {
	fly()
}

type Swimmer interface {
	swim()
}
type FlyFish interface {
	Flyer
	Swimmer
}

type Fish struct {
}

func (fish Fish) fly() {
	fmt.Println("fly")
}

func (fish Fish) swim() {
	fmt.Println("swim")
}

func main() {
	var ff FlyFish
	ff = Fish{}
	ff.fly()
	ff.swim()
}
```

### 类型断言

![image-20240218205120634](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218205120634.png)

空接口的类型断言

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218205219082.png)

## 反射

在Go语言的反射机制中，任何接口值都由是`一个具体类型`和`具体类型的值`两部分组成的。在Go语言中反射的相关功能由内置的reflect包提供，任意接口值在反射中都可以理解为由`reflect.Type`和`reflect.Value`两部分组成，并且reflect包提供了`reflect.TypeOf`和`reflect.ValueOf`两个函数来获取任意对象的Value和Type。

### TypeOf

在反射中关于类型还划分为两种：`类型（Type）`和`种类（Kind）`。因为在Go语言中我们可以使用type关键字构造很多自定义类型，而`种类（Kind）`就是指底层的类型，但在反射中，当需要区分指针、结构体等大品种的类型时，就会用到`种类（Kind）`。 

Go语言的反射中像数组、切片、Map、指针等类型的变量，它们的`.Name()`都是返回`空`。

在`reflect`包中定义的Kind类型如下：

```go
type Kind uint
const (
    Invalid Kind = iota  // 非法类型
    Bool                 // 布尔型
    Int                  // 有符号整型
    Int8                 // 有符号8位整型
    Int16                // 有符号16位整型
    Int32                // 有符号32位整型
    Int64                // 有符号64位整型
    Uint                 // 无符号整型
    Uint8                // 无符号8位整型
    Uint16               // 无符号16位整型
    Uint32               // 无符号32位整型
    Uint64               // 无符号64位整型
    Uintptr              // 指针
    Float32              // 单精度浮点数
    Float64              // 双精度浮点数
    Complex64            // 64位复数类型
    Complex128           // 128位复数类型
    Array                // 数组
    Chan                 // 通道
    Func                 // 函数
    Interface            // 接口
    Map                  // 映射
    Ptr                  // 指针
    Slice                // 切片
    String               // 字符串
    Struct               // 结构体
    UnsafePointer        // 底层指针
)
```

### ValueOf

`reflect.ValueOf()`返回的是`reflect.Value`类型，其中包含了原始值的值信息。`reflect.Value`与原始值之间可以互相转换。

`reflect.Value`类型提供的获取原始值的方法如下：

|           方法           |                             说明                             |
| :----------------------: | :----------------------------------------------------------: |
| Interface() interface {} | 将值以 interface{} 类型返回，可以通过类型断言转换为指定类型  |
|       Int() int64        |     将值以 int 类型返回，所有有符号整型均可以此方式返回      |
|      Uint() uint64       |     将值以 uint 类型返回，所有无符号整型均可以此方式返回     |
|     Float() float64      | 将值以双精度（float64）类型返回，所有浮点数（float32、float64）均可以此方式返回 |
|       Bool() bool        |                     将值以 bool 类型返回                     |
|     Bytes() []bytes      |               将值以字节数组 []bytes 类型返回                |
|     String() string      |                     将值以字符串类型返回                     |

E.g:

```go
v:=reflect.Valueof(x)
return int(v.Int())
```

想要在函数中通过反射修改变量的值，需要注意函数参数传递的是值拷贝，必须传递变量地址才能修改变量值。而反射中使用专有的`Elem()`方法来获取指针对应的值。

```go
package main

import (
	"fmt"
	"reflect"
)

func reflectSetValue1(x interface{}) {
	v := reflect.ValueOf(x)
	if v.Kind() == reflect.Int64 {
		v.SetInt(200) //修改的是副本，reflect包会引发panic
	}
}
func reflectSetValue2(x interface{}) {
	v := reflect.ValueOf(x)
	// 反射中使用 Elem()方法获取指针对应的值
	if v.Elem().Kind() == reflect.Int64 {
		v.Elem().SetInt(200)
	}
}
func main() {
	var a int64 = 100
	// reflectSetValue1(a) //panic: reflect: reflect.Value.SetInt using unaddressable value
	reflectSetValue2(&a)
	fmt.Println(a)
}
```

### 结构体反射

任意值通过`reflect.TypeOf()`获得反射对象信息后，如果它的类型是结构体，可以通过反射值对象（`reflect.Type`）的`NumField()`和`Field()`方法获得结构体成员的详细信息。

`reflect.Type`中与获取结构体成员相关的的方法如下表所示。

|                            方法                             |                             说明                             |
| :---------------------------------------------------------: | :----------------------------------------------------------: |
|                  Field(i int) StructField                   |          根据索引，返回索引对应的结构体字段的信息。          |
|                       NumField() int                        |                   返回结构体成员字段数量。                   |
|        FieldByName(name string) (StructField, bool)         |       根据给定字符串返回字符串对应的结构体字段的信息。       |
|            FieldByIndex(index []int) StructField            | 多层成员访问时，根据 []int 提供的每个结构体的字段索引，返回字段的信息。 |
| FieldByNameFunc(match func(string) bool) (StructField,bool) |              根据传入的匹配函数匹配需要的字段。              |
|                       NumMethod() int                       |                返回该类型的方法集中方法的数目                |
|                     Method(int) Method                      |                返回该类型方法集中的第i个方法                 |
|             MethodByName(string)(Method, bool)              |              根据方法名返回该类型方法集中的方法              |

E.g:

```go
package main

import (
	"fmt"
	"reflect"
)

type User struct {
	Id   int    `json:"id" ini:"s_id"`
	Name string `json:"name" ini:"s_name"`
	Age  int    `json:"score" ini:"s_score"`
	test interface{}
}

func (u User) Call(arg int) {
	fmt.Println(arg)
}

func main() {
	user := User{
		Id:   0,
		Name: "C++",
		Age:  3,
		test: 1131,
	}
	//user.Call()
	Do(user)
}

func Do(input interface{}) { //传指针加Elem()即可,加了Elem()必须要传指针
	t := reflect.TypeOf(input)
	v := reflect.ValueOf(input)
	fmt.Println("t is ", t)
	fmt.Println("v is ", v)
	for i := 0; i < t.NumField(); i++ { //t.Numfield==v.Numfield
		field := t.Field(i)
		value := v.Field(i)
		tag := t.Field(i).Tag.Get("json")
		fmt.Println("field is ", field, "\nvalue is ", value, "\ntag is ", tag)
	}
	fmt.Println("-------------------------------------------------------")
	for i := 0; i < v.NumMethod(); i++ {
		fmt.Println("i=", i)
		method := t.Method(i).Name
		var args = []reflect.Value{reflect.ValueOf(1)}
		fmt.Println(method)
		v.Method(i).Call(args)
	}
}
```

## Go 并发编程

一个线程可以对应多个协程

### 协程vs线程

#### 调度方式

协程依附于线程而存在

![截屏2024-02-18 21.11.53](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-18%2021.11.53.png)

#### 上下文切换速度

协程0.2微秒，线程1～2微秒

#### 调度策略

线程：抢占式

协程：协作式

#### 栈大小

线程默认的栈比较大（例如2MB）

而Go语言中的协程栈默认大小为2KB，且可以动态扩容

### goroutine

#### sync.WaitGroup

可以用`sync.WaitGroup`来让主线程在其他用户线程之后退出

```go
package main

import (
	"fmt"
	"sync"
)

// 声明全局等待组变量
var wg sync.WaitGroup

func hello() {
	fmt.Println("hello")
	wg.Done() // 告知当前goroutine完成
}

func main() {
	wg.Add(1) // 登记1个goroutine
	go hello()
	fmt.Println("你好")
	wg.Wait() // 阻塞等待登记的goroutine完成
}
```

#### 动态栈

操作系统的线程一般都有固定的栈内存（通常为2MB）,而 Go 语言中的 goroutine 非常轻量级，一个 goroutine 的初始栈空间很小（一般为2KB），所以在 Go 语言中一次创建数万个 goroutine 也是可能的。并且 goroutine 的栈不是固定的，可以根据需要动态地增大或缩小， Go 的 runtime 会自动为 goroutine 分配合适的栈空间

#### goroutine调度

操作系统内核在调度时会挂起当前正在执行的线程并将寄存器中的内容保存到内存中，然后选出接下来要执行的线程并从内存中恢复该线程的寄存器信息，然后恢复执行该线程的现场并开始执行线程。从一个线程切换到另一个线程需要完整的上下文切换。因为可能需要多次内存访问，索引这个切换上下文的操作开销较大，会增加运行的cpu周期。

区别于操作系统内核调度操作系统线程，goroutine 的调度是Go语言运行时（runtime）层面的实现，是完全由 Go 语言本身实现的一套调度系统——go scheduler。它的作用是按照一定的规则将所有的 goroutine 调度到操作系统线程上执行。

在经历数个版本的迭代之后，目前 Go 语言的调度器采用的是 `GPM` 调度模型。

![gpm](https://s2.loli.net/2023/12/15/xJ2lAHP9cWIfYrk.png)

其中：

- G：表示 goroutine，每执行一次`go f()`就创建一个 G，包含要执行的函数和上下文信息。
- 全局队列（Global Queue）：存放等待运行的 G。
- P：表示 goroutine 执行所需的资源，最多有 GOMAXPROCS 个。
- P 的本地队列：同全局队列类似，存放的也是等待运行的G，存的数量有限，不超过256个。新建 G 时，G 优先加入到 P 的本地队列，如果本地队列满了会批量移动部分 G 到全局队列。
- M：线程想运行任务就得获取 P，从 P 的本地队列获取 G，当 P 的本地队列为空时，M 也会尝试从全局队列或其他 P 的本地队列获取 G。M 运行 G，G 执行之后，M 会从 P 获取下一个 G，不断重复下去。
- Goroutine 调度器和操作系统调度器是通过 M 结合起来的，每个 M 都代表了1个内核线程，操作系统调度器负责把内核线程分配到 CPU 的核上执行。

单从线程调度讲，Go语言相比起其他语言的优势在于OS线程是由OS内核来调度的， goroutine 则是由Go运行时（runtime）自己的调度器调度的，完全是在用户态下完成的， 不涉及内核态与用户态之间的频繁切换，包括内存的分配与释放，都是在用户态维护着一块大的内存池， 不直接调用系统的malloc函数（除非内存池需要改变），成本比调度OS线程低很多。 另一方面充分利用了多核的硬件资源，近似的把若干goroutine均分在物理线程上， 再加上本身 goroutine 的超轻量级，以上种种特性保证了 goroutine 调度方面的性能。

- Work stealing

	所有P放满了才会放到全局队列，如果某个M没东西了，会从其他P偷一个G过来，·	其他P没得偷从全局偷

- handoff

  如果某P的本地队列中的某G使得M阻塞，P会移动到另一个唤醒/创建的M，原来的M在G运行完之后睡眠或者销毁

#### GOMAXPROCS

Go运行时的调度器使用`GOMAXPROCS`参数来确定需要使用多少个 OS 线程来同时执行 Go 代码。默认值是机器上的 CPU 核心数。

```go
func main(){
	runtime.GOMAXPROCS(i)
}
```

### channel

Go语言采用的并发模型是`CSP（Communicating Sequential Processes）`，提倡**通过通信共享内存**而不是**通过共享内存而实现通信**。

只读通道：`v <-chan int`

只写通道：`v chan<- int`

**注意：**一个通道值是可以被垃圾回收掉的。通道通常由发送方执行关闭操作，并且只有在接收方明确等待通道关闭的信号时才需要执行关闭操作。它和关闭文件不一样，通常在结束操作之后关闭文件是必须要做的，但关闭通道不是必须的。

关闭后的通道有以下特点：

1. 对一个关闭的通道再发送值就会导致 panic。
2. 对一个关闭的通道进行接收会一直获取值直到通道为空。
3. 对一个关闭的并且没有值的通道执行接收操作会得到对应类型的零值。
4. 关闭一个已经关闭的通道会导致 panic。

无缓冲通道：`c := make(chan int)`

有缓冲通道：`cc := make(chan int, 3)`

对无缓冲通道发送消息而不接收会造成死锁，我们要创建一个goroutine来接收通道中的内容：

```go
func recv(c chan int) {
	ret := <-c
	fmt.Println("接收成功", ret)
}

func main() {
	ch := make(chan int)
	go recv(ch) // 创建一个 goroutine 从通道接收值
	ch <- 10
	fmt.Println("发送成功")
}
```

我们可以用多返回值模式来判断通道是否关闭：

```go
value, ok := <- ch
```

其中：

- value：从通道中取出的值，如果通道被关闭则返回对应类型的零值。
- ok：通道ch关闭时返回 false，否则返回 true。

#### Worker Pool

E.g：三个线程干五个活

```go
package main

import (
	"fmt"
	"time"
)

func worker(id int, jobs <-chan int, results chan<- int) {
	for job := range jobs {
		fmt.Println("worker id: ", id, "doing job: ", job)
		results <- job * 2
		time.Sleep(time.Second)
		fmt.Println("worker id: ", id, "finished job: ", job)
	}
}

func main() {
	jobs := make(chan int, 100)
	results := make(chan int, 100)

	for j := 0; j < 3; j++ {
		go worker(j, jobs, results)
	}

	for i := 0; i < 5; i++ {
		jobs <- i
	}
	close(jobs)

	for i := 0; i < 5; i++ {
		fmt.Println(<-results)
	}

}
```

#### select

Select 语句具有以下特点。

- 可处理一个或多个 channel 的发送/接收操作。
- 如果多个 case 同时满足，select 会**随机**选择一个执行。
- 对于没有 case 的 select 会一直阻塞，可用于阻塞 main 函数，防止退出

```go
package main

import "fmt"

func main() {
	ch := make(chan int, 1)

	for i := 0; i < 10; i++ {
		select { //如果多个case都满足，随机选一个执行
		case x := <-ch: //可以从channel中取值
			fmt.Println("Receiving", x)

		case ch <- i:
			fmt.Println("Sending ", i) //可以从channel中存放值
		default:
			fmt.Println("do nothing")
		}
	}
}
```

### 并发安全和锁

#### 原子锁

梦回操作系统

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218211839731.png)

#### 互斥锁

互斥锁是一种常用的控制共享资源访问的方法，它能够保证同一时间只有一个 goroutine 可以访问共享资源。Go 语言中使用`sync`包中提供的`Mutex`类型来实现互斥锁。

`sync.Mutex`提供了两个方法供我们使用。

|          方法名          |    功能    |
| :----------------------: | :--------: |
|  func (m *Mutex) Lock()  | 获取互斥锁 |
| func (m *Mutex) Unlock() | 释放互斥锁 |

```go
package main

import (
	"fmt"
	"sync"
)

// sync.Mutex

var (
	x int64
	wg sync.WaitGroup // 等待组
	m sync.Mutex // 互斥锁
)

// add 对全局变量x执行5000次加1操作
func add() {
	for i := 0; i < 5000; i++ {
		m.Lock() // 修改x前加锁
		x = x + 1
		m.Unlock() // 改完解锁
	}
	wg.Done()
}

func main() {
	wg.Add(2)

	go add()
	go add()

	wg.Wait()
	fmt.Println(x)
}
```

#### 读写互斥锁

互斥锁是完全互斥的，但是实际上有很多场景是读多写少的，当我们并发的去读取一个资源而不涉及资源修改的时候是没有必要加互斥锁的，这种场景下使用读写锁是更好的一种选择。读写锁在 Go 语言中使用`sync`包中的`RWMutex`类型。

`sync.RWMutex`提供了以下5个方法。

|               方法名                |              功能              |
| :---------------------------------: | :----------------------------: |
|      func (rw *RWMutex) Lock()      |            获取写锁            |
|     func (rw *RWMutex) Unlock()     |            释放写锁            |
|     func (rw *RWMutex) RLock()      |            获取读锁            |
|    func (rw *RWMutex) RUnlock()     |            释放读锁            |
| func (rw *RWMutex) RLocker() Locker | 返回一个实现Locker接口的读写锁 |

读写锁分为两种：读锁和写锁。当一个 goroutine 获取到读锁之后，其他的 goroutine 如果是获取读锁会继续获得锁，如果是获取写锁就会等待；而当一个 goroutine 获取写锁之后，其他的 goroutine 无论是获取读锁还是写锁都会等待。

在读多写少（相差一个数量级）的情况下，使用读写互斥锁比起使用互斥锁可以提高执行效率

```go
// 使用互斥锁，10并发写，1000并发读
do(writeWithLock, readWithLock, 10, 1000) // x:10 cost:1.466500951s

// 使用读写互斥锁，10并发写，1000并发读
do(writeWithRWLock, readWithRWLock, 10, 1000) // x:10 cost:117.207592ms
```

#### sync.WaitGroup

|                方法名                |        功能         |
| :----------------------------------: | :-----------------: |
| func (wg * WaitGroup) Add(delta int) |    计数器+delta     |
|        (wg *WaitGroup) Done()        |      计数器-1       |
|        (wg *WaitGroup) Wait()        | 阻塞直到计数器变为0 |

```go
var wg sync.WaitGroup

func hello() {
	defer wg.Done()
	fmt.Println("Hello Goroutine!")
}
func main() {
	wg.Add(1)
	go hello() // 启动另外一个goroutine去执行hello函数
	fmt.Println("main goroutine done!")
	wg.Wait()
}
```

#### sync.Once

在某些场景下我们需要确保某些操作即使在高并发的场景下也只会被执行一次，例如只加载一次配置文件等。

Go语言中的`sync`包中提供了一个针对只执行一次场景的解决方案——`sync.Once`，`sync.Once`只有一个`Do`方法

```go
package singleton

import (
    "sync"
)

type singleton struct {}

var instance *singleton
var once sync.Once

func GetInstance() *singleton {
    once.Do(func() {
        instance = &singleton{}
    })
    return instance
}
```

#### sync.Map

Go 语言中内置的 map 不是并发安全的，当并发地写map时会报错`fatal error: concurrent map writes`，因此我们可以使用`sync.Map`

|                            方法名                            |              功能               |
| :----------------------------------------------------------: | :-----------------------------: |
|         func (m *Map) Store(key, value interface{})          |        存储key-value数据        |
| func (m *Map) Load(key interface{}) (value interface{}, ok bool) |       查询key对应的value        |
| func (m *Map) LoadOrStore(key, value interface{}) (actual interface{}, loaded bool) |    查询或存储key对应的value     |
| func (m *Map) LoadAndDelete(key interface{}) (value interface{}, loaded bool) |          查询并删除key          |
|            func (m *Map) Delete(key interface{})             |             删除key             |
|   func (m *Map) Range(f func(key, value interface{}) bool)   | 对map中的每个key-value依次调用f |

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	wg := sync.WaitGroup{}
	m := sync.Map{}
	for i := 0; i < 20; i++ {
		go func(i int) {
			wg.Add(1)
			m.Store(i, i+100)
			t, _ := m.Load(i)
			fmt.Println(i, ":", t)
			wg.Done()
		}(i)
	}
	wg.Wait()
}
```

#### Cond

```go
var c sync.Cond
//协程A
c.L.Lock()
for !conditon(){
	c.Wait()
}
c.L.Unlock
//协程B
c.Broadcast()
```

> 感谢[李文周大佬的教程](https://www.liwenzhou.com/posts/Go/concurrence/)

#### GO并发模式

##### Ping-Pong模式

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218220017271.png)

##### Fan-in模式

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218220432486.png)

##### Fan-out模式

Worker Pool是一个典型的例子

![image-20240218220726384](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218220726384.png)

##### Sub-worker模式

对Fan-out的扩展

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218220917957.png)

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218221234891.png)

##### Pipeline模式

其实就是linux的管道，把前一个的输出作为后一个的输入

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218221836910.png)

Step1. generator

![image-20240224105041699](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240224105041699.png)

Step2. multiply

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218222027127.png)

Step3. add

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218222042163.png)

例子-筛选素数：

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240218222342130.png)

## 依赖管理

 ### GOPATH

可以用`go env`来查看

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-19%2009.36.52.png)

### GO Modules

用GOPATH是很痛苦的，当我们需要切换版本的时候，就要切换GOPATH

而GO Modules解决了这一问题

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-02-19%2009.39.36.png)

```bash
go mod init modulename
go get modulename
go mod tidy
```

## 其他

### 构造函数

不同于C++，Go本身是没有构造函数的，但我们可以人为地写一个

```go
package main

import "fmt"

type Person struct {
	name string
	age  int
}

func NewPerson(name string, age int) (*Person, error) {
	if name == "" {
		return nil, fmt.Errorf("name is null")
	}
	if age < 0 {
		return nil, fmt.Errorf("age must be above 0")
	}
	return &Person{name, age}, nil
}

func main() {
	per, err := NewPerson("tom", -1)

	if err == nil {
		fmt.Println(per)
	} else {
		fmt.Println(err)
	}
}
```

***入门篇到此为止，测试、调试、泛型等内容不在入门篇做介绍***