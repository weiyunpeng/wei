## virtual DOM  

virtual DOM实现的三个步骤：
```
createElement().用javascript对象（虚拟树）描述真实的DOM对象（真是树）;

diff(oldNode,newNode).对比新旧两个虚拟树的区别，收集差异;

patch().将差异应用到真实的DOM树;
```