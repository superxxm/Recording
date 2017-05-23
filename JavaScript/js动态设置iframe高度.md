#js动态设置iframe高度
```
<iframe src="default.html" id="mainweb" name="mainweb" width="100%" height="100%" frameborder="0"  onLoad="iFrameHeight()" ></iframe>
	<script type="text/javascript" language="javascript">
		function iFrameHeight() {
			var ifm= document.getElementById("mainweb");
			var subWeb = document.frames ? document.frames["mainweb"].document :
			ifm.contentDocument;
			if(ifm != null && subWeb != null) {
				ifm.height = subWeb.body.scrollHeight;
			}
		}
	</script>
```
`documetn.frames` 在chrome中需要经过http协议才能获取，在本地无法获取，会显示undefine。
