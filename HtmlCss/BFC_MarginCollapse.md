# BFC (Block formatting contexts)
## 块格式化上下文

W3C规范中的BFC定义：<br>
浮动元素和绝对定位元素，非块级盒子的块级容器(例如inline-blocks,table-cells,table-captions)，以及overflow值不为"visiable"的块级盒子，都会为他们的内容创建新的BFC。

在BFC中，盒子从顶端开始垂直一个接着一个的排列，两个盒子之间的间距是由他们的margin值决定的，在一个BFC中，两个相邻的块级盒子的垂直外边距会产生重叠。(只有垂直会产生，水平不会)

在BFC中，每一个盒子的左外边缘(margin-left)会触碰到容器的左边缘(border-left)(从右到左的格式来说就是触碰右外边缘)。

BFC通俗的理解：

是一个独立的布局环境，可以理解为一个箱子，里面的东西不受外界影响，即BFC中的元素布局不受外界影响(往往利用这个特性来相处浮动元素对非浮动兄弟元素和其子元素带来的影响)。并且在一个BFC中，块盒和行盒(行盒由一行内的所有内联元素组成)，都会垂直的沿着其父元素的边框排列。

__BFC的运用：__

网站中经常见到的左边图片+右边信息的两栏结构，可以利用BFC实现。

首先给出如下结构

	//css
	.box{
	width:210px;
	border:1px solid #000;
	float:left;
	}
	.img{
	width:100px;
	height: 100px;
	background-color: green;
	float:left;
	}
	.info{
	background-color: #ccc;
	color: #fff;
	}
一般情况下会呈现：

![](http://i2.buimg.com/567571/fb920f0aca919042.png)

但是当文字内容增多后，会变成：

![](http://i2.buimg.com/567571/4e9a855d4e7a538f.png)

很明显，这里因为info类里面的文字收到了浮动元素的影响，这并不是我们想要的，这时我们可以为p元素的内容建立一个新的BFC，让其内容消除外界浮动元素的影响，我们只要给info元素添加overflow：hidden；即可以为其内容建立新的BFC，也可以通过其他方法来建立，效果如下：

![](http://i2.buimg.com/567571/ab20b8a84e489189.png)






## 合并外边距与BFC

在css当中，相邻的两个盒子(可能是兄弟关系也可能是祖先关系)的外边距可以结合成一个单独的外边距。这种合并外边距的方式被称为折叠，并且因而所结合成的外边距称为折叠外边距。

折叠的结果：

- 两个相邻的外边距都是正数时。折叠结果是它们两者之间较大的值。

- 两个相邻的外边距都是负数时，折叠结果是两者绝对值的较大者。

- 两个外边距一正一负时，折叠结果是两者的和。

产生折叠的必备条件：margin必须是邻接的！

根据W3C规范，两个margin是邻接的必须满足以下条件：

- 必须是处于常规文档流(非float和绝对定位)的块级盒子，并且处于同一个BFC当中。

- 没有线盒，没有空隙(**clearance**看下文)，没有padding和border将他们分隔开。

- 都属于垂直方向上相邻的外边距，可以是下面任意一种情况。

- 元素margin-top与其第一个常规文档流的子元素的margin-top。

- 元素的margin-bottom与其下一个常规文档流的兄弟元素的margin-top。

- height为auto的元素的margin-bottom与其最后一个常规文档流的子元素的margin-bottom。

- 高度为0并且最小高度也为0，不包含常规文档流的子元素，并且自身没有建立新的BFC的元素的margin-top和margin-bottom。

以上条件以为着下列的规则：

- 创建了新的BFC的元素(例如浮动元素或者'overflow'值为'visible'以外的元素)与它的子元素的外边距不会折叠。

- 浮动元素不与任何元素的外边距产生折叠(包括其父元素和子元素)。

- 绝对定位元素不与任何元素的外边距产生折叠。

- inline-block元素不与任何元素的外边距产生折叠。

- 一个常规文档流的margin-bottom与它的下一个常规文档流的兄弟元素的margin-top会产生折叠，除非他们之间存在间隙(**clearance**)。

- 一个常规文档流元素的margin-top与其第一个常规文档流的子元素的margin-top产生折叠，条件为父元素不包含'padding'和'border'，子元素不包含间隙(**clearance**)。

- 一个'height'为'auto'并且'min-height'为'0'的常规文档流元素的margin-bottom会与其最后一个常规文档流子元素的margin-bottom折叠，条件为父元素不包含'padding'和'border'，子元素的margin-bottom不与包含clearance的margin-top折叠。

- 一个不包含border-top,border-bottom,padding-top,padding-bottom的常规文档流元素，并且其'height'为0或'auto'，'min-height'为0，其里面也不包含行盒(line box)，其自身的margin-top和margin-bottom会折叠。

**(逐一分析不产生折叠的情况)**

浮动和绝对定位不与任何元素产生margin折叠
--
原因：浮动元素和绝对定位元素不与其他盒子产生外边距折叠是因为**元素会脱离当前的文档流，违反了上面所述的两个margin是邻接的条件，同时，浮动和绝对定位会是元素为它的内容创建新的BFC**，因此该元素和子元素所处的BFC是不相同的，因此也不会产生margin的折叠。
DEMO:


	//CSS
	body {padding:0;margin: 0; text-align: center;}
	.wrapper {margin:30px;width: 450px;border:1px solid red;}
	.small-box {width: 50px;height: 50px;margin: 10px;background: #9cc;}
	.middle-box {width: 100px;height: 100px;margin: 20px;background: #99c;}
	.big-box {width: 120px;height: 120px;margin: 20px;background: #33e;}
	.floatL {float: left;}
	.floatR {float: right;}
	.clear {clear: both;}
	.posA {position: absolute;}
	.overHid{overflow: hidden;}
	.red {background: #f00;}
	.green {background: #0f0;}
	.blue {background: #00f;}
	//HTML
	<div class="wrapper overHid">
	    <div class="big-box blue">non-float</div>
	    <div class="middle-box green floatL">
	        <div class="small-box red"></div>
	        float left
	    </div>
	</div>

![](http://i2.buimg.com/567571/08c1a32a6ef1ee85.png)

但是浮动元素脱离了当前的BFC并不影响它后面的兄弟元素，后面的兄弟元素与浮动元素前面的元素依然在同一个BFC中，所有，他们之间的margin还是会折叠的，下面对上面的demo进行修改：

	<div class="wrapper overHid">
	    <div class="big-box">non-float</div>
	    <div class="middle-box green floatL">float left</div>
	    <div class="middle-box red">non-clear</div>
	</div>

![](http://i2.buimg.com/567571/471fa8d473b81457.png)

可以看出，红色的块盒在没有清除浮动的情况下，其margin-top和蓝色块盒的margin-bottom产生折叠。<br>
下面来看看**'clearance'**，当浮动元素之后的元素设置clear以闭合相关方向的浮动时，根据W3C规范规定，闭合浮动(清除浮动)的元素会在其margin-top以上产生一定的空隙(clearance，如下图)，该空隙会组织元素margin-top的折叠，并作为间距存在于元素的margin-top的上方。来看看例子

	<div class="wrapper overHid">
	    <div class="big-box" style="box-shadow:0 20px 0 rgba(0,0,255,0.2);">non-float</div>
	    <div class="middle-box green floatL" style="opacity:0.6">float left</div>
	    <div class="middle-box red clear" style="margin-top:40px;box-shadow:0 -40px 0 rgba(255,0,0,0.2);">clear</div>
	</div>

![](http://i2.buimg.com/567571/44e608c2619a0466.png)

上面的图中我们可以看到，我们为红色块盒设置的40px的margin-top(使用相同高度的阴影来将其可视化)好像并没有对紫色块盒起作用，而且无论我们怎么修改这个margin-top值都不会影响红色块盒的位置，而只由绿色块盒的margin-bottom所决定。

也就是说，我们只需要知道，闭合浮动的元素的border-top会紧贴着相应的浮动元素的margin-bottom。

原来，通过W3C的官方规范可知，闭合浮动(清除浮动)的块盒在margin-top上所产生的间距(clearance)的值与该块盒的margin-top之和应该足够让该块盒垂直跨越浮动元素的margin-bottom，使闭合浮动的块盒的border-top恰好与浮动元素的块盒的margin-bottom向邻接。

PS！闭合浮动并不能使浮动元素回到原来的BFC中！

inline-block元素与其兄弟元素，子元素和父元素的外边距都不会折叠(包括其父元素和子元素)
--
inline-block不符合W3C规范所说元素必须是块级盒子的条件，规范中又说明，块级盒子的display属性必须是一下三种之一：'block','list-item','table'。
