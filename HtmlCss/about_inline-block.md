# about——inline-block元素

原生`inline-block`元素与其他标签通过`display`转化过来的元素都会有默认间隙处理间隙的方式:  
1. 去除标签段之间的空格，**标签之间换行会产生间隙**
```
<div class="space">
	<a href="##">
	哈哈</a><a href="##">
	呵呵</a><a href="##">
	嘻嘻</a>
</div>

```
