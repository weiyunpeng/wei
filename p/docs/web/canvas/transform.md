### drawImage方法
> Canvas API 允许将图像文件插入画布，做法是读取图片后，使用drawImage方法在画布内进行重绘。

```
var image = new Image();

image.onload = function() {
  var canvas = document.createElement('canvas');
  canvas.width = image.width;
  canvas.height = image.height;
  canvas.getContext('2d').drawImage(image, 0, 0);
  // 插入页面底部
  document.body.appendChild(image);
  return canvas;
}

image.src = 'image.png';
```
### getImageData方法，putImageData方法
> getImageData方法可以用来读取Canvas的内容，返回一个对象，包含了每个像素的信息。

```
imageData对象有一个data属性，它的值是一个一维数组。
该数组的值，依次是每个像素的红、绿、蓝、alpha通道值，因此该数组的长度等于 图像的像素宽度 x 图像的像素高度 x 4，每个值的范围是0–255。
这个数组不仅可读，而且可写，因此通过操作这个数组的值，就可以达到操作图像的目的。
修改这个数组以后，使用putImageData方法将数组内容重新绘制在Canvas上。

var imageData = context.getImageData(0, 0, canvas.width, canvas.height);
context.putImageData(imageData, 0, 0);
```

### toDataURL方法
> 对图像数据做出修改以后，可以使用toDataURL方法，将Canvas数据重新转化成一般的图像文件形式。

```
function convertCanvasToImage(canvas) {
  var image = new Image();
  image.src = canvas.toDataURL('image/png');
  return image;
}
```

### 图形变换

- 位移 translate( x , y )
- 旋转 rotate( deg )
- 缩放 scale( sx , sy )

对于每一段图形的变幻需要进行状态的保存和恢复
```
save()

restore()
```

### 变换矩阵  

$$
\\
\begin{bmatrix}
a & c & e \\\\
b & d & f \\\\
0& 0 & 1
\end{bmatrix}
\\
$$
a 水平缩放 ( 1 )  
b 水平倾斜 ( 0 )  
c 垂直倾斜 ( 0 )  
d 垂直缩放 ( 1 )  
e 水平位移 ( 0 )  
f  垂直位移 ( 0 )  

其实可以理解为一个单位矩阵 ：
$$
\\
\begin{bmatrix}
1 & 0 & 0 \\\\
0 & 1 & 0 \\\\
0& 0 & 1
\end{bmatrix}
\\
$$