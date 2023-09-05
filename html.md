# HTML 详解

## HTML是什么

超文本标记语言

Hyper Text Markup Language

所有浏览器都支持HTML5

可跨平台

W3C标准

结构话标准语言（HTML、XML）
表现标准语言（CSS）
行为标准（DOM，ECMAScript）

## 语法

### 注释

```html
<!-- 
注释
-->
```

### DOCTYPE
告诉浏览器使用什么规范
```html
<!DOCTYPE html>
```

### \<html lang='en'>

所有内容均写在该标签下

### head标签

网页的头部
#### meta标签
描述网站的信息
一般用来左seo

### title标签

网页的标题

### body标签

网页内容

### 标签

#### 标题

```html
<h1>一级标签</h1>
<h2>二级标签</h2>
<h3>三级标签</h3>
```

#### 段落

```html
<p>两只老虎</p>
<p>跑得快</p>
```

#### 换行

```html
两只老虎<br/>
跑得快<br/>
```

#### 水平线

```html
<hr/>
```

#### 字体样式

粗体和斜体
```java
<strong>i love you</strong>
<em>i hate you</em>
```

#### 特殊符号

空格
大于号
小于号
版权符号
```java
&nbsp;
&gt;
&lt;
&copy;
```

#### 图像

##### 常见图像格式

JPG

GIF

PNG

BMP

...

##### 书写格式

```html
<img src="path" alt="text" title="text" width="x" height="y" />
```

#### 链接标签

```html
<a href="https://www.baidu.com" target="_blank">点我跳转</a>新页面跳转
```

##### 锚链接
```html
<a name="top">顶部</a>
...
...
...
<a href="#top">回到顶部</a>
```

##### 功能性链接
```html
<a href="mailto:1365957941@qq.com">点击联系我</a>
```

#### 列表

##### 有序列表

```html
<ol>
    <li>Java</li>
    <li>Python</li>
</ol>
```

##### 无序列表

```html
<ul>
    <li>Java</li>
    <li>Python</li>
    <li>C++</li>
</ul>
```

##### 自定义列表

```html
<dl>
    <dt>学科</dt>
    <dd>Java</dd>
    <dd>C</dd>
    <dd>C++</dd>

    <dt>地点</dt>
    <dd>Jav</dd>
    <dd>C-</dd>
    <dd>C+</dd>
</dl>
```

#### 表格

```html
<table border="=1px">
    <tr>
        <td colspan="3">1-1</td>
    </tr>
    <tr>
        <td rowspan="2">2-1</td>
        <td>2-2</td>
        <td>2-3</td>
    </tr>
    <tr>
        <td>3-1</td>
        <td>3-2</td>

    </tr>
</table>
```

#### 音视频

```html
<video src="崔三娘残局1打2.mp4" controls autoplay></video>

<audio src="" controls autoplay></audio>


```

#### 页面结构

```html
<body>
<header>
    <h2>网页头部</h2>
</header>
<section>
    <h2>网页主体</h2>
</section>
<footer>
    <h2>网页脚部</h2>
</footer>
</body>
```
#### 表单

```html
<form action="path" method="get">
    <p>名字：<input type="text" name="username"></p>
    <p>密码：<input type="password" name="psd"></p>
    <p>
        <input type="submit">
        <input type="reset">
    </p>
</form>yo
```

type 指定元素的类型
text password checkbox
radio submit reset file 
hidden image button 默认text

name 指定元素的名称

value 元素的初始值 type位radio时必须指定一个值

size 指定表单元素的初始值
当type为text或password时
表单元素的大小以字符为单位
其他类型宽度以像素为单位

maxlength 最大字符数

checked 指定按钮是否被选中



