## flutter中的视图数据的组织和渲染抽象
> flutter在视图中的核心概念有三个：**Widget**、**Element**、**RenderObject**。  


 为了便于理解，可以与vue中的相应概念进行类比。  

 flutter: Widget -> Element -> RenderObject  
 vue: template -> virtual DOM -> DOM  
 React：JSX -> virtual DOM -> DOM  


 Flutter 渲染过程，分三步：
 - 通过Widget树生成对应的Element树；
 - 创建相应的RenderObject并关联到Element.renderObject属性上；
 - 构建成RenderObject树，完成最终渲染。

Flutter 采用深度优先机制遍历渲染对象，确定树中各个对象的位置和尺寸，并把它们绘制到不同的图层上。绘制完毕后，合成和渲染的工作则交给Skia搞定。


对于Element的创建，Flutter会在遍历Widget树时，调用createElement去同步Widget自身配置，从而生成对应节点的Element对象。而对于RenderObject的创建与更新，其实是在RenderObjectElement类中完成的。
```dart
abstract class RenderObjectElement extends Element {
  RenderObject _renderObject;

  @override
  void mount(Element parent, dynamic newSlot) {
    super.mount(parent, newSlot);
    _renderObject = widget.createRenderObject(this);
    attachRenderObject(newSlot);
    _dirty = false;
  }
   
  @override
  void update(covariant RenderObjectWidget newWidget) {
    super.update(newWidget);
    widget.updateRenderObject(this, renderObject);
    _dirty = false;
  }
  ...
}
```