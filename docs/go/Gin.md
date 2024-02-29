# Gin

终于来哩！

**Gin** 是一个 Go (Golang) 编写的轻量级 http web 框架

Gin 的官网:https://gin-gonic.com/zh-cn/

Gin Github 地址:https://github.com/gin-gonic/gin

## 环境搭建

1. 下载&安装

在项目目录下面执行

```bash
go get -u github.com/gin-gonic/gin
```

2. 将 gin 引入到代码中

```go
import "github.com/gin-gonic/gin"
```

3. 新建Main.go

```go
package main

import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()
	r.GET("/", func(c *gin.Context) {
		c.String(200, "value %v", "hello gin")
	})
	r.Run()
  r.Run(":9000")//若改变端口
}
```

4. Gin，启动！

```bash
go run main.go
```

## **golang** 程序的热加载

所谓热加载就是当我们对代码进行修改时，程序能够自动重新加载并执行，这在我们开发中是非常便利的，可以快速进行代码测试，省去了每次手动重新编译

工具 **1**(推荐):https://github.com/gravityblast/fresh

```bash
go get github.com/pilu/fresh
go run github.com/pilu/fresh
```

工具 2:https://github.com/codegangsta/gin

```bash
go get -u github.com/codegangsta/gin
```

## Gin 框架中的路由

| GET（SELECT）    | 从服务器取出资源（一项或多项）                 |
| ---------------- | ---------------------------------------------- |
| POST（CREATE）   | 在服务器新建一个资源                           |
| PUT（UPDATE）    | 在服务器更新资源（客户端提供改变后的完整资源） |
| DELETE（DELETE） | 从服务器删除资源                               |

c.String() c.JSON() c.JSONP() c.HTML()

GET POST PUT

例子

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

type Article struct {
	Title string `json:"title"`
}

func main() {
	r := gin.Default()
	r.GET("/", func(c *gin.Context) {
		c.String(http.StatusOK, "value %v", "hello gin!!")
	})
	r.POST("/add", func(c *gin.Context) {
		c.String(200, "post request")
	})
	r.PUT("/edit", func(c *gin.Context) {
		c.String(200, "put 1request")
	})
	r.GET("/json", func(c *gin.Context) {
		c.JSONP(http.StatusOK, gin.H{
			"success": true,
			"msg":     "hello gin",
		})
	})
	r.GET("/jsonp", func(c *gin.Context) {
		a := Article{"jsonp"}
		c.JSONP(http.StatusOK, a)
	})
	err := r.Run("127.0.0.1:8080")
	if err != nil {
		return
	}

}
```

## Gin HTML 模板渲染

### 模板放在不同目录里面的配置方法

Gin 框架中如果不同目录下面有同名模板的话我们需要给模版起别名

```html
{{ define "admin/index.html" }}
#html内容
{{ end }}
```

在main.go中这样写

```go
r.LoadHTMLGlob("templates/**/*")
```

### gin 模板基本语法

#### {{.}} 输出数据

例子

```html
{{ define "default/index.html" }} <!DOCTYPE html> <html lang="en"> <head>

<meta charset="UTF-8">

<meta http-equiv="X-UA-Compatible" content="IE=edge">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Document</title> </head> <body>

<h1>前台模板</h1>

<h3>{{.title}}</h3>

<h4>{{.user.Name}}</h4> <h4>{{.user.Age}}</h4> </body> </html> {{end}}
```

其中user结构体定义如下

```go
type user struct{
	Age int
	Name string
}
```

#### 注释

可以多行，不能嵌套

```html
{{/* a comment */}}
```

#### 变量

```html
<h4>{{$obj := .title}}</h4>
<h4>{{$obj}}</h4>
```

#### 移除空格

```html
{{- .Name -}}
```

”-“要紧挨着“{{“和“}}”

#### 比较函数

| 符号 | 含义                       |
| ---- | -------------------------- |
| eq   | 如果 arg1 == arg2 则返回真 |
| ne   | 如果 arg1 != arg2 则返回真 |
| lt   | 如果 arg1 < arg2 则返回真  |
| le   | 如果 arg1 <= arg2 则返回真 |
| gt   | 如果 arg1 > arg2 则返回真  |
| ge   | 如果 arg1 >= arg2 则返回真 |

#### 条件判断

例子

```
{{define "default/index.html"}}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h2>{{.title}}</h2>
    

    {{if gt .score 90}}
    <p>excellent</p>
    {{else if gt .score 80}}
    <p>great</p>
    {{else if gt .score 60}}
    <p>pass</p>
    {{else}}
    <p>fail</p>
    {{end}}

