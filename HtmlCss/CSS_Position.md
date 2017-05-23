## CSS关于定位的一些知识点
__绝对定位(absolute):__将被定位的对象从文档流中拖出，使用trbl属性控制对象，相对于一个最接近的有定位设置的父级对象进行定位。(会完全脱离文档流)
> 但是如果没有设置trbl值，则会变成一个特殊的存在，变成一个浮动元素，且比float更彻底，失去高宽属性。
定位后的对象可重叠，通过z-index属性控制。

__相对定位(relative):__通过trbl属性相对于对象本来的位置来定位，可以通过z-index来重叠。