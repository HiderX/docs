---
date: 2024-07-03
title: 使用Github Action自动化打包构建部署Go程序
weight: 10
---

## Dockerfile

首先在项目根目录创建`Dockerfile`文件，以下是一个样例：

```dockerfile
# 使用官方的 Golang 镜像创建构建产物。
FROM golang:1.21.6 AS builder

RUN mkdir /app
# 将本地代码复制到容器镜像中。
WORKDIR /app
COPY . .

# 在容器内构建命令。
RUN go mod download && \
    CGO_ENABLED=0 GOOS=linux go build -o dbdemo .

# 使用一个新的阶段创建一个最小的镜像。
FROM alpine:3.20
COPY ./conf /conf
COPY --from=builder /app/dbdemo /usr/local/bin/dbdemo
# 更新文件权限以确保它是可执行的。
RUN chmod +x /usr/local/bin/dbdemo
# 设置容器的默认端口
EXPOSE 3000

# 设置容器的默认命令。
CMD ["/usr/local/bin/dbdemo"]
```

> [!NOTE] 
>
> 如果有静态文件，需要在二次创建时复制进去

说明：

`dbdemo`：我的镜像的名字，需要修改成你自己的

`EXPOSE 3000`：容器的端口号，改成你的服务端端口号

## Github Action

在根目录创建`.github/workflows/xxx.yml`，yml的名字自己取，以下是一个样例：

```yml
name: CI	#名字随意

on:
  push:
    branches:
      - main # 触发工作流的分支

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Build Docker image	#打包镜像
        run: |
          docker build -t username/dbdemo:${{ github.sha }} .
          docker tag username/dbdemo:${{ github.sha }} username/dbdemo:latest

      - name: Login to Docker Hub	#登录Docker Hub
        uses: docker/login-action@v1
        with:
          username: ${{ secrets.DOCKER_HUB_USERNAME }}
          password: ${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}

      - name: Push Docker image to Docker Hub	#推送到Docker Hub
        run: |
          docker push username/dbdemo:latest
          docker push username/dbdemo:${{ github.sha }}

      - name: Deploy to server	#部署到服务器
        uses: appleboy/ssh-action@v0.1.3
        with:
          host: ${{ secrets.SERVER_HOST }}
          username: ${{ secrets.SERVER_USERNAME }}
          password: ${{ secrets.SERVER_PASSWORD }}
          port: ${{ secrets.SERVER_PORT }}
          script: |
            docker pull username/dbdemo:${{ github.sha }}
            docker stop dbdemo || true  
            docker rm dbdemo || true   
            docker run -d --name dbdemo -p 3000:3000 username/dbdemo:${{ github.sha }}
```

说明：

`username`：你的Docker Hub用户名，没有账户的可以去注册一个[Docker Hub](https://hub.docker.com/)账户

`dbdemo`：这是我的镜像名，改成你自己的

`appleboy/ssh-action@v0.1.3`：用于ssh连接服务器，可选，支持多种验证方式，我这里选择的用户名密码，你也可以选择sshkey等方式，参考[官方文档](https://github.com/appleboy/ssh-action)

`secrets.xxx`：需要在Github仓库创建对应的secret，例如`secrets.DOCKER_HUB_USERNAME`就需要创建一个名为`DOCKER_HUB_USERNAME`的secret

## Ngnix

我们可以通过Ngnix进行反代，简化api接口的链接

我这里使用的OpenResty，可以理解为Ngnix的Plus版本

```nginx
location /api {
    proxy_pass http://127.0.0.1:3000; 
    proxy_set_header Host $host; 
    proxy_set_header X-Real-IP $remote_addr; 
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
    proxy_set_header REMOTE-HOST $remote_addr; 
    proxy_set_header Upgrade $http_upgrade; 
    proxy_set_header Connection "upgrade"; 
    proxy_set_header X-Forwarded-Proto $scheme; 
    proxy_http_version 1.1; 
    add_header X-Cache $upstream_cache_status; 
    add_header Strict-Transport-Security "max-age=31536000"; 
    add_header Cache-Control no-cache; 
}
```

反代可以简单地理解为将请求链接进行替换，举个例子：

前台请求的是ip/xxx/api，ngnix会将其转化为127.0.0.1:3000/api

这样我们的服务器就只需要开放443和80端口，而不需要开放3000端口

## Cors

我们还需要注意跨域的问题，关于什么是跨域，可以参考[跨域资源共享 CORS 详解](https://www.ruanyifeng.com/blog/2016/04/cors.html)

我们可以在前端/Nginx/后端任何一个地方配置跨域，注意不要重复配置

我这里选择在后端进行配置，Golang中只需要加入Cors中间件即可：

```go
func Cors() gin.HandlerFunc {
	return cors.New(cors.Config{
		//AllowOrigins:  []string{"*"},
		AllowAllOrigins: true,
		AllowMethods:    []string{"PUT", "PATCH", "GET", "POST", "DELETE", "OPTIONS"},
		AllowHeaders:    []string{"Origin", "Content-Type"},
		ExposeHeaders:   []string{"Content-Length", "Authorization"},
		MaxAge:          12 * time.Hour,
	})
}
```

`AllowOrigins`可以设置允许的来源，`*`表示任意来源

`AllowAllOrigins`的值设置为`true`表示允许任何来源

## Tips

在写Golang程序的时候，注意不要将服务端地址写成`localhost:3000`，不然会导致外部无法访问，Nginx也无法进行代理

应当写成`0.0.0.0:3000`或者`:3000`，表示允许任意ip访问