</body>
</html>
{{end}}
```

#### range

例子

```go
r.GET("/", func(ctx *gin.Context) {
		ctx.HTML(http.StatusOK, "default/index.html", gin.H{
			"title": "首页",
			"score": 88,
			"hobby": []string{"eat", "sleep", "code"},
      "kong": []string{},
		})
	})
```

```html
<ul>
{{range $key,$value:=.hobby}}
<li>{{$key}}:{{$value}}</li>
{{else}}
<li>空</li>
{{end}}
</ul>
<ul>
{{range $key,$value:=.kong}}
<li>{{$key}}:{{$value}}</li>
{{else}}
<li>空</li>
{{end}}
</ul>
```

#### with

```html
{{with .news}}
<!-- 相当于.news.Title -->
<p>{{.Title}}</p>
<!-- 相当于.news.Content -->
<p>{{.Content}}</p>
{{end}}
```

#### 预定义函数

执行模板时，函数从两个函数字典中查找：首先是模板函数字典，然后是全局函数字典。一 般不在模板内定义函数，而是使用 Funcs 方法添加函数到模板里。

预定义的全局函数如下：

| 名称     | 功能                                                         |
| -------- | ------------------------------------------------------------ |
| and      | 函数返回它的第一个 empty 参数或者最后一个参数； 就是说"and x y"等价于"if x then y else x"；所有参数都会执行； |
| or       | 返回第一个非 empty 参数或者最后一个参数； 亦即"or x y"等价于"if x then x else y"；所有参数都会执行； |
| not      | 返回它的单个参数的布尔值的否定                               |
| len      | 返回它的参数的整数类型长度                                   |
| index    | 执行结果为第一个参数以剩下的参数为索引/键指向的值； 如"index x 1 2 3"返回 x\[1]\[2][3]的值；每个被索引的主体必须是数组、切片或者字典。 |
| print    | 即 fmt.Sprint                                                |
| printf   | 即 fmt.Sprintf                                               |
| println  | 即 fmt.Sprintln                                              |
| html     | 返回与其参数的文本表示形式等效的转义 HTML。 这个函数在 html/template 中不可用。 |
| urlquery | 以适合嵌入到网址查询中的形式返回其参数的文本表示的转义值。 这个函数在 html/template 中不可用。 |
| js       | 返回与其参数的文本表示形式等效的转义 JavaScript。            |
| call     | 执行结果是调用第一个参数的返回值，该参数必须是函数类型，其余参数作为调用该函 数的参数； 如"call .X.Y 1 2"等价于 go 语言里的 dot.X.Y(1, 2)； 其中 Y 是函数类型的字段或者字典的值，或者其他类似情况； call 的第一个参数的执行结果必须是函数类型的值（和预定义函数如 print 明显不同）； 该函数类型值必须有 1 到 2 个返回值，如果有 2 个则后一个必须是 error 接口类型； 如果有 2 个返回值的方法返回的 error 非 nil，模板执行会中断并返回给调用模板执行者 该错误； |

#### 自定义模板函数

main.go中：

在`LoadHTMLGlob`之前`SetFuncMap`，添加自定义的模版函数

`SetFuncMap`就是设置了一个Map

```go
r := gin.Default()
r.SetFuncMap(template.FuncMap{
  "UnixToTime": UnixToTime,
})
r.LoadHTMLGlob("templates/*/**")
```

实现函数

```go
func UnixToTime(timestamp int64) string {
	t := time.Unix(timestamp, 0)
	fmt.Println(t)
	return t.Format("2006-01-02 15:04:05")
}
```

模版中：

调用函数

函数名 参数1 参数2……

```
<p>{{UnixToTime .date}}</p>
```

### 嵌套 template

新建public/header.html

```html
{{define "public/header"}}
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>public header</title>
    <style>
        h1 {
            background: #000;
            color: #fff;
            text-align: center;
        }
    </style>
</head>

<body>
    <h1>public header {{.title}}</h1>
</body>

