[toc]


# 你的页面应该长什么样
- 编写代码之前如何做好计划和设计工作，包括：
	- “网页是用来做什么的？”
	- “网页要提供什么信息？”
	- “要用什么字体和颜色？”
## 色彩设计
- 多看看别的知名网站是怎么设计颜色搭配的，如各大公司的官网
- google的 红 - 黄 -蓝 -绿
- mrtk-webrtc的 蓝-红-浅红-绿-金-淡金
### 简洁-优雅-让人舒服的秘密


## 布局设计

# how使用html+css+js实现出页面
## 骨(html)-皮(css)-神(js)

## html入门
### html由elements构成
1. 元素的结构
- elements的结构：
<img src="C:\Users\king-kong\Desktop\BlogPlan\4+1\Gitmind\Picture\element.png" alt="elements的结构" style="zoom:50%;" />
2. 元素可以嵌套
- 但是要有序
```
//正确
<p>我的猫咪脾气<strong>暴躁</strong>:)</p>
//错误
<p>我的猫咪脾气<strong>暴躁</p></strong>
```
3. 元素可以为空
- 不包含任何内容的元素称为空元素。比如 <img> 元素：
```
<img src="images/firefox-icon.png" alt="测试图片">
```

- 本元素包含两个属性，但是并没有 </img> 结束标签，元素里也没有内容。这是因为图像元素不需要通过内容来产生效果，它的作用是向其所在的位置嵌入一个图像。

### elements可以有Attribute：
- 属性包含了关于元素的一些额外信息，这些信息本身不应显现在内容中。

### 1. 一个pure html的结构
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>测试页面</title>
  </head>
  <body>
    <img src="images/firefox-icon.png" alt="测试图片">
  </body>
</html>
```
1. <!DOCTYPE html> — 文档类型。混沌初分，HTML 尚在襁褓（大约是 1991/92 年）之时，DOCTYPE 用来链接一些 HTML 编写守则，比如自动查错之类。DOCTYPE 在当今作用有限，仅用于保证文档正常读取。现在知道这些就足够了。
2. <html></html> 。该元素包含整个页面的内容，也称作根元素。
3. <head></head> 。该元素的内容对用户不可见，其中包含例如面向搜索引擎的搜索关键字（keywords）、页面描述、CSS 样式表和字符编码声明等。
4. <meta charset="utf-8"> — 该元素指定文档使用 UTF-8 字符编码 ，UTF-8 包括绝大多数人类已知语言的字符。基本上 UTF-8 可以处理任何文本内容，还可以避免以后出现某些问题，没有理由再选用其他编码。
5. <title></title> 。该元素设置页面的标题，显示在浏览器标签页上，也作为收藏网页的描述文字。
6. <body></body> 。该元素包含期望让用户在访问页面时看到的内容，包括文本、图像、视频、游戏、可播放的音轨或其他内容。

### 2. 往pure html中加入image
```
<img src="images/firefox-icon.png" alt="一只盘旋在地球上的火狐">
```
1. img元素使用时一般只需要设置成空元素
2. img元素还包括一个替换文字属性 alt，是图像的描述内容，用于当图像不能被用户看见时显示，不可见的原因可能是：
- 用户有视觉障碍。视障用户可以使用屏幕阅读器来朗读 alt 属性的内容。
- 有些错误使图像无法显示。可以试着故意将 src 属性里的路径改错。保存并刷新页面就可以在图像位置看到
### 3. 往pure html中加入标记文本
#### 标题
1. HTML 包括六个级别的标题
```
<h1>主标题</h1>
<h2>顶层标题</h2>
<h3>子标题</h3>
<h4>次子标题</h4>
```
#### 段落
```
<p>这是一个段落</p>
```
#### 链表
1. 列表类型为：<ul></ul> 有序列表， <ol> </ol>无序列表。
2. 列表的每个项目用一个列表项目（List Item)元素 ```<li>``` 包围
```
<ul>
  <li>技术人员</li>
  <li>思考者</li>
  <li>建造者</li>
</ul>
```
#### 链接
```
<a href="https://www.mozilla.org/zh-CN/about/manifesto/">Mozilla 宣言</a>
```

## css入门
### css由规则集构成
<img src="C:\Users\king-kong\Desktop\BlogPlan\4+1\Gitmind\Picture\css-declaration.png" style="zoom:50%;" />

### 各种类型的选择器
#### 1. 元素选择器
- 会对html所有符合的元素进行设置
##### 单元素选择
###### 单属性
######多属性
1. 字体-文本相关属性
2. 
##### 多元素选择
- 对多种元素进行同一种设置时使用多元素选择
#### 3. ID 选择器	
#### 4. 类选择器	
#### 5. 属性选择器	
#### 6. 伪(Pseudo)类选择器

### 一切皆盒子
#### 每一组闭合标签看作一个盒子
- 顺序排列的盒子
- 嵌套的盒子
#### 每个盒子视为单位，对其进行属性设置
##### 盒子可配置的属性有哪些
###### 布局属性
1. 使用margin-border-padding来进行布局
<img src="C:\Users\king-kong\Desktop\BlogPlan\4+1\Gitmind\Picture\box-model.png" style="zoom:50%;" />

- 1. 使用__相对的布局__ 优于 绝对布局
	- 因为不同的浏览器分辨率(长宽比)可能不同
- 2. 尽量居中显示
	- margin: 0 auto;
		- 为 margin 或 padding 等属性设置两个值时，第一个值代表元素的上方和下方（在这个例子中设置为 0），而第二个值代表左边和右边（在这里，auto 是一个特殊的值，意思是水平方向上左右对称）。
	- 如：图像居中
			- 1. 只需要将图像看作普通的盒子组件即可
			- 2. 为了使图像有外边距，我们必须使用 display: block 给予其块级行为。
				- <body> 元素是块级元素，意味着它占据了页面的空间并且能够赋予外边距和其他改变间距的值。而图片是内联元素，不具备块级元素的一些功能。所以为了使图像有外边距，我们必须使用 display: block 给予其块级行为。
```
img {
  display: block;
  margin: 0 auto;
}
```
- 3. 
	- border: 5px solid black; 
		- 直接为 body 设置 5 像素的黑色实线边框。
- 4. 内边距和border间留点空隙
	- padding: 0 20px 20px 20px; 
		- 我们给内边距设置了四个值来让内容四周产生一点空间。这一次我们不设置上方的内边距，设置右边，下方，左边的内边距为20像素。值以上、右、下、左的顺序排列。
		###### 


##### 不同粒度的设置组合
1.  对整个页面进行统一设置：背景色、字体大小、字体样式
```
	html {
    /* px 表示 “像素（pixels）”: 基础字号为 10 像素 */
    font-size: 20px;
    /* Google fonts 输出的 CSS */
    font-family: 'Open Sans', sans-serif;
    background-color: #00539F;
	}
```
2. 对文档体进行设置
```
body {
  width: 600px;
  margin: 0 auto;
  background-color: #FF9500;
  padding: 0 20px 20px 20px;
  border: 5px solid black;
}
```
3. 给标题设置样式
- 
```
  h1 {
    margin: 0;
    padding: 20px 0;
    color: #00539F;
    text-shadow: 3px 3px 1px black;
  }
```

### 将css的样式作用于html文件

- 将css用于html文件中的<head> 和 </head> 标签之间
```
<link href="styles/style.css" rel="stylesheet">
```

## js入门

### 编写js代码

### 将js效果加入html中
- 一般简单短小的使用嵌入式
	- 嵌入式的位置一般要在内容呈现后的地方，除非使用异步加载机制
- 复杂又长的使用外部链接式
	- 优点：
		- 1. 快。
			- 浏览器会下载它，然后将它保存到浏览器的缓存中
			- 之后，其他页面想要相同的脚本就会从缓存中获取，而不是下载它。所以文件实际上只会下载一次。这可以节省流量，并使得页面（加载）更快。
		- 2. 一次编写多个页面复用。

3. 嵌入式&&外部式不能用于同一对script标签：外部会覆盖嵌入的部分
<script src="file.js">
  alert(1); // 此内容会被忽略，因为设定了 src
</script>
#### 嵌入式

#### 外部链接式
##### 本地文件夹链接
1. 相对路径
2. 绝对路径
<script src="/path/to/script.js"></script>
##### url链接式
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>







# 网站存到哪
1. 每一个网站(多个网页(html+css+js+asset的集合)的集合)应该存储在同一个文件夹下，一个文件夹就是一个工程

2. 最基本、最常见的结构是：一个主页、一个图片文件夹、一个样式表文件夹和一个脚本文件夹：
- index.html ：这个文件一般包含主页内容，即用户第一次访问站点时看到的文本和图像。使用文本编辑器在 test-site 文件夹中新建 index.html。
- images 文件夹 ：这个文件夹包含站点中的所有图像。在 test-site 文件夹中新建 images 文件夹。
- styles 文件夹 ：这个文件夹包含站点所需样式表（比如，设置文本颜色和背景颜色）。在 test-site 文件夹中新建一个 styles 文件夹。
- scripts 文件夹 ：这个文件夹包含提供站点交互功能的 JavaScript 代码（比如读取数据的按钮）。在 test-site 文件夹中新建一个 scripts 文件夹。

3. 路径问题
- 1. 如果按照2.中的结构，图片在 images 目录下，而 images 目录与 index.html 处于同级目录。要从 index.html 所处一级目录进入图片所在目录，所需的文件路径是 images/xxxxx.png 。
- 2. 文件路径的一些通用规则：
	- 若引用的__目标文件与 HTML 文件同级__，只需直接使用文件名，比如 my-image.jpg 。
	- 要引用子文件夹中的文件，要在路径前写下目录名并加一个__正斜杠__（windows下一般使用反斜杠，但是使用正斜杠不会报错，推荐使用正斜杠），比如 subdirectory/my-image.jpg 。
	- 若引用的__目标文件位于 HTML 文件的上级__，需要加上两个点。比如，如果 index.html 在 test-site 下面的一个子目录而 my-image.png 在 test-site 目录，你可以在 index.html 里使用 ../my-image.png 引用 my-image.png 。
	- 以上方法可以随意组合，比如 ../subdirectory/another-subdirectory/my-image.png。