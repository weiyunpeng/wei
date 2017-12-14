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