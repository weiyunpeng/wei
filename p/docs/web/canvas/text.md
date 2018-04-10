## 绘制文本

> fillText(string, x, y) 用来绘制文本，它的三个参数分别为文本内容、起点的x坐标、y坐标。
> 使用之前，需用font设置字体、大小、样式（写法类似与CSS的font属性）。与此类似的还有strokeText方法，用来添加空心字。


```
// 设置字体
ctx.font = "Bold 20px Arial"; 
// 设置对齐方式
ctx.textAlign = "left";
// 设置填充颜色
ctx.fillStyle = "#008600"; 
// 设置字体内容，以及在画布上的位置
ctx.fillText("Hello!", 10, 50); 
// 绘制空心字
ctx.strokeText("Hello!", 10, 100); 
```