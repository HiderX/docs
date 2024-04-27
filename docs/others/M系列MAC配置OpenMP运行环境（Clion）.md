# M系列MAC配置OpenMP运行环境（Clion）

## 0. 安装Homebrew

直接使用homebrew安装即可，没有homebrew的可以先安装homebrew，因为众所周知的原因，使用国内镜像源

```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

然后按照提示，可以选择中科大的

## 1. 安装gcc和libomp

```bash
brew install gcc
brew install libomp
```

记住你的`gcc`和`libomp`安装路径，如果忘了也没关系，可以通过`brew info gcc`、`brew info libomp`来查看。虽然mac自带clang，但它没有omp。

## 2. Clion配置

先随便新建一个c可执行工程，在`设置-构建、执行、部署-工具链`中修改c和c++编译器为gcc的gcc和g++。

```bash
/opt/homebrew/Cellar/gcc/13.2.0/bin/gcc-13	#我的gcc
/opt/homebrew/Cellar/gcc/13.2.0/bin/g++-13	#我的g++
```

## 3. 修改CmakeLists

```python
cmake_minimum_required(VERSION 3.26)	#保留你的
project(ExOpenMP C)	#保留你的

set(CMAKE_CXX_STANDARD 14)	#保留你的

# 设置OpenMP路径
set(OpenMP_C_FLAGS "-Xpreprocessor -fopenmp -I/usr/local/opt/libomp/include")	#你的libomp/include	如果是按步骤来的，那不需要改
set(OpenMP_C_LIB_NAMES "omp")
set(OpenMP_omp_LIBRARY "/usr/local/opt/libomp/lib/libomp.dylib")	#你的libomp.dylib 如果是按步骤来的，那不需要改

# 设置架构平台，默认的arm会报错
set(CMAKE_OSX_ARCHITECTURES "x86_64")

find_package(OpenMP REQUIRED)

if(OpenMP_C_FOUND)
    #增加编译器的头文件搜索路经
    include_directories(${OpenMP_C_INCLUDE_DIRS})
    #添加可执行文件
    add_executable(main main.c)
    #链接动态库文件到目标可执行文件中
    target_link_libraries(main PUBLIC OpenMP::OpenMP_C)
endif()
```

## 4. 测试

如果你的配置没问题，那么应该已经可以跑起来了，可以用以下代码测试一下

```c
#include <omp.h>
#include <stdio.h>
int main(int argc, char* argv[]){
    int nthreads, tid;
    int nprocs;
    /* Fork一组线程*/
#pragma omp parallel private(nthreads, tid)
    {
        tid = omp_get_thread_num();  /*获得线程id*/
        printf("Hello World from OMP thread %d\n", tid);
        /*主线程工作*/
        if (tid==0) {
            nthreads = omp_get_num_threads(); /*获得线程数量*/
            printf("Number of threads %d\n", nthreads);
        }
    }
    return 0;
}
```

## 5. Clion标黄

通过点击右下的`.clang-tidy`编辑该文件，将其中`openmp-use-default-none`注释掉即可