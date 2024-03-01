# MacOS配置Conda

## 安装

### 0. homebrew

直接使用homebrew安装即可，没有homebrew的可以先安装homebrew，因为众所周知的原因，使用国内镜像源

```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

然后按照提示，可以选择中科大的 

### 1. anaconda

```bash
brew install anaconda
```

可能会报错：`curl: (7) Failed to connect to http://raw.githubusercontent.com port 443: Operation timed out`，这是国内网络问题，请自行解决，如果你用黑色小猫咪，可以配置如下环境变量：

```bash
export https_proxy=http://127.0.0.1:7890
export http_proxy=http://127.0.0.1:7890
export all_proxy=socks5://127.0.0.1:7890
```

### 2. 配置环境变量
如果你和我一样是arm的芯片，anaconda应该在`/opt/homebrew/anaconda`

```bash
echo 'export PATH="/opt/homebrew/anaconda3/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile 
```

***注：如果你用zsh，还需要额外两步操作：***

```bash
echo 'export PATH="/opt/homebrew/anaconda3/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

最后通过`conda -V`测试是否正确安装并配置环境变量，正常情况下会输出conda的版本号

## Pycharm配置

1.打开Pycharm-创建New Project -点击Add Interpreter

2.左侧选择conda environment-右侧点击conda executable 栏最右侧的文件夹标识

3.根据Anaconda部分找到的位置，找到conda-点击Open-跳回界面-点击右下角OK

conda应该在`/opt/homebrew/anaconda3/condabin/conda`

## Anaconda虚拟环境

### 一、什么是Anaconda虚拟环境？

在Python开发中，虚拟环境指隔离Python环境的一种方式，使得不同项目所需要的库和版本隔离开来，便于代码管理和移植。

Anaconda虚拟环境是指Anaconda中创建的虚拟Python环境，用于隔离不同项目所需的Python库和版本。

### 二、创建Anaconda虚拟环境

1. 在Anaconda中创建虚拟环境的命令为：

```bash
conda create --name env_name
```

其中，`env_name`为我们需要创建的虚拟环境的名称。我们可以使用以下命令列出我们已有的虚拟环境：

```bash
conda info --envs 或者 conda info -e 或者 conda env list
```

2. 创建虚拟环境并指定Python版本的命令为：

```bash
conda create --name env_name python=3.7
```

Python版本如果不指定的话，建立的虚拟环境就会和Anaconda使用同一个目录，那么以后安装的所有安装包就会自动安装在Anaconda的安装目录下，而不会安装在用户定义的虚拟环境的目录下。这一点要特别注意

其中，`env_name`为我们需要创建的虚拟环境的名称，`python=3.7`为我们需要使用的Python版本号。

3. 创建包含指定库的虚拟环境的命令为：

```bash
conda create --name env_name pandas numpy matplotlib
```

其中，`env_name`为我们需要创建的虚拟环境的名称，`pandas`、`numpy`、`matplotlib`为我们需要安装在虚拟环境中的Python库。

###  三、使用Anaconda虚拟环境

我们可以通过以下命令激活我们需要使用的虚拟环境：

```bash
conda activate env_name
```

其中，`env_name`为我们需要激活的虚拟环境的名称。

激活成功后，我们可以在终端/命令行工具中看到虚拟环境前缀 `(env_name)`。

当我们需要退出当前虚拟环境时，我们可以使用以下命令：

```bash
conda deactivate
```

### 四、删除Anaconda虚拟环境

我们可以使用以下命令删除我们不需要的虚拟环境：

```bash
conda remove --name env_name --all
```

其中，`env_name`为我们需要删除的虚拟环境的名称。

### 五、修改环境名

1、进入旧环境

```bash
conda activate old_name
```

2、克隆旧环境

```bash
conda create -n new_name --clone old_name
```

3、退出旧环境

```bash
conda deactivate
```

4、删除旧环境

```bash
conda remove -n old_name
```

5、查看最终结果

```bash
conda info --envs
```

### 六、分享环境

1、进入要分享的环境：

```bash
activate target_env_name
```

2、输入命令：

```bash
conda env export > environment.yml
```

会在当前目录下生成environment.yml文件，别人拿到environment.yml文件，在cmd中进入目录文件下可以通过以下命令从该文件创建环境

```bash
conda env create -f environment.yml
```

### 七、安装第三方库

1、查看当前环境下安装的第三方库：

```bash
conda list
```

2、 给当前环境安装第三方库：

```bash
conda install package_name
```

3、给指定环境安装第三方库：

```bash
conda install -n env_name package_name
```

## 参考

https://zhuanlan.zhihu.com/p/640175325

https://www.cnblogs.com/sx66/p/17823608.html

https://blog.csdn.net/young_kp/article/details/119765752