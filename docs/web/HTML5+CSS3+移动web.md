# HTML5+CSS3+移动web

## HTML

HTML 超文本标记语言——HyperText Markup Language。 

* 超文本：链接

### HTML骨架

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

### 标签

标记：标签，带尖括号的文本

注意，文本本身也算标签的一部分

```html
<strong>需要加粗的文字<strong>	<!--双标签-->
<br>	<!--单标签-->
<hr>
```

#### 标签关系

父子关系（嵌套关系）：子级标签换行且缩进（Tab键）

兄弟关系（并列关系）：兄弟标签换行要对齐

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demo</title>
</head>
```

#### 标题标签

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

#### 段落标签

一般用在新闻段落、文章段落、产品描述信息等等

```html
<p>段落</p>
<p>段落2</p>
```

显示特点：

* 独占一行
* 段落之间存在间隙

#### 换行和水平线

* 换行：br
* 水平线：hr

```html
<br>
<hr>
```

#### 文本格式化标签

|  标签名  |  效果  |
| :------: | :----: |
| strong/b |  加粗  |
|   em/i   |  倾斜  |
|  ins/u   | 下划线 |
|  del/s   | 删除线 |

一般用strong、em、ins、del

#### 图像标签

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

#### 超链接标签

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

#### 音频标签

```html
<!-- 在 HTML5 里面，如果属性名和属性值完全一样，可以简写为一个单词 -->
<audio src="./media/music.mp3" controls loop autoplay></audio>
```

|   属性   |           作用           |
| :------: | :----------------------: |
| autoplay | 自动播放，浏览器一般禁用 |
|   loop   |         循环播放         |
| controls |       显示控制面板       |

#### 视频标签

```html
<!-- 在浏览器中，想要自动播放，必须有 muted 属性 -->
<video src="./media/vue.mp4" controls loop muted autoplay></video>
```

### 列表

作用：布局内容排列整齐的区域。

列表分类：无序列表、有序列表、定义列表。

#### 无序列表

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

#### 有序列表

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

#### 定义列表

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

### 表格

#### 基本使用

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

#### 表格结构标签

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

#### 合并单元格

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

### 表单

作用：收集用户信息。

使用场景：

* 登录页面
* 注册页面
* 搜索区域

#### input 标签

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

##### input 标签占位文本 

占位文本：提示信息，文本框和密码框都可以使用。 

```html
<input type="..." placeholder="提示信息">
```

##### 单选框

常用属性

| 属性名  | 作用 | 特殊说明                |
| ------- | -------------- | ----------------------------------- |
| name    | 控件名称       | 控件分组，同组只能选中一个(单选功能) |
| checked | 默认选中       | 属性名和属性值相同，简写为一个单词  |

```html
<input type="radio" name="gender" checked> 男
<input type="radio" name="gender"> 女
```

##### 上传文件 

默认情况下，文件上传表单控件只能上传一个文件，添加 multiple 属性可以实现文件多选功能。

```html
<input type="file" multiple>
```

##### 多选框

多选框也叫复选框，默认选中：checked。

```html
<input type="checkbox" checked> 我同意xx条款
```

#### 下拉菜单

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

#### 文本域

作用：多行输入文本的表单控件。 

```html
<textarea>默认提示文字</textarea>
```

> 注意点：
>
> * 实际开发中，使用 CSS 设置 文本域的尺寸
> * 实际开发中，一般禁用右下角的拖拽功能

#### label 标签 

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

#### 按钮

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

### 语义化

#### 无语义的布局标签 

作用：布局网页（划分网页区域，摆放内容）

* div：独占一行
* span：不换行

```html
<div>div 标签，独占一行</div>
<span>span 标签，不换行</span>
```

#### 有语义的布局标签

| 标签名  |    语义    |
| :-----: | :--------: |
| header  |  网页头部  |
|   hav   |  网页导航  |
| footer  |  网页底部  |
|  aside  | 网页侧边栏 |
| section |  网页区块  |
| article |  网页文章  |

### 字符实体

| 显示结果 | 描述   | 实体名称 |
| -------- | ------ | -------- |
|          | 空格   | \&nbsp;  |
| <        | 小于号 | \&lt;    |
| >        | 大于号 | \&gt;    |

## CSS

层叠样式表 (Cascading Style Sheets，缩写为 CSS），是一种 **样式表** 语言，用来**描述 HTML 文档的呈现**（**美化内容**）。

书写位置：**title 标签下方添加 style 双标签，style 标签里面书写 CSS 代码**。

```html
<title>CSS 初体验</title>
<style>
  /* 选择器 { } */
  p {
    /* CSS 属性 */
    color: red;
  }
</style>

