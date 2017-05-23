# 常用知识
#### echo()
>可以一次输出多个值，多个值之间用逗号分开。echo是语言结构，不是真正的函数，不能作为表达式的一部分使用。


#### print()
>函数print()打印一个值，成功则返回true，否则返回false。


#### pring_r()
>输出布尔值与null没有意义，输出数组会以键和值列表形式显示，并以Array开头。


#### var_dump()
>判断一个变量的类型与长度，并输出变量数值，如果变量有值则输出值并返回变量类型。


#### mysql 更改密码
>set password for 'root'@'localhost'=password('');

#### 更改phpmyadmin密码
>打开phpmyadmin安装目录，找到config.inc.php更改`$cfg['Servers'][$i][password]=;`

#### include与require的区别
- 它们的作用是基本相同的，不同点在于，`require`是在程序开头，程序一开始就会加载，而`include`则是程序运行到`include`的位置才会加载。
- 后者是过程型的，`include`是条件包含型，而`require`是无条件包含函数`require`如果出现在条件语句中，无论条件是否满足，都将执行，而`include`则会在满足条件是才会执行。
- 此外，两者失败报错也不一样，`require`如果失败会报出致命错误，程序将无法继续执行，而`include`则只会是普通错误，程序会继续执行，所以如果是加载比较重要的脚本推荐使用`require`，而加载html脚本则推荐使用`include`，循环加载的也需要使用过程型的`include`。
    
