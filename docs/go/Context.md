# Context

## 声明

```go
type Context interface {	//接口
  Deadline() (deadline time.Time, ok bool)	//截止时间
  Done() <-chan struct{}	//协程是否结束，返回只读通道结构体
  Err() error	//错误信息，返回error类型
  Value(key any) any	//存储数据
}
```

## 数据传递

```go
package main

import (
	"context"
	"fmt"
)

func main() {
	ctx := context.Background()
	ctx = context.WithValue(ctx, "access_token", "123")
	GetUser(ctx)
}

func GetUser(ctx context.Context) {
	accessToken := ctx.Value("access_token")
	fmt.Println(accessToken)
}
```

## 取消协程 WithCancel

可以假设这样一个场景，用户想要查看订单记录，开启查询一个协程，但这是一个耗时操作，所以可能会中途取消。用户取消了查询，那么这个协程就应该停止，how？

```go
package main

import (
	"context"
	"fmt"
	"sync"
	"time"
)

var wait = sync.WaitGroup{}

func main() {
	t := time.Now()
	ctx, cancel := context.WithCancel(context.Background())
	wait.Add(1)
	go func() {
		info, err := GetInfo(ctx)
		fmt.Println(info, err)
 	}()
	go func() {
		time.Sleep(2 * time.Second)
		cancel() // 取消
	}()
	wait.Wait()
	fmt.Println(time.Since(t))
}

func GetInfo(ctx context.Context) (order []string, err error) {
	go func() {
		select {
		case <-ctx.Done():
			fmt.Println("Canceled")
			err = ctx.Err()
			wait.Done()
			return
		}
	}()
	time.Sleep(4 * time.Second) // 模拟耗时操作
	wait.Done()
	return []string{"a", "b", "c"}, nil
}
```

## 截止时间 WithDeadline

```go
package main

import (
	"context"
	"fmt"
	"sync"
	"time"
)

var wait = sync.WaitGroup{}

func main() {
	t := time.Now()
	ctx, _ := context.WithDeadline(context.Background(), time.Now().Add(3*time.Second))
	wait.Add(1)
	go func() {
		info, err := GetInfo(ctx)
		fmt.Println(info, err)
	}()
  //cancel()	可以手动调用cancel取消
  wait.Wait()
	fmt.Println(time.Since(t))
}

func GetInfo(ctx context.Context) (order []string, err error) {
	go func() {
		select {
		case <-ctx.Done():
			fmt.Println("Canceled")
			err = ctx.Err()
			wait.Done()
			return
		}
	}()
	time.Sleep(4 * time.Second) // 模拟耗时操作
	wait.Done()
	return []string{"a", "b", "c"}, nil
}
```

## 超时时间 WithTimeout

```go
package main

import (
	"context"
	"fmt"
	"sync"
	"time"
)

var wait = sync.WaitGroup{}

func main() {
	t := time.Now()
	ctx, _ := context.WithTimeout(context.Background(), 3*time.Second)
	wait.Add(1)
	go func() {
		info, err := GetInfo(ctx)
		fmt.Println(info, err)
	}()
  //cancel()	同样可以手动调用cancel取消
	wait.Wait()
	fmt.Println(time.Since(t))
}

func GetInfo(ctx context.Context) (order []string, err error) {
	go func() {
		select {
		case <-ctx.Done():
			fmt.Println("Canceled")
			err = ctx.Err()
			wait.Done()
			return
		}
	}()
	time.Sleep(4 * time.Second) // 模拟耗时操作
	wait.Done()
	return []string{"a", "b", "c"}, nil
}
```

> https://www.bilibili.com/video/BV1ix4y1k721