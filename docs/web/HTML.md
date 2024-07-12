# HTML

HTML 超文本标记语言——HyperText Markup Language。 

* 超文本：链接

## HTML骨架

* html：整个网页
* head：网页头部，用来存放给浏览器看的信息，例如 CSS，title，meta
* body：网页主体，用来存放给用户看的信息，例如图片、文字

```html
<html>
  <head>
    <title>网页标题</title>
  </head>
  <body>
    网页主体
    <!--我是注释-->
  </body>
</html>
```

在vscode中，可以输入`!`或者`html5`快速生成

## 标签

标记：标签，带尖括号的文本

注意，文本本身也算标签的一部分

```html
<strong>需要加粗的文字<strong>	<!--双标签-->
<br>	<!--单标签-->
<hr>
```

### 标签关系

父子关系（嵌套关系）：子级标签换行且缩进（Tab键）

兄弟关系（并列关系）：兄弟标签换行要对齐

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demo</title>
</head>
```

### 标题标签

一般用在新闻标题、文章标题、网页区域名称、产品名称等等

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>
```

显示特点：

* 文字加粗
* 字号逐渐减小
* 独占一行（换行）

> 经验
>
> 1. h1 标签在一个网页中只能用一次，用来放新闻标题或网页的 logo
> 2. h2 ~ h6 没有使用次数的限制

### 段落标签

一般用在新闻段落、文章段落、产品描述信息等等

```html
<p>段落</p>
<p>段落2</p>
```

显示特点：

* 独占一行
* 段落之间存在间隙

### 换行和水平线

* 换行：br
* 水平线：hr

```html
<br>
<hr>
```

### 文本格式化标签

|  标签名  |  效果  |
| :------: | :----: |
| strong/b |  加粗  |
|   em/i   |  倾斜  |
|  ins/u   | 下划线 |
|  del/s   | 删除线 |

一般用strong、em、ins、del

### 图像标签

```html
<img src="url" alt="Pulpit rock" title="xxx" width="304" height="228">
```

- src

  `src`用于指定图像的位置和名称，是 `<img>`的必须**属性**，url可以是相对路径、绝对路径、在线网址

- alt

  图片无法显示时显示替换文本`alt`，对于图像和图像热点是必须的。它只能用在img、area和input元素中。对于input元素，`alt`属性意在用来替换提交按钮的图片。比如：

  ```html
  <input type="image" src="image.gif" alt="Submit" />
  ```

- title

  鼠标悬停在图片上显示`title`，`title`可以使用的地方比`alt`多得多，`title`属性可以用在除了base，basefont，head，html，meta，param，script和title之外的所有标签，但是并不是必须的。

- width/height

  如果只写`width`或者`height`，默认是等比例缩放

### 超链接标签

作用：点击跳转到其他页面。 

```html
<a href="https://www.baidu.com">跳转到百度</a>
```

**href 属性值是跳转地址，是超链接的必须属性。**

超链接默认是在当前窗口跳转页面，添加 **target="_blank"** 实现**新窗口**打开页面。

拓展：开发初期，不确定跳转地址，则 href 属性值写为 **#**，表示**空链接**，页面不会跳转，在当前页面刷新一次。

```html
<a href="https://www.baidu.com/">跳转到百度</a>

<!-- 跳转到本地文件：相对路径查找 --> 
<!-- target="_blank" 新窗口跳转页面 --> 
<a href="./01-标签的写法.html" target="_blank">跳转到01-标签的写法</a>

<!-- 开发初期，不知道超链接的跳转地址，href属性值写#，表示空链接，不会跳转 -->
<a href="#">空链接</a>
```

a标签可以嵌套其他标签，下面代码实现了点击图片跳转百度

```html
<a href="https://baidu.com">
    <img src="img/stone2.jpeg" alt="image1" width="1000" >
</a>
```

也可以用其他标签嵌套a标签

```html
<p>百度的链接：<a href="https://baidu.com">点我去百度</a></p>
```

### 音频标签

```html
<!-- 在 HTML5 里面，如果属性名和属性值完全一样，可以简写为一个单词 -->
<audio src="./media/music.mp3" controls loop autoplay></audio>
```

|   属性   |           作用           |
| :------: | :----------------------: |
| autoplay | 自动播放，浏览器一般禁用 |
|   loop   |         循环播放         |
| controls |       显示控制面板       |

### 视频标签

```html
<!-- 在浏览器中，想要自动播放，必须有 muted 属性 -->
<video src="./media/vue.mp4" controls loop muted autoplay></video>
```

## 列表

作用：布局内容排列整齐的区域。

列表分类：无序列表、有序列表、定义列表。

### 无序列表

作用：布局排列整齐的**不需要规定顺序**的区域。

标签：ul 嵌套 li，ul 是无序列表，li 是列表条目。

```html
<ul>
  <li>第一项</li>
  <li>第二项</li>
  <li>第三项</li>
  ……
</ul>
```

> 注意事项：
>
> * ul 标签里面只能包裹 li 标签
> * li 标签里面可以包裹任何内容

### 有序列表

作用：布局排列整齐的**需要规定顺序**的区域。

标签：ol 嵌套 li，ol 是有序列表，li 是列表条目。

```html
<ol>
  <li>第一项</li>
  <li>第二项</li>
  <li>第三项</li>
  ……
</ol>
```

> 注意事项：
>
> * ol 标签里面只能包裹 li 标签
> * li 标签里面可以包裹任何内容

### 定义列表

标签：dl 嵌套 dt 和 dd，dl 是定义列表，dt 是定义列表的标题，dd 是定义列表的描述 / 详情。

```html
<dl>
  <dt>列表标题</dt>
  <dd>列表描述 / 详情</dd>
   ……
</dl>
```

> 注意事项：
>
> * dl 里面只能包含dt 和 dd
> * dt 和 dd 里面可以包含任何内容

## 表格

### 基本使用

标签：table 嵌套 tr，tr 嵌套 td / th。 

> 提示：在网页中，**表格默认没有边框线**，使用 **border 属性**可以为表格添加边框线。 

```html
<table border="1">
  <tr>
    <th>姓名</th>
    <th>语文</th>
    <th>数学</th>
    <th>总分</th>
  </tr>
  <tr>
    <td>张三</td>
    <td>99</td>
    <td>100</td>
    <td>199</td>
  </tr>
  <tr>
    <td>李四</td>
    <td>98</td>
    <td>100</td>
    <td>198</td>
  </tr>
  <tr>
    <td>总结</td>
    <td>全市第一</td>
    <td>全市第一</td>
    <td>全市第一</td>
  </tr>
</table>
```

### 表格结构标签

```html
<table border="1">
  <thead>
    <tr>
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>总分</th>
    </tr>
  </thead> 
  <tbody>
    <tr>
      <td>张三</td>
      <td>99</td>
      <td>100</td>
      <td>199</td>
    </tr>
    <tr>
      <td>李四</td>
      <td>98</td>
      <td>100</td>
      <td>198</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>总结</td>
      <td>全市第一</td>
      <td>全市第一</td>
      <td>全市第一</td>
    </tr>
  </tfoot>
</table>
```

### 合并单元格

```html
<table border="1">
  <thead>
    <tr>
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>总分</th>
    </tr>
  </thead> 
  <tbody>

    <tr>
      <td>张三</td>
      <td>99</td>
      <!--跨行合并-->
      <td rowspan="2">100</td>
      <td>199</td>
    </tr>
    <tr>
      <td>李四</td>
      <td>98</td>
      <td>198</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>总结</td>
      <!--跨列合并-->
      <td colspan="3">全市第一</td>
    </tr>
  </tfoot>
</table>
```

>注意：不能跨表格结构标签合并单元格（thead、tbody、tfoot）

## 表单

作用：收集用户信息。

使用场景：

* 登录页面
* 注册页面
* 搜索区域

### input 标签

input 标签 type 属性值不同，则功能不同。 

```html
<input type="..." >
```

| type属性值 |           说明           |
| :--------: | :----------------------: |
|    text    | 文本框，用于输入单行文本 |
|  password  |          密码框          |
|   radio    |          单选框          |
|  checkbox  |          多选框          |
|    file    |         上传文件         |

#### input 标签占位文本 

占位文本：提示信息，文本框和密码框都可以使用。 

```html
<input type="..." placeholder="提示信息">
```

#### 单选框

常用属性

| 属性名  | 作用     | 特殊说明                             |
| ------- | -------- | ------------------------------------ |
| name    | 控件名称 | 控件分组，同组只能选中一个(单选功能) |
| checked | 默认选中 | 属性名和属性值相同，简写为一个单词   |

```html
<input type="radio" name="gender" checked> 男
<input type="radio" name="gender"> 女
```

#### 上传文件 

默认情况下，文件上传表单控件只能上传一个文件，添加 multiple 属性可以实现文件多选功能。

```html
<input type="file" multiple>
```

#### 多选框

多选框也叫复选框，默认选中：checked。

```html
<input type="checkbox" checked> 我同意xx条款
```

### 下拉菜单

标签：select 嵌套 option，select 是下拉菜单整体，option是下拉菜单的每一项。

```html
<select>
  <option>北京</option>
  <option>上海</option>
  <option>广州</option>
  <option>深圳</option>
  <option selected>武汉</option>
</select>
```

> 默认显示第一项，**selected** 属性实现**默认选中**功能。

### 文本域

作用：多行输入文本的表单控件。 

```html
<textarea>默认提示文字</textarea>
```

> 注意点：
>
> * 实际开发中，使用 CSS 设置 文本域的尺寸
> * 实际开发中，一般禁用右下角的拖拽功能

### label 标签 

作用：网页中，某个标签的说明文本。

经验：用 label 标签绑定文字和表单控件的关系，增大表单控件的点击范围。 

* 写法一
  * label 标签只包裹内容，不包裹表单控件
  * 设置 label 标签的 for 属性值 和表单控件的 id 属性值相同

```html
<input type="radio" id="man">
<label for="man">男</label>
```

* 写法二：使用 label 标签包裹文字和表单控件，不需要属性 

```html
<label><input type="radio"> 女</label>
```

> 提示：支持 label 标签增大点击范围的表单控件：文本框、密码框、上传文件、单选框、多选框、下拉菜单、文本域等等。 

### 按钮

```html
<button type="">按钮</button>
```

| type属性值 |                      说明                       |
| :--------: | :---------------------------------------------: |
|   submit   |  提交按钮，点击后可以提交数据到后台(默认功能)   |
|   reset    |      重置按钮，点击后将表单控件恢复默认值       |
|   button   | 普通按钮，默认没有功能， 一般配合JavaScript使用 |

```html
<!-- form 表单区域 -->
<!-- action="" 发送数据的地址 -->
<form action="">
  用户名：<input type="text">
  <br><br>
  密码：<input type="password">
  <br><br>

  <!-- 如果省略 type 属性，功能是 提交 -->
  <button type="submit">提交</button>
  <button type="reset">重置</button>
  <button type="button">普通按钮</button>
</form>
```

> 提示：按钮需配合 form 标签（表单区域）才能实现对应的功能。

## 语义化

### 无语义的布局标签 

作用：布局网页（划分网页区域，摆放内容）

* div：独占一行
* span：不换行

```html
<div>div 标签，独占一行</div>
<span>span 标签，不换行</span>
```

### 有语义的布局标签

| 标签名  |    语义    |
| :-----: | :--------: |
| header  |  网页头部  |
|   hav   |  网页导航  |
| footer  |  网页底部  |
|  aside  | 网页侧边栏 |
| section |  网页区块  |
| article |  网页文章  |

## 字符实体

| 显示结果 | 描述   | 实体名称 |
| -------- | ------ | -------- |
|          | 空格   | \&nbsp;  |
| <        | 小于号 | \&lt;    |
| >        | 大于号 | \&gt;    |