<style type="text/css">
body {
	background-color: #CB4042;	
}
.body-style-0 {
	background-color: #CB4042;
}
.body-style-1 {
	background-color: #B5CAA0;
}
.body-style-2 {
	background-color: #66BAB7;
}
pre {
	color: red;
	background-color: white;
}
code {
	font-size: 20px;
	background-color: lightgreen;
}
h1 {
	font-size: 50px;
}
h2 {
	font-size: 30px;
}
hr {
	border-color: black;
}
blockquote {
	background-color: black;
	color: white;
	font-size: 20px;
}
</style>
#Canvas取色Demo
---
##内容导读
		1.取色Demo展示及原理
		2.Canvas简介以及一些Demo
		3.题外话
##1.取色器Demo及其原理
>思维导图

![](./网页取色工具思路.png)

##2.Canvas简介及一些Demo
>HTML5`<canvas>`元素用与网页中图形的绘制，通过脚本(javascript)来完成，`<canvas>`标签只是图形容器，必须使用脚本来绘图

>常用方法

>- moveTo(x, y)
>- lineTo(x, y)

	使用这个方法我们可以画一些东东，比如：

<canvas id="canvas-1" width="400" height="400"></canvas>
<canvas id="canvas-2" width="400" height="400">
	<span>不支持canvas的浏览器就会显示</span>
</canvas>

<script type="text/javascript">
	function draw(){
		var oc = document.getElementById('canvas-1');
		var content = oc.getContext('2d');
		content.beginPath();
		content.arc(75,75,50,0,Math.PI*2,true);//脸
		content.moveTo(110,75);
		content.arc(75,75,35,0,Math.PI,false); //嘴巴
		content.moveTo(65,65);
		content.arc(60,65,5,0,Math.PI*2,true); //左眼
		content.moveTo(95,65);
		content.arc(90,65,5,0,Math.PI*2,true);//右眼
		content.stroke();
	}
	draw();
</script>
<script type="text/javascript">
	window.onload = function(){
		var oc = document.getElementById('canvas-2');
		var content = oc.getContext('2d');
 		
 		function toDraw(){
 			var x= 200;
 			var y = 200;
 			var r = 150;
 			content.clearRect(0,0,oc.width,oc.height);
 			var date = new Date();
 			var hour = date.getHours();
 			var minute = date.getMinutes();
 			var second = date.getSeconds();
 			var hValue = (-90+hour*30 + minute/2)*Math.PI/180;
 			var mValue = (-90+minute*6)*Math.PI/180;
 			var sValue = (-90+second*6)*Math.PI/180;
 			//表盘小刻度
 			content.beginPath();
 			for(var i=0;i<60;i++){
 				content.moveTo(x,y);
 				content.arc(x,y,r,6*i*Math.PI/180,6*(i+1)*Math.PI/180,false);
 			}
 			content.closePath();			
 			content.stroke();
 			//盖上中间部分
 			content.fillStyle = 'white';
 			content.beginPath();
 			content.moveTo(x,y);
 			content.arc(x,y,r*19/20,0,360*(i+1)*Math.PI/180,false);
 			content.closePath();
 			content.fill();
 			//表盘大刻度
 			content.lineWidth = 3;
 			content.beginPath();
 			for(var i=0;i<12;i++){
 				content.moveTo(x,y);
 				content.arc(x,y,r,30*i*Math.PI/180,30*(i+1)*Math.PI/180,false);
 			}
 			content.closePath();			
 			content.stroke();
 			//盖上中间部分
 			content.fillStyle = 'white';
 			content.beginPath();
 			content.moveTo(x,y);
 			content.arc(x,y,r*18/20,0,360*(i+1)*Math.PI/180,false);
 			content.closePath();
 			content.fill();
 			//时针
 			content.lineWidth = 5;
 			content.beginPath();
 			content.moveTo(x,y);
 			content.arc(x,y,r*10/20,hValue,hValue,false);
 			content.closePath();
 			content.stroke();
 			//分针
 			content.lineWidth = 3;
 			content.beginPath();
 			content.moveTo(x,y);
 			content.arc(x,y,r*14/20,mValue,mValue,false);
 			content.closePath();
 			content.stroke();
 			//秒针
 			content.lineWidth = 1;
 			content.beginPath();
 			content.moveTo(x,y);
 			content.arc(x,y,r*19/20,sValue,sValue,false);
 			content.closePath();
 			content.stroke();
 		}
 		setInterval(toDraw,1000);
 		toDraw();
	}
</script>
	还有一些更高大上的方法
	#quadraticCurveTo(cp1x, cp1y, x, y)
	(cp1x, cp1y)--控制点
	这个函数用于从当前画笔位置，到(x, y)处画一条二次曲线
	#bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)
	从当前位置到(x, y)画一条贝塞尔曲线
	我们看看他能画啥:

<canvas id="canvas-3" width="400" height="200"></canvas>
<canvas id="canvas-4" width="400" height="200"></canvas>
<script type="text/javascript">
	function draw(){
	  var canvas = document.getElementById('canvas-3');
	  if (canvas.getContext) {
	    var ctx = canvas.getContext('2d');
	    // Quadratric curves example
	    ctx.beginPath();
	    ctx.moveTo(75,25);
	    ctx.quadraticCurveTo(25,25,25,62.5);
	    ctx.quadraticCurveTo(25,100,50,100);
	    ctx.quadraticCurveTo(50,120,30,125);
	    ctx.quadraticCurveTo(60,120,65,100);
	    ctx.quadraticCurveTo(125,100,125,62.5);
	    ctx.quadraticCurveTo(125,25,75,25);
	    ctx.stroke();
		}
	}
	draw();
</script>
<script type="text/javascript">
	function draw(){
	  var canvas = document.getElementById('canvas-4');
	  if (canvas.getContext){
	    var ctx = canvas.getContext('2d');
	    // Quadratric curves example
	    ctx.beginPath();
	    ctx.moveTo(75,40);
	    ctx.bezierCurveTo(75,37,70,25,50,25);
	    ctx.bezierCurveTo(20,25,20,62.5,20,62.5);
	    ctx.bezierCurveTo(20,80,40,102,75,120);
	    ctx.bezierCurveTo(110,102,130,80,130,62.5);
	    ctx.bezierCurveTo(130,62.5,130,25,100,25);
	    ctx.bezierCurveTo(85,25,75,37,75,40);
	    ctx.fill();
	  }
	}
	draw();
</script>
##3.题外话(装个x)

![](./linus.jpg)
>Linus Benedict Torvalds

>他想写个操作系统，就写出了**Linux**

>他嫌合并世界各地提交的代码太麻烦，就写出了**Git**

>他说Just For Fun

>做你感兴趣的

<script type="text/javascript">
	var pHeight = document.body.scrollHeight;
	var cHeight = pHeight/3;
	var obj = document.getElementsByTagName('body');
	var test = function(e) {
		e = e || window.event;
		var nowTop = document.body.scrollTop;
		if(nowTop > 0) {
			obj[0].className = "";
			obj[0].className = "body-style-0";
		}
		if(nowTop > cHeight) {
			//obj[0].style.backgroundColor = "black";
			obj[0].className = "";
			obj[0].className = "body-style-1";
		}
		if(nowTop > 2*cHeight) {
			obj[0].className = "";
			obj[0].className = "body-style-2";
		}
	}
	if(document.addEventListener) {
		document.addEventListener('DOMMouseScroll', test, false);
	}
	window.onmousewheel = test;
</script>