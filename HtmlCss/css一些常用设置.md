# css使背景图片全屏
```
body {
		background:url('image/background.jpg');
		background-size: 100% 100%;
		background-repeat: no-repeat;
		background-attachment: fixed;
	}
.bg {
	background-image:url(scale.jpg);
	-moz-background-size: 100% 100%; /*  Firefox 3.6 */
	-o-background-size: 100% 100%;/* Opera 9.5 */
	-webkit-background-size: 100% 100%;/* Safari 3.0 */
	background-size: 100% 100%;/*  Firefox 4.0 and other CSS3-compliant browsers */
	-moz-border-image: url(scale.jpg) 0; /* Firefox 3.5 */
	filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='scale.jpg', sizingMethod='scale');/* for < ie9 */
	}
```
__img标签__
```
	<img class="stock" style="position: absolute; top: 0px; left: 0px; height: 100%; width: 100%;" src="default.jpg">

```
# div水平居中方法
```
	text-align: center;
	margin-left: auto;
	margin-right: auto;
```
# css图片中心放大
```
	transition: all 0.3s;
	transform: scale(1.1, 1.1);
```