<p>体验 CSS</p>
```

> 提示：属性名和属性值成对出现 → 键值对。 

### CSS引入方式

* **内部**样式表：学习使用
  * CSS 代码写在 style 标签里面
* **外部**样式表：开发使用
  * CSS 代码写在单独的 CSS 文件中（**.css**）
  * 在 HTML 使用 link 标签引入

```html
<link rel="stylesheet" href="./my.css">
```

* **行内**样式：配合 JavaScript 使用
  * CSS 写在标签的 style 属性值里

```html
<div style="color: red; font-size:20px;">这是 div 标签</div>
```

### 选择器

作用：**查找标签**，设置样式。 

#### 标签选择器

标签选择器：使用**标签名**作为选择器 → 选中**同名标签设置相同的样式**。

例如：p, h1, div, a, img......

```html
<style>
  p {
    color: red;
  }
</style>
```

> 注意：标签选择器**无法差异化**同名标签的显示效果。

#### 类选择器

作用：查找标签，**差异化**设置标签的显示效果。

步骤：

* 定义类选择器 → **.类名**
* 使用类选择器 → 标签添加 **class="类名"**

```html
<style>
  /* 定义类选择器 */
  .red {
    color: red;
  }
</style>

<!-- 使用类选择器 -->
<div class="red">这是 div 标签</div>
<div class="red size">div 标签</div>
```

注意：

* 类名**自定义**，不要用纯数字或中文，尽量用英文命名
* 一个类选择器**可以供多个标签使用**
* **一个标签可以使用多个类名**，类名之间用**空格**隔开

> 开发习惯：类名见名知意，多个单词可以用 - 连接，例如：news-hd。

#### id选择器

作用：查找标签，差异化设置标签的显示效果。

场景：id 选择器一般**配合 JavaScript** 使用，很少用来设置 CSS 样式

步骤：

* 定义 id 选择器 → #id名
* 使用 id 选择器 → 标签添加 id= "id名"

```html
<style>
  /* 定义 id 选择器 */
  #red {
    color: red;
  }
</style>

<!-- 使用 id 选择器 -->
<div id="red">这是 div 标签</div>
```

> 规则：同一个ID选择器在CSS样式设置时，可以被多次使用，但在实际开发中，用到javaScript技术时，就不能在页面中多次使用同一个id。

#### 通配符选择器

作用：查找页面**所有**标签，设置相同样式。

通配符选择器： ***，不需要调用**，浏览器自动查找页面所有标签，设置相同的样式

```css
* {
  color: red;
}
```

> 经验：通配符选择器可以用于**清除标签的默认样式**，例如：标签默认的外边距、内边距。

#### 结构伪类选择器 

作用：根据元素的**结构关系**查找元素。

|     选择器     |               说明               |
| :------------: | :------------------------------: |
| E:first-child  |         查找第一个E元素          |
|  E:last-child  |        查找最后一个E元素         |
| E:nth-child(N) | 查找第N个E元素(第一个元素N值为1) |

```css
li:first-child {
  background-color: green;
}
```

**:nth-child(公式)** 

|        功能         |     公式      |
| :-----------------: | :-----------: |
|      偶数标签       |    2n;even    |
|      奇数标签       | 2n+1;2n-1;odd |
|  找到5的倍数的标签  |      5n       |
| 找到第5个以后的标签 |      n+5      |
| 找到第5个以前的标签 |     -n+5      |

> 提示：公式中的n取值从 **0** 开始。 

#### 伪元素选择器 

作用：创建**虚拟元素**（伪元素），用来**摆放装饰性的内容**。 

|  选择器   |              说明               |
| :-------: | :-----------------------------: |
| E::before | 在E元素里面最前面添加一个伪元素 |
| E::after  | 在E元素里面最后面添加一个伪元素 |

```css
div::before {
  content: "before 伪元素";
}
div::after {
  content: "after 伪元素";
}
```

注意点：

* 必须设置 **content: ""属性**，用来 设置伪元素的内容，如果没有内容，则**引号留空**即可
* 伪元素默认是**行内**显示模式
* **权重和标签选择器相同**

#### 优先级

如下代码的结果是？

```html
<style>
  p{
    color: red;
    font-size: xx-large;
  }
  #q{
    color: green;
  }
  .t1{
    color: blue;
    text-align: center;
  }
  *{
    color: orange;
  }
</style>

<p>dsfsfsfads</p>
<p class="t1">dsfsfsfads</p>
<p class="t1" id="q">dsfsfsfads</p>
<p id="q">sss</p>
<h2>11</h2>
```

> ID选择器>类选择器>标签选择器>通配符选择器

### 文字控制属性

#### 字体大小

* 属性名：**font-size**
* 属性值：文字尺寸，PC 端网页最常用的单位 **px**

```css
p {
  font-size: 30px;
}
```

> 经验：谷歌浏览器默认字号是16px。

#### 字体样式（是否倾斜） 

作用：清除文字默认的倾斜效果

属性名：**font-style**

属性值

* 正常（不倾斜）：**normal** 
* 倾斜：**italic**

#### 字体加粗

```css
.div1{
  font-weight:400;	 /*400=normal*/
}
.div2{
  font-weight:700;	/*700=bold*/
}
```

#### 行高

作用：设置多行文本的间距

属性名：line-height

属性值

* 数字 + px
* 数字（当前标签font-size属性值的倍数）

```css
line-height: 30px;


/* 当前标签字体大小为16px */
line-height: 2;
```

> 行高的测量方法：从一行文字的最顶端（最底端）量到下一行文字的最顶端（最底端）。 

#### 单行文字垂直居中

垂直居中技巧：**行高属性值等于盒子高度属性值**

注意：该技巧适用于单行文字垂直居中效果

```css
div {
  height: 100px;
  background-color: skyblue;

  /* 注意：只能是单行文字垂直居中 */
  line-height: 100px;
}
```

#### 字体族

属性名：**font-family**

属性值：字体名

```css
font-family: 楷体;
```

> 拓展（了解）：font-family属性值可以书写多个字体名，各个字体名用逗号隔开，执行顺序是从左向右依次查找
>
> *  font-family 属性最后设置一个字体族名，网页开发建议使用无衬线字体

```css
font-family: Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53", sans-serif;
```

#### font复合属性

复合属性：属性的简写方式，**一个属性对应多个值的写法**，各个属性值之间用**空格**隔开。

**font: 是否倾斜  是否加粗  字号/行高 字体（必须按顺序书写）**

```css
div {
  font: italic 700 30px/2 楷体;
}
```

> 注意：字号和字体值必须书写，否则 font 属性不生效 

#### 文本缩进 

属性名：**text-indent**

属性值：

* 数字 + px
* **数字 + em**（推荐：**1em = 当前标签的字号大小**）

```css
p {
  text-indent: 2em;
}
```

#### 文本对齐方式 

作用：控制内容水平对齐方式

属性名：**text-align**

```css
text-align : center;	/*left、center、right*/
```

> text-align本质是控制内容的对齐方式，属性要设置给内容的父级。 

```html
<style>
  div {
    text-align: center;
  }
</style>
<div>
  <!--控制图片对齐-->
  <img src="../0/img/stone2.jpeg" width="1000px">
</div>
```

#### 文本修饰线 

属性名： **text-decoration** 

|    属性值    |  效果  |
| :----------: | :----: |
|     none     |   无   |
|  underline   | 下划线 |
| line-through | 删除线 |
|   overline   | 上划线 |

#### 文字颜色

|  颜色表示方式  |    属性值     |                说明                |        使用场景        |
| :------------: | :-----------: | :--------------------------------: | :--------------------: |
|   颜色关键字   | 颜色英文单词  |         red、green、blue…          |        学习测试        |
|   rgb表示法    |   rgb(r,g,b   | r,g,b表示红绿蓝三原色，取值：0-255 |          了解          |
|   rgba表示法   | rgba(r,g,b,a) |     a表示透明度，  取 值 ：0-1     |  开发使用，实现透明色  |
| 十六进制表示法 |    #RRGGBB    |  #000000,#ffcc00,简写：#000,#fcO   | 开发使用(从设计稿复制) |

### 复合选择器

定义：由两个或多个基础选择器，通过不同的方式组合而成。

作用：更准确、更高效的选择目标元素（标签）。

#### 后代选择器

后代选择器：**选中某元素的后代元素**。

选择器写法：父选择器  子选择器 { CSS 属性}，父子选择器之间用**空格**隔开。

后代选择器会对所有后代生效，包括儿子、孙子、重孙子……

```html
<style>
  div span {
    color: red;
  }
</style>
<span> span 标签</span>
<div>
  <span>这是 div 的儿子 span</span >
  <p>
    <span>这是孙子</span>
  </p>
</div>
```

#### 子代选择器

子代选择器：选中某元素的子代元素（**最近的子级**）。

选择器写法：父选择器 > 子选择器 { CSS 属性}，父子选择器之间用 **>** 隔开。

```html
<style>
  div > span {
    color: red;
  }
</style>

<div>
  <span>这是 div 里面的 span</span>
  <p>
    <span>这是 div 里面的 p 里面的 span</span>
  </p>
</div>

```

#### 并集选择器

并集选择器：选中**多组标签**设置**相同**的样式。

选择器写法：选择器1, 选择器2, …, 选择器N { CSS 属性}，选择器之间用 **,** 隔开。

```html
<style>
  div,
  p,
  span {
    color: red;
  }
</style>

<div> div 标签</div>
<p>p 标签</p>
<span>span 标签</span>
```

#### 交集选择器 

交集选择器：选中**同时满足多个条件**的元素。

选择器写法：选择器1选择器2 { CSS 属性}，选择器之间连写，没有任何符号。 

```html
<style>
  p.box#hhh {
  color: red;
}
</style>

<p class="box" id="hhh">p 标签，使用了类选择器 box</p>
<p>p 标签</p>
<div class="box">div 标签，使用了类选择器 box</div>
```

> 注意：如果交集选择器中有标签选择器，标签选择器必须书写在最前面。 

#### 伪类选择器 

伪类选择器：伪类表示元素**状态**，选中元素的某个状态设置样式。

鼠标悬停状态：**选择器:hover { CSS 属性 }**

```html
<style>
  a:hover {
    color: red;
  }
  .box:hover {
    color: green;
  }
</style>

<a href="#">a 标签</a>
<div class="box">div 标签</div>
```

|  选择器  |     作用     |
| :------: | :----------: |
|  :link   |    访问前    |
| :visited |    访问后    |
|  :hoyer  |   鼠标悬停   |
| :active  | 点击时(激活) |

> 提示：如果要给超链接设置以上四个状态，需要按 LVHA 的顺序书写。 
>
> 经验：工作中，一个 a 标签选择器设置超链接的样式， hover状态特殊设置 

### CSS特性

CSS特性：化简代码 / 定位问题，并解决问题

* 继承性
* 层叠性
* 优先级

#### 继承性

继承性：子级默认继承父级的**文字控制属性**。 

> 注意：如果标签有默认文字样式会继承失败。 例如：a 标签的颜色、h1、h2、h3、h4、h5、h6的字体大小。

#### 层叠性

特点：

* 相同的属性会覆盖：**后面的 CSS 属性覆盖前面的 CSS 属性**
* 不同的属性会叠加：**不同的 CSS 属性都生效**

```html
<style>
  div {
    color: red;
    font-weight: 700;
  }
  div {
    color: green;
    font-size: 30px;
  }
</style>

<div>div 标签</div>
```

> 注意：选择器类型相同则遵循层叠性，否则按选择器优先级判断。 

#### 优先级

优先级：也叫权重，当一个标签**使用了多种选择器时**，基于不同种类的选择器的**匹配规则**。

```html
<style>
  div {
    color: red;
  }
  .box {
    color: green;
  }
</style>

<div class="box">div 标签</div>
```

##### 基础选择器

规则：选择器**优先级高的样式生效**。

公式：**通配符选择器 < 标签选择器 < 类选择器 < id选择器 < 行内样式 < !important**

​           **（选中标签的范围越大，优先级越低）**

##### 复合选择器-叠加

叠加计算：如果是复合选择器，则需要**权重叠加**计算。

公式：（每一级之间不存在进位）

(行内样式，id选择器个数，类选择器个数，标签选择器个数)

规则：

* 从左向右依次比较选个数，同一级个数多的优先级高，如果个数相同，则向后比较
* **!important 权重最高**
* 继承权重最低

### Emmet 写法

Emmet写法：代码的**简写**方式，输入缩写 VS Code 会自动生成对应的代码。 

* HTML标签

|     说明     |                   标签结构                    |    Emmet    |
| :----------: | :-------------------------------------------: | :---------: |
|   类选择器   |          ` <div class="box"></div>`           | 标签名.类名 |
|   id选择器   |            `<div id="box"></div>`             | 标签名#id名 |
|   同级标签   |             `<div></div><p></p>`              |    div+p    |
|  父子级标签  |             `<div><p></p></div>`              |    div>p    |
| 多个相同标签 | ` <span>1</span><span>2</span><span>3</span>` |   span*3    |
| 有内容的标签 |              ` <div>内容</div>`               |  div{内容)  |

- CSS：大多数简写方式为属性单词的**首字母** 

|   说明    |                      CSS属性                      |     Emmet     |
| :-------: | :-----------------------------------------------: | :-----------: |
|   宽度    |                      `width`                      |       W       |
| 宽度500px |                  `width:500px;`                   |     w500      |
|  背景色   |                `background-color`                 |      bgc      |
| 多个属性  | `width:200px;height:100px;background-color:#fff;` | W200+h100+bgc |

### 背景属性

#### 背景图

网页中，使用背景图实现装饰性的图片效果。

* 属性名：**background-image**（bgi）
* 属性值：url(背景图 URL)

```css
div {
  width: 400px;
  height: 400px;

  background-image: url(./images/1.png);
}
```

> 提示：背景图默认有**平铺（复制）效果**。 

#### 平铺方式

属性名：**background-repeat**（bgr） 

|  属性值   |      效果      |
| :-------: | :------------: |
| no-repeat |     不平铺     |
|  repeat   | 平铺(默认效果) |
| repeat-x  |  水平方向平铺  |
| repeat-y  |  垂直方向平铺  |

```css
div {
  width: 400px;
  height: 400px;
  background-color: pink;
  background-image: url(./images/1.png);

  background-repeat: no-repeat;
}
```

#### 背景图位置

属性名：**background-position**（bgp）

属性值：水平方向位置 垂直方向位置

- 关键字

| 关键字 | 位置 |
| :----: | :--: |
|  eft   | 左侧 |
| right  | 右侧 |
| center | 居中 |
|  top   | 顶部 |
| bottom | 底部 |

坐标

* 水平：正数向右；负数向左
* 垂直：正数向下；负数向上

```css
div {
  width: 400px;
  height: 400px;
  background-color: pink;
  background-image: url(./images/1.png);
  background-repeat: no-repeat;

  background-position: center bottom;
  background-position: 50px -100px;
  background-position: 50px center;
  background-position: center;
  background-position: 50px;
}
```

> 提示：
>
> * 关键字取值方式写法，可以颠倒取值顺序
> * 可以只写一个关键字，另一个方向默认为居中；数字只写一个值表示水平方向，垂直方向为居中

#### 背景图缩放

作用：设置背景图大小

属性名：**background-size**（bgz）

常用属性值：

* 关键字
  *  cover：等比例缩放背景图片以完全覆盖背景区，可能背景图片部分看不见
  * contain：等比例缩放背景图片以完全装入背景区，可能背景区部分空白

* 百分比：根据盒子尺寸计算图片大小
* 数字 + 单位（例如：px）

```css
div {
  width: 500px;
  height: 400px;
  background-color: pink;
  background-image: url(./images/1.png);
  background-repeat: no-repeat;
  
  background-size: cover;
  background-size: contain;
}
```

> 提示：工作中，**图片比例与盒子比例相同**，使用 cover 或 contain 缩放背景图效果相同。

#### 背景图固定

作用：背景不会随着元素的内容滚动。

属性名：**background-attachment**（bga）

属性值：**fixed**

```css
body {
  background-image: url(./images/bg.jpg);
  background-repeat: no-repeat;
  background-attachment: fixed;
}
```

#### 背景复合属性

属性名：**background**（bg）

属性值：背景色 背景图 背景图平铺方式 背景图位置/背景图缩放  背景图固定（**空格隔开各个属性值，不区分顺序**）

```css
div {
  width: 400px;
  height: 400px;

  background: pink url(./images/1.png) no-repeat right center/cover;
}
```

### 显示模式

显示模式：标签（元素）的显示方式。 

作用：布局网页的时候，根据标签的显示模式选择合适的标签摆放内容。 

#### 块级元素

特点：

* 独占一行
* 宽度默认是父级的100%
* 添加宽高属性生效

<div style="background-color:orange;width:100px;height:100px;">div1</div>
<div style="background-color:green;width:100px;height:100px;">div2</div>

#### 行内元素

特点：

* 一行可以显示多个
* 设置宽高属性不生效
* 宽高尺寸由内容撑开

<span style="background-color:orange;width:100px;height:100px">span1</span><span style="background-color:green;width:100px;height:100px">span2</span>

#### 行内块元素 

特点：

* 一行可以显示多个
* 设置宽高属性生效
* 宽高尺寸也可以由内容撑开

#### 转换显示模式

属性：**display**

|    属性值    |  效果  |
| :----------: | :----: |
|    block     |  块级  |
| inline-block | 行内块 |
|    inline    |  行内  |

inline-block:

<div style="background-color:orange;width:100px;height:100px;display:inline-block;">div1</div>
<div style="background-color:green;width:100px;height:100px;display:inline-block">div2</div>

block:

<span style="background-color:orange;width:100px;height:100px;display:block;">span1</span><span style="background-color:green;width:100px;height:100px;display:block;">span2</span> 

### 盒子模型

作用：布局网页，摆放盒子和内容。

#### 组成

* 内容区域 – width & height
* 内边距 – padding（出现在内容与盒子边缘之间）
* 边框线 – border 
* 外边距 – margin（出现在盒子外面）

```css
div {
  margin: 50px;
  border: 5px solid brown;
  padding: 20px;
  width: 200px;
  height: 200px;
  background-color: pink;
}
```

<div style="
  margin: 50px;
  border: 5px solid brown;
  padding: 20px;
  width: 200px;
  height: 200px;
  background-color: pink;">我是div</div>
<div style="
  margin: 50px;
  border: 5px solid green;
  padding: 20px;
  width: 200px;
  height: 200px;
  background-color: yellow;">我是div2</div>

#### 边框线

##### 四个方向

属性名：**border**（bd）

属性值：边框线粗细  线条样式  颜色（不区分顺序）

| 属性值 | 线条样式 |
| :----: | :------: |
| solid  |   实线   |
| dashed |   虚线   |
| dotted |   点线   |

```css
div {
  border: 5px solid brown;
  width: 200px;
  height: 200px;
  background-color: pink;
}
```

##### 单方向边框线 

属性名：**border-方位名词**（bd+方位名词首字母，例如，bdl）

属性值：边框线粗细  线条样式  颜色（不区分顺序）

```css
div {
  border-top: 2px solid red;
  border-right: 3px dashed green;
  border-bottom: 4px dotted blue;
  border-left: 5px solid orange;
  width: 200px;
  height: 200px;
  background-color: pink;
}
```

#### 内边距 

作用：设置 内容 与 盒子边缘 之间的距离。

* 属性名：padding / padding-方位名词

```css
div {
  /* 四个方向 内边距相同 */
  padding: 30px;
  /* 单独设置一个方向内边距 */
  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 40px;
  padding-left: 80px;
  width: 200px;
  height: 200px;
  background-color: pink;
}
```

> 提示：添加 padding 会撑大盒子。

* padding 多值写法

| 取值个数 |             示例             |                含义                 |
| :------: | :--------------------------: | :---------------------------------: |
|  一个值  |        padding:10px;         |       四个方向内边距均为10px        |
|  四个值  | padding:10px 20px 40px 80px; | 上：10px;右：20px;下：40px;左：80px |
|  三个值  |   padding:10px 40px 80px;    |    上：10px;左右：40px;下：80px     |
|  两个值  |      padding:10px 80px;      |        上下：10px;左右：80px        |

> 技巧：从**上**开始**顺时针**赋值，当前方向没有数值则与**对面取值相同**。 

#### 尺寸计算

默认情况：盒子尺寸 = 内容尺寸 + border 尺寸 + 内边距尺寸

结论：给盒子加 border / padding 会撑大盒子

解决：

* 手动做减法，减掉 border / padding 的尺寸
* 內减模式：**box-sizing: border-box**

#### 外边距

作用：拉开两个盒子之间的距离

属性名：**margin**

提示：与 padding 属性值写法、含义相同

margin-left/margin-right/margin-top/margin-bottom

#### 版心居中

左右 margin 值 为 auto（盒子要有宽度）

```css
div {
  margin: 0 auto;
  width: 1000px;
  height: 200px;
  background-color: pink;
}
```

<div style="
        margin: 0 auto;
        width: 500px;
        height: 200px;
        background-color: pink;
      ">div</div>

#### 清除默认样式 

```css
/* 清除默认内外边距 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
/* 清除列表项目符号 */
li {
  list-style: none;
}
```

#### 元素溢出

作用：控制溢出元素的内容的显示方式。

属性名：**overflow**

| 属性值 |                   效果                   |
| :----: | :--------------------------------------: |
| hidden |                 溢出隐藏                 |
| scroll | 溢出滚动(无论是否溢出，都显示滚动条位置) |
|  auto  |      溢出滚动(溢出才显示滚动条位置)      |

hidden:

<div style=" width: 200px;
            height: 200px;
            background-color: pink;
            overflow: hidden;">汉皇重色思倾国，御宇多年求不得。
        杨家有女初长成，养在深闺人未识。
        天生丽质难自弃，一朝选在君王侧。
        回眸一笑百媚生，六宫粉黛无颜色。
        春寒赐浴华清池，温泉水滑洗凝脂。
        侍儿扶起娇无力，始是新承恩泽时。
        云鬓花颜金步摇，芙蓉帐暖度春宵。
        春宵苦短日高起，从此君王不早朝。
        承欢侍宴无闲暇，春从春游夜专夜。
        后宫佳丽三千人，三千宠爱在一身。
        金屋妆成娇侍夜，玉楼宴罢醉和春。
        姊妹弟兄皆列土，可怜光彩生门户。
        遂令天下父母心，不重生男重生女。
        骊宫高处入青云，仙乐风飘处处闻。
        缓歌慢舞凝丝竹，尽日君王看不足。
        渔阳鼙鼓动地来，惊破霓裳羽衣曲。
        九重城阙烟尘生，千乘万骑西南行。
        翠华摇摇行复止，西出都门百余里。
        六军不发无奈何，宛转蛾眉马前死。
        花钿委地无人收，翠翘金雀玉搔头。
        君王掩面救不得，回看血泪相和流。
        黄埃散漫风萧索，云栈萦纡登剑阁。
        峨嵋山下少人行，旌旗无光日色薄。
        蜀江水碧蜀山青，圣主朝朝暮暮情。
        行宫见月伤心色，夜雨闻铃肠断声。
        天旋地转回龙驭，到此踌躇不能去。
        马嵬坡下泥土中，不见玉颜空死处。
        君臣相顾尽沾衣，东望都门信马归。
        归来池苑皆依旧，太液芙蓉未央柳。
        芙蓉如面柳如眉，对此如何不泪垂。
        春风桃李花开夜，秋雨梧桐叶落时。
        西宫南苑多秋草，落叶满阶红不扫。
        梨园弟子白发新，椒房阿监青娥老。
        夕殿萤飞思悄然，孤灯挑尽未成眠。
        迟迟钟鼓初长夜，耿耿星河欲曙天。
        鸳鸯瓦冷霜华重，翡翠衾寒谁与共。
        悠悠生死别经年，魂魄不曾来入梦。
        临邛道士鸿都客，能以精诚致魂魄。
        为感君王辗转思，遂教方士殷勤觅。
        排空驭气奔如电，升天入地求之遍。
        上穷碧落下黄泉，两处茫茫皆不见。
        忽闻海上有仙山，山在虚无缥渺间。
        楼阁玲珑五云起，其中绰约多仙子。
        中有一人字太真，雪肤花貌参差是。
        金阙西厢叩玉扃，转教小玉报双成。
        闻道汉家天子使，九华帐里梦魂惊。
        揽衣推枕起徘徊，珠箔银屏迤逦开。
        云鬓半偏新睡觉，花冠不整下堂来。
        风吹仙袂飘飖举，犹似霓裳羽衣舞。
        玉容寂寞泪阑干，梨花一枝春带雨。
        含情凝睇谢君王，一别音容两渺茫。
        昭阳殿里恩爱绝，蓬莱宫中日月长。
        回头下望人寰处，不见长安见尘雾。
        惟将旧物表深情，钿合金钗寄将去。
        钗留一股合一扇，钗擘黄金合分钿。
        但令心似金钿坚，天上人间会相见。
        临别殷勤重寄词，词中有誓两心知。
        七月七日长生殿，夜半无人私语时。
        在天愿作比翼鸟，在地愿为连理枝。
        天长地久有时尽，此恨绵绵无绝期。</div>

scroll:

<div style=" width: 200px;
            height: 200px;
            background-color: pink;
            overflow: scroll;">汉皇重色思倾国，御宇多年求不得。
        杨家有女初长成，养在深闺人未识。
        天生丽质难自弃，一朝选在君王侧。
        回眸一笑百媚生，六宫粉黛无颜色。
        春寒赐浴华清池，温泉水滑洗凝脂。
        侍儿扶起娇无力，始是新承恩泽时。
        云鬓花颜金步摇，芙蓉帐暖度春宵。
        春宵苦短日高起，从此君王不早朝。
        承欢侍宴无闲暇，春从春游夜专夜。
        后宫佳丽三千人，三千宠爱在一身。
        金屋妆成娇侍夜，玉楼宴罢醉和春。
        姊妹弟兄皆列土，可怜光彩生门户。
        遂令天下父母心，不重生男重生女。
        骊宫高处入青云，仙乐风飘处处闻。
        缓歌慢舞凝丝竹，尽日君王看不足。
        渔阳鼙鼓动地来，惊破霓裳羽衣曲。
        九重城阙烟尘生，千乘万骑西南行。
        翠华摇摇行复止，西出都门百余里。
        六军不发无奈何，宛转蛾眉马前死。
        花钿委地无人收，翠翘金雀玉搔头。
        君王掩面救不得，回看血泪相和流。
        黄埃散漫风萧索，云栈萦纡登剑阁。
        峨嵋山下少人行，旌旗无光日色薄。
        蜀江水碧蜀山青，圣主朝朝暮暮情。
        行宫见月伤心色，夜雨闻铃肠断声。
        天旋地转回龙驭，到此踌躇不能去。
        马嵬坡下泥土中，不见玉颜空死处。
        君臣相顾尽沾衣，东望都门信马归。
        归来池苑皆依旧，太液芙蓉未央柳。
        芙蓉如面柳如眉，对此如何不泪垂。
        春风桃李花开夜，秋雨梧桐叶落时。
        西宫南苑多秋草，落叶满阶红不扫。
        梨园弟子白发新，椒房阿监青娥老。
        夕殿萤飞思悄然，孤灯挑尽未成眠。
        迟迟钟鼓初长夜，耿耿星河欲曙天。
        鸳鸯瓦冷霜华重，翡翠衾寒谁与共。
        悠悠生死别经年，魂魄不曾来入梦。
        临邛道士鸿都客，能以精诚致魂魄。
        为感君王辗转思，遂教方士殷勤觅。
        排空驭气奔如电，升天入地求之遍。
        上穷碧落下黄泉，两处茫茫皆不见。
        忽闻海上有仙山，山在虚无缥渺间。
        楼阁玲珑五云起，其中绰约多仙子。
        中有一人字太真，雪肤花貌参差是。
        金阙西厢叩玉扃，转教小玉报双成。
        闻道汉家天子使，九华帐里梦魂惊。
        揽衣推枕起徘徊，珠箔银屏迤逦开。
        云鬓半偏新睡觉，花冠不整下堂来。
        风吹仙袂飘飖举，犹似霓裳羽衣舞。
        玉容寂寞泪阑干，梨花一枝春带雨。
        含情凝睇谢君王，一别音容两渺茫。
        昭阳殿里恩爱绝，蓬莱宫中日月长。
        回头下望人寰处，不见长安见尘雾。
        惟将旧物表深情，钿合金钗寄将去。
        钗留一股合一扇，钗擘黄金合分钿。
        但令心似金钿坚，天上人间会相见。
        临别殷勤重寄词，词中有誓两心知。
        七月七日长生殿，夜半无人私语时。
        在天愿作比翼鸟，在地愿为连理枝。
        天长地久有时尽，此恨绵绵无绝期。</div>

#### 外边距问题

##### 合并现象

场景：**垂直**排列的兄弟元素，上下 **margin** 会**合并**

现象：取两个 margin 中的**较大值生效**

```css
.one {
  margin-bottom: 50px;
}
.two {
  margin-top: 20px;
}
```

##### 外边距塌陷

场景：父子级的标签，子级的添加 **上外边距** 会产生**塌陷**问题

现象：**导致父级一起向下移动**

```css
.son {
  margin-top: 50px;
  width: 100px;
  height: 100px;
  background-color: orange;
}
```

 <div class="father" style="width: 300px;
            height: 300px;
            background-color: pink;">
        <div class="son" style=" margin-top: 50px;
            width: 100px;
            height: 100px;
            background-color: orange;">son</div>
    </div>

解决方法：

* 取消子级margin，父级设置padding
* 父级设置 overflow: hidden 让浏览器找到父级的正确边缘
* 父级设置 border-top 让浏览器找到父级的正确边缘

> 如果父级有内容，就不会有这个问题

#### 行内元素 – 内外边距问题 

场景：行内元素添加 margin 和 padding，无法改变元素垂直位置

解决方法：给行内元素添加 **line-height** 可以改变垂直位置

```css
span {
  /* margin 和 padding 属性，无法改变垂直位置 */
  margin: 50px;
  padding: 20px;
  /* 行高可以改变垂直位置 */
  line-height: 100px;
}
```

#### 圆角

作用：设置元素的外边框为圆角。

属性名：**border-radius**

属性值：数字+px / 百分比

提示：属性值是圆角半径

- 多值写法

| 取值个数 |               示例                |                    含义                     |
| :------: | :-------------------------------: | :-----------------------------------------: |
|  一个值  |        border-radius:10px;        |               四个角均为10px                |
|  四个值  | border-radius:10px 20px 40px 80px | 左上：10px;右上：20px;右下：40px;左下：80px |
|  三个值  |   border-radius:10px 40px 80px    |    左上：10px;右上+左下：40px;右下：80px    |
|  两个值  |     border-radius:10px 80px;      |       左上+右下：10px;右上+左下：80px       |

> 技巧：从左上角开始顺时针赋值，当前角没有数值则与对角取值相同。 

* 正圆形状：给正方形盒子设置圆角属性值为 **宽高的一半 / 50%**

```css
img {
  width: 200px;
  height: 200px;
  
  border-radius: 100px;		/*width=height时，设置border-radius为width/height一半相当于圆形*/
  border-radius: 50%;
}
```

<div style="width:200px;height:200px;border-radius:50%;background-color:green;"></div>

* 胶囊形状：给长方形盒子设置圆角属性值为 盒子高度的一半 

```css
div {
  width: 200px;
  height: 80px;
  background-color: orange;
  border-radius: 40px;
}
```

<div style="width: 200px;
  height: 80px;
  background-color: orange;
  border-radius: 40px;">
</div>

#### 盒子阴影（拓展）

作用：给元素设置阴影效果

属性名：**box-shadow**

属性值：X 轴偏移量  Y 轴偏移量  模糊半径  扩散半径  颜色  内外阴影

注意： 

* X 轴偏移量 和 Y 轴偏移量 必须书写
* 默认是外阴影，内阴影需要添加 inset

```css
div {
  width: 200px;
  height: 80px;
  background-color: orange;
  box-shadow: 2px 5px 10px 0 rgba(0, 0, 0, 0.5) inset;
}
```

<div style="width: 200px;
  height: 80px;
  background-color: orange;
  border-radius:40px;
  box-shadow: 2px 5px 10px 0 rgba(0, 0, 0, 0.5);">
</div>

 