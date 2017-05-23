CSS Tables
--
去除双层border(既border塌陷)
``` css
	border-collapse: collapse;
```
Responsive Table(响应式表格)
``` html
	<div style="overflow-x:auto;">

	<table>
	... table content ...
	</table>

	</div>
```
Striped Tables(条纹表格nth-child()选择器)
``` css
	tr:nth-child(even) {background-color: #f2f2f2}
```
CSS Display
--
Examples of block-level elements:

- <div\>
- <h1\> - <h6\>
- <p\>
- <form\>
- <footer\>
- <header\>
- <section\>

Examples of inline elements:

- <span\>
- <a\>
- <img\>

display:none 与 visibility:hidden区别

前者网页会认为它不存在，不会占据位置，后者还是存在的并且占据位置指示不显示而已。

CSS Layout-width and max-width
-
使用max-width可以实现浏览器宽度小于最大宽度后，宽度随浏览器缩小变小。

CSS Layout-The position Property
-
position：static；

默认的定位方式不被上下左右的元素所影响。

position：relative；

相对于自己默认的位置根据TRBL来移动，但还是会占据原位置，且如果原位置被挤走，位置也会跟着变动。不是瞬移，只是隐藏本体，显示分身位置。

position： absolute；

相对于有定位(非static定位)的最近的父级元素定位，如果没有定位的父级元素，则根据body左上角来定位。定位后会脱离文档流，不会占据原先的位置，理解为瞬间移动。

overlapping elements(重叠的元素)

z-index;

定位后的元素可以使用此属性来划分层次。定位必须是除static外的其他几种定位方式，如果所有节点都定义了position：relative，A节点的z-index和B节点一样大，但因为顺序规则，B节点覆盖在A节点前面，就算A的子节点z-index值比B的子节点大，B的子节点还是会覆盖在A的子节点前面。

### Tips
----
inline-block化

absolute与float会是其作用的元素inline-block化，例如一个div标签默认宽度是100%显示，如果使用了absolute或者float则其宽度就会变成自适应内部元素的宽度。

CSS Layout-float and clear
-
浮动最开始也是最正确的用途就是使文字环绕图片，越来越多的开发人员使用它来布局，推荐能不使用浮动就不使用浮动，它会带来很多问题。

清除浮动，既消除浮动对其他元素的影响，可以给浮动元素外套一层标签加入clear：...属性，但不推荐，太多无意义的标签破坏代码结构，其实清除浮动即闭合浮动，只要为其创建一个独立的BFC即可，就可以把浮动元素与外部隔离，不会影响外部，创建BFC的方法很多如overflow除visiable外，float除none外，position除static，relative外，
display：inline-block|table-cells|table-captions,会为其内容创建BFC。

CSS Layout-inline-block
-
可实现与float类似效果但不会有float的影响。

CSS Align
-
文字垂直居中可以使用line-height等于高度来设置，也可以使用定位配合transform属性来实现居中。
``` css
	//css
		.center {
	    height: 200px;
	    position: relative;
	    border: 3px solid green;
	}

	.center p {
	    margin: 0;
	    position: absolute;
	    top: 50%;
	    left: 50%;
	    -ms-transform: translate(-50%, -50%);
	    transform: translate(-50%, -50%);
	}
```
![](http://i4.buimg.com/567571/3bd603b15a919a51.png)
CSS Combinators
-
>A combinator is something that explains the relationship between the selectors.

* descendant selector(space)只要位于父级标签内的子标签全部选中
* child selector(>)选中直接子标签
* adjacent sibling selector(+)相邻标签选择
* general sibling selector(~)一般统计选择
CSS Pseudo-classes(伪类)
-
Anchor Pseudo-classes
``` css
	/* unvisited link */
	a:link {
	    color: #FF0000;
	}

	/* visited link */
	a:visited {
	    color: #00FF00;
	}

	/* mouse over link */
	a:hover {
	    color: #FF00FF;
	}

	/* selected link */
	a:active {
	    color: #0000FF;
	}
```
>Note:`a:hover`MUST come after `a:link` and `a:visited` in the CSS definition in order to be effective `a:active` MUST come after `a:hover` in the CSS definition in order to be effective! Pseudo-class names are not case-sensitive.

The :first-child Pseudo-class

##伪类种类
|伪类|作用|
|---|---|
|:active|将样式添加到被激活的元素|
|:focus|将样式添加到被选中的元素|
|:hover|当鼠标悬浮在元素上方时，向元素添加样式|
|:link|将特殊的样式添加到未被访问过的链接|
|:visited|将特殊的样式添加到被访问过的链接|
|:first-child|将特殊的样式添加到元素的第一个子元素|
|:lang|允许创作者来定义指定的元素中使用的语言|

##伪元素种类
|伪元素|作用|
|-----|----|
|::first-letter|将特殊样式添加到文本首字母|
|::first-line|将特殊样式添加到文本首行|
|::before|在某元素之前插入|
|::after|在某元素之后插入|

完整版
-
![](http://i2.buimg.com/567571/4197e660e04b47e3.png)

![](http://i2.buimg.com/567571/1bbaaaa80ade5d2b.png)

![](http://i1.buimg.com/567571/e67b8cbf3aa6e393.png)

![](http://i1.buimg.com/567571/1bd15d20f953f622.png)

CSS Navigation Bar
-
导航栏一般是使用列表实现，水平的导航栏使用浮动或display:inline-block;使用媒体查询实现响应式导航栏
CSS [attribute] Selector(属性选择器)
-
根据自己的需要选择有相应的元素。
> p[type="text"]

##CSS3 Introduction(介绍)
Some of the most inportant CSS3 modules are:
- Selectors
- Box Model
- Backgrounds and Borders
- Text Effects
- 2D/3D Transformations
- Animations
- Multiple Column Layout
- User Interface

CSS3 Rounded Corners
-
examples:
1. Four values - border-radius: 15px 50px 30px 5px;

![](http://ww1.sinaimg.cn/large/97c215ddjw1f73xde7ztxj206r04v744.jpg)
2. Three values - border-radius: 15px 50px 30px;

![](http://ww1.sinaimg.cn/large/97c215ddjw1f73xx8e2gjj207s04tq2s.jpg)

CSS3 Border Images
-
>border-image: url();
>-webkit-border-image: url();
>-o-border-image: url();

CSS3 Backgrounds
-
New CSS3 properties:
- background-size
- background-origin
- background-clip

CSS3 colors
-
>RGBA Colors (red,green,blue,alpha)
>HSL Colors (hue色调,saturation饱和,lightness亮度)
>HSLA
>Opacity

CSS3 Gradients
-
渐变
CSS3 Shadow Effects
-
- text-shadow
- box-shadow

CSS3 Text
-
- text-overflow
- word-wrap
- word-break

>text-overflow: ellipsis //可以将超出宽度的以省略号显示。
>text-overflow: clip //直接将超出宽度的切割
>word-wrap: break-word //自动换行
>word-break: keep-all //单词显示完整
>word-break: break-all //单词会被中间换行分开

CSS3 Web Fonts
-
ex.

    @font-face {
      font-family: myFirstFont;
      src: url(...);
    }
    div {
      font-family: myFirstFont;
    }

CSS3 2D Transforms
-
- translate()
- ratate()
- scale()
- skewX()
- skewY()
- matrix()

>translate() //让元素在x/y轴平移<br>
>rotate() //旋转元素<br>
>scale() //沿x/y轴放大元素<br>
>skewX() //沿x轴拉伸<br>
>skewY() //沿y轴拉伸<br>
>skew() //沿x,y轴拉伸<br>
>matrix() //通过矩阵变换实现上述效果，是上述变化的原理可以实现更高级的变化。<br>
>matrix(a,b,c,d,e,f)对应矩阵如下

![](http://ww3.sinaimg.cn/large/97c215ddjw1f74v4xlb60j204m02wa9w.jpg)
CSS3 Transitions
-
>transition: property time;

The transition-timing-function

- ease
- linear
- ease-in
- ease-out
- ease-in-out
- cubic-bezier(n,n,n,n)

The transition-delay
> transition-delay: time;

>Transition + Transformation

CSS3 Animations
-
    example
    /* The animation code */
    @keyframes example {
       from {background-color: red;}
       to {background-color: yellow;}
    }
    /* The element to apply the animation to */
    div {
       width: 100px;
       height: 200px;
       background-color: red;
       animation-name: example;
       animation-duration: 4s;
    }
    example
    /* The animation code */
    @keyframes example {
       0% {}
       25% {}
       50% {}
       75% {}
       100% {}
    }

>animation-iteration-count: 3; //重复次数(infinite无限循环)
>animation-delay: 2s; //延迟时间
