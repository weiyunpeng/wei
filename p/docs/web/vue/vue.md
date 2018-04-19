## 解析模板😂
```
- 模板就是一段字符串，非结构化的数据，没法分析。因此，第一步是将非结构化的模板字符串，转变成结构化的 JS 对象，抽象语法树，即 AST 。其实就是一个 JS 对象，这样就结构化了。

- 第二步，将 AST 转换成一个 render 函数，步骤是先转换为一段函数体的字符串，然后再用new Function(...)生成函数。

- 第三部，渲染时执行 render 函数，返回虚拟 DOM 对象，然后执行虚拟 DOM 的patch方法，渲染成真正的 html 。
```

## virtual DOM  

virtual DOM实现的三个步骤：
```
createElement().用javascript对象（虚拟树）描述真实的DOM对象（真是树）;

diff(oldNode,newNode).对比新旧两个虚拟树的区别，收集差异;

patch().将差异应用到真实的DOM树;
```

## [vue中点击空白处隐藏div的实现（用指令优雅的实现）](./20180419.md)
