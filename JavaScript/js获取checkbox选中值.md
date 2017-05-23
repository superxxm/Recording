# js获取checkbox选中值
```
var obj = document.getElementsByName("interest");//选择所有name="interest"的对象，返回数组      
var s='';//如果这样定义var s;变量s中会默认被赋个null值  
for(var i=0;i<obj.length;i++){  
     if(obj[i].checked) //取到对象数组后，我们来循环检测它是不是被选中  
     s+=obj[i].value+',';   //如果选中，将value添加到变量s中      
}  
```