</html>
{{end}}
```

在其他模版内引入

```html
{{template "public/header" .}}
```

注意加上最后的“.”

## 静态文件服务

当我们渲染的 HTML 文件中引用了静态文件时,我们需要配置静态 web 服务

r.Static("/static", "./static") 前面的/static 表示路由 后面的./static 表示路径

若css放在/static/css下，则在html中这样引入

```html
<link rel="stylesheet" href="/static/css/base.css">
```

## 路由详解

### GET POST 以及获取 Get Post 传值

#### Get 请求传值

```go
r.GET("/", func(c *gin.Context) {
  username := c.Query("username")
  age := c.Query("age")
  page := c.DefaultQuery("page", "1")

  c.JSON(http.StatusOK, gin.H{
    "username": username,
    "age":      age,
    "page":     page,
  })
})
```

此时的GET请求应该如下：

```txt
GET http://127.0.0.1:8080?username=kamisatoayaka&age=18
```

#### Post 请求传值 获取 form 表单数据

前台：

```html
<!-- 相当于给模板定义一个名字 define end 成对出现-->
{{ define "default/user.html" }}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="static/css/base.css">
</head>
<body>
    <form action="/doAddUser1" method="post">
        
        用户名:<input type="text" name="username" /> <br><br>
        密码:<input type="password" name="password" /> <br><br>      

        <input type="submit" value="提交">
    </form>
</body>
</html>

{{end}}
```

后台：

```go
//post演示
r.GET("/user", func(c *gin.Context) {
  c.HTML(http.StatusOK, "default/user.html", gin.H{})
})
//获取表单post过来的数据
r.POST("/doAddUser1", func(c *gin.Context) {
  username := c.PostForm("username")
  password := c.PostForm("password")
  age := c.DefaultPostForm("age", "20")

  c.JSON(http.StatusOK, gin.H{
    "username": username,
    "password": password,
    "age":      age,
  })
})
```

#### 获取 GET POST 传递的数据绑定到结构体

定义结构体，添加form标签

json标签的作用是解析的时候把json字段名改成小写

```go
type UserInfo struct {
	Username string `json:"username" form:"username"`
	Password string `json:"password" form:"password"`
}
```

GET

声明为结构体

传的时候用它的指针！！！

别他妈写出什么user:=&UserInfo{}然后传&user了，你传牛魔呢

或者干脆用user:=new(UserInfo)

直接传user

浪费老子一个早上看你那💩代码

```go
r.GET("/getUser", func(c *gin.Context) {
  user := UserInfo{}
  if err := c.ShouldBind(&user); err == nil {
    fmt.Printf("%#v", user)
    c.JSON(http.StatusOK, user)
  } else {
    c.JSON(http.StatusOK, gin.H{
      "err": err.Error(),
    })
  }
})
```

POST

```go
r.POST("/doAddUser2", func(c *gin.Context) {
  user := UserInfo{}
  if err := c.ShouldBind(&user); err == nil {
    c.JSON(http.StatusOK, user)
  } else {
    c.JSON(http.StatusBadRequest, gin.H{
      "err": err.Error(),
    })
  }
})
```

#### 获取 Post Xml 数据

```go
r.POST("/xml", func(c *gin.Context) {
  article := Article{}

  xmlSliceData, _ := c.GetRawData() //获取 c.Request.Body 读取请求数据

  fmt.Println(xmlSliceData)

  if err := xml.Unmarshal(xmlSliceData, &article); err == nil {
    c.JSON(http.StatusOK, article)
  } else {
    c.JSON(http.StatusBadRequest, gin.H{
      "err": err.Error(),
    })
  }

})
```

#### 动态路由

```go
r.GET("/list/:cid", func(c *gin.Context) {

  cid := c.Param("cid")
  c.String(200, "%v", cid)

})
```

### 路由分组

在同文件下分组

```go
func main() { router := gin.Default()

// 简单的路由组: v1 
  v1 := router.Group("/v1") {

  v1.POST("/login", loginEndpoint)

  v1.POST("/submit", submitEndpoint)

  v1.POST("/read", readEndpoint) }

// 简单的路由组: v2 
  v2 := router.Group("/v2") {

  v2.POST("/login", loginEndpoint)

  v2.POST("/submit", submitEndpoint)

  v2.POST("/read", readEndpoint) }

  router.Run(":8080")

}
```

拆分到不同文件

新建 routes 文件夹，routes 文件下面新建 adminRoutes.go、apiRoutes.go、defaultRoutes.go

在main.go中，导入routers包

```go
routers.AdminRoutersInit(r)
routers.ApiRoutersInit(r)
routers.DefaultRoutersInit(r)
```

然后在各自的xxx.go下配置路由即可

## Gin 中自定义控制器

新建controllers文件夹，在其下建立对应的控制器，以admin为例

新建admin文件夹，在其中建立userController.go

```go
package admin

import "github.com/gin-gonic/gin"

type UserController struct{}

func (con UserController) Index(c *gin.Context) {
	c.String(200, "用户列表")
}

func (con UserController) Add(c *gin.Context) {
	c.String(200, "add 用户列表")
}
```

之所以建立结构体是为了方便继承

然后在对应的router中使用即可

```go
package routers

import (
	"demo4/controllers/admin"

	"github.com/gin-gonic/gin"
)

func AdminRoutersInit(r *gin.Engine) {
	adminRouters := r.Group("/admin")
	{
		adminRouters.GET("/", func(c *gin.Context) {
			c.String(200, "后台首页")
		})
		adminRouters.GET("/user", admin.UserController{}.Index)
		adminRouters.GET("/user/add", admin.UserController{}.Add)
		adminRouters.GET("/article", func(c *gin.Context) {
			c.String(200, "新闻列表")
		})
	}
}
```

继承

新建 controller/admin/BaseController.go

```go
package admin import (

  "net/http"

  "github.com/gin-gonic/gin"
) 

type BaseController struct { } 
func (c BaseController) Success(ctx *gin.Context) {
  ctx.String(http.StatusOK, "成功") 
} 
func (c BaseController) Error(ctx *gin.Context) {
  ctx.String(http.StatusOK, "失败") 
}
```

可以让 UserController继承BaseController

```go
type UserController struct{
	BaseController
}
```

然后直接调用BaseController的方法

## Gin 中间件

### next

先跳转到后面的剩余处理程序，再回来继续执行

```go
func initMiddleware(c *gin.Context) {
	start := time.Now().UnixNano()
	fmt.Println("1-我是一个中间件")
	//调用该请求的剩余处理程序
	c.Next()

	fmt.Println("2-我是一个中间件")
	end := time.Now().UnixNano()

	fmt.Println(end - start)
}
```

### Abort

终止调用请求的剩余处理程序

```go
func initMiddleware(c *gin.Context) {
	start := time.Now().UnixNano()
	fmt.Println("1-我是一个中间件")
	//调用该请求的剩余处理程序
	c.Abort()

	fmt.Println("2-我是一个中间件")
	end := time.Now().UnixNano()

	fmt.Println(end - start)
}
```

一个路由可以添加多个中间件

```go
r.GET("/login", initMiddleware, initMiddleware2, func(c *gin.Context) {
	c.String(200, "login")
})
```

### 全局中间件

在main函数中添加：

```go
r.Use(func1,func2,...)
```

### 分组路由中间件

法1:

```go
adminRouters:=r.Group("/admin",func)
```

法2:

```go
adminRouters.Use(func)
```

### 中间件传值

```go
ctx.Set("keyName","value")
key,_=ctx.Get("keyName") //key是空接口类型
```

## Model

就是把一个常用的功能，放到一个模块里，中间件/控制器/main都可以使用该功能。

例如把时间转换放到一个model里。

## 文件上传

html模版：

```html
<body>
    <h2>演示文件上传</h2>

    <form action="/admin/user/doUpload" method="post" enctype="multipart/form-data">
        
        用户名:<input type="text" name="username" placeholder="用户名" />
        <br>
        <br>
        头 像<input type="file" name="face" />
        <br>    <br>
				头 像2<input type="file" name="face2" />
        <br>    <br>
      	头 像2<input type="file" name="face[]" />
        <br>    <br>
        <input type="submit" value="提交">
    </form>
</body>
```

Controller：

```go
func (con UserController) DoUpload(c *gin.Context) {
	username := c.PostForm("username")

	file, err := c.FormFile("face")
	file2, err := c.FormFile("face2")
  file,err:= c.FormFile("face[]")
  
  for _,file:=range file{
    dst:=path.Join("./static/upload",file.Filename)
    c.SaveUploadedFile(file,dst)
  }
  
	// file.Filename 获取文件名称  aaa.jpg   ./static/upload/aaa.jpg
	dst := path.Join("./static/upload", file.Filename)
	if err == nil {
		c.SaveUploadedFile(file, dst)
	}
	// c.String(200, "执行上传")
  dst2 := path.Join("./static/upload", file2.Filename)
	if err == nil {
		c.SaveUploadedFile(file2, dst2)
	}
  
	c.JSON(http.StatusOK, gin.H{
		"success":  true,
		"username": username,
		"dst":      dst,
    "dst2": dst2
	})
}
```

## 按日期存储文件

1. 获取上传文件
2. 判断后缀是否合法
3. 创建保存目录
4. 生成文件名和保存的目录
5. 执行上传

```
func (c UserController) DoAdd(ctx *gin.Context) {
	username := ctx.PostForm("username")
	// 1、获取上传的文件
	file, err1 := ctx.FormFile("face")
	if err1 == nil {
		// 2、获取后缀名 判断类型是否正确 .jpg .png .gif .jpeg
		extName := path.Ext(file.Filename)
		allowExtMap := map[string]bool{".jpg": true, ".png": true, ".gif": true, ".jpeg": true}
		if _, ok := allowExtMap[extName]; !ok {
			ctx.String(200, "文件类型不合法")
			return
		}
		// 3、创建图片保存目录 static/upload/20200623
		day := models.GetDay()
		dir := "./static/upload/" + day
		if err := os.MkdirAll(dir, 0666); err != nil {
			log.Error(err)
		}
		// 4、生成文件名称 144325235235.png
		fileUnixName := strconv.FormatInt(models.GetUnix(), 10)
		// static/upload/20200623/144325235235.png
		saveDir := path.Join(dir, fileUnixName+extName)
		ctx.SaveUploadedFile(file, saveDir)
	}
	ctx.JSON(http.StatusOK, gin.H{"message": "文件上传成功", "username": username})
	// ctx.String(200, username)
} 
```

## Cookie

### SetCookie

```go
c.SetCookie(name, value string, maxAge int, path, domain string, secure, httpOnly bool)
```

第一个参数 key

第二个参数 value

第三个参数 过期时间.如果只想设置 Cookie 的保存路径而不想设置存活时间，可以在第三个参数中传递 nil

第四个参数 cookie 的路径

第五个参数 cookie 的路径 Domain 作用域 本地调试配置成 localhost , 正式上线配置成域名

第六个参数是 secure ，当 secure 值为 true 时，cookie 在 HTTP 中是无效，在 HTTPS 中才有效

第七个参数 httpOnly，是微软对 COOKIE 做的扩展。如果在 COOKIE 中设置了“httpOnly”属性，

则通过程序（JS 脚本、applet 等）将无法读取到 COOKIE 信息，防止 XSS 攻击产生

### Cookie（获取）

```go
cookie, err := c.Cookie("name")
```

## Session

session 是另一种记录客户状态的机制，不同的是 Cookie 保存在客户端浏览器中，而 session保存在服务器上。当客户端浏览器第一次访问服务器并发送请求时，服务器端会创建一个 session 对象，生成一个类似于 key,value 的键值对，然后将 value 保存到服务器 将 key(cookie)返回到浏览器(客户)端。浏览器下次访问时会携带 key(cookie)，找到对应的 session(value)。

```go
package main
import ( "github.com/gin-contrib/sessions"
	"github.com/gin-contrib/sessions/cookie"
	"github.com/gin-gonic/gin"
)
func main() {
	r := gin.Default()
	// 创建基于 cookie 的存储引擎，secret11111 参数是用于加密的密钥，可以改成redis等
	store := cookie.NewStore([]byte("secret11111"))
	// 设置 session 中间件，参数 mysession，指的是 session 的名字，也是 cookie 的名字
	// store 是前面创建的存储引擎，我们可以替换成其他存储引擎
	r.Use(sessions.Sessions("mysession", store))
	r.GET("/", func(c *gin.Context) {
		//初始化 session 对象
		session := sessions.Default(c)
		//设置过期时间
		session.Options(sessions.Options{
			MaxAge: 3600 * 6, // 6hrs
		})
		//设置 Session
		session.Set("username", "张三")
		session.Save()
		c.JSON(200, gin.H{"msg": session.Get("username")})
	})
	r.GET("/user", func(c *gin.Context) {
		// 初始化 session 对象
		session := sessions.Default(c)
		// 通过 session.Get 读取 session 值
		username := session.Get("username")
		c.JSON(200, gin.H{"username": username})
	})
	r.Run(":8000")
}
```

## Gorm

### gorm.model

```go
// gorm.Model 定义
type Model struct {
  ID        uint `gorm:"primary_key"`
  CreatedAt time.Time
  UpdatedAt time.Time
  DeletedAt *time.Time
}
```

可以用继承加入到自己的结构体中，也可以不加入

默认用ID作为主键

```go
type User struct {
  gorm.Model
  Name         string
  Age          sql.NullInt64
  Birthday     *time.Time
  Email        string  `gorm:"type:varchar(100);unique_index"`
  Role         string  `gorm:"size:255"` // 设置字段大小为255
  MemberNumber *string `gorm:"unique;not null"` // 设置会员号（member number）唯一并且不为空
  Num          int     `gorm:"AUTO_INCREMENT"` // 设置 num 为自增类型
  Address      string  `gorm:"index:addr"` // 给address字段创建名为addr的索引
  IgnoreMe     int     `gorm:"-"` // 忽略本字段
}

```

### tag

| 结构体标记（Tag） |                           描述                           |
| :---------------: | :------------------------------------------------------: |
|      Column       |                         指定列名                         |
|       Type        |                      指定列数据类型                      |
|       Size        |                  指定列大小, 默认值255                   |
|    PRIMARY_KEY    |                      将列指定为主键                      |
|      UNIQUE       |                      将列指定为唯一                      |
|      DEFAULT      |                       指定列默认值                       |
|     PRECISION     |                        指定列精度                        |
|     NOT NULL      |                    将列指定为非 NULL                     |
|  AUTO_INCREMENT   |                   指定列是否为自增类型                   |
|       INDEX       | 创建具有或不带名称的索引, 如果多个索引同名则创建复合索引 |
|   UNIQUE_INDEX    |         和 `INDEX` 类似，只不过创建的是唯一索引          |
|     EMBEDDED      |                     将结构设置为嵌入                     |
|  EMBEDDED_PREFIX  |                    设置嵌入结构的前缀                    |
|         -         |                        忽略此字段                        |

|        结构体标记（Tag）         |                描述                |
| :------------------------------: | :--------------------------------: |
|            MANY2MANY             |             指定连接表             |
|            FOREIGNKEY            |              设置外键              |
|      ASSOCIATION_FOREIGNKEY      |            设置关联外键            |
|           POLYMORPHIC            |            指定多态类型            |
|        POLYMORPHIC_VALUE         |             指定多态值             |
|       JOINTABLE_FOREIGNKEY       |          指定连接表的外键          |
| ASSOCIATION_JOINTABLE_FOREIGNKEY |        指定连接表的关联外键        |
|        SAVE_ASSOCIATIONS         |    是否自动完成 save 的相关操作    |
|      ASSOCIATION_AUTOUPDATE      |   是否自动完成 update 的相关操作   |
|      ASSOCIATION_AUTOCREATE      |   是否自动完成 create 的相关操作   |
|    ASSOCIATION_SAVE_REFERENCE    | 是否自动完成引用的 save 的相关操作 |
|             PRELOAD              |    是否自动完成预加载的相关操作    |

### 表名

```go
type User struct {} // 默认表名是 `users`

// 将 User 的表名设置为 `profiles`
func (User) TableName() string {
  return "profiles"
}

func (u User) TableName() string {
  if u.Role == "admin" {
    return "admin_users"
  } else {
    return "users"
  }
}

// 禁用默认表名的复数形式，如果置为 true，则 `User` 的默认表名是 `user`
db.SingularTable(true)
```

### 列名

```go
type Animal struct {
  AnimalId    int64     `gorm:"column:beast_id"`         // set column name to `beast_id`
  Birthday    time.Time `gorm:"column:day_of_the_beast"` // set column name to `day_of_the_beast`
  Age         int64     `gorm:"column:age_of_the_beast"` // set column name to `age_of_the_beast`
}
```
