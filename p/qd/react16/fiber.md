# Fiber
> Reconciler(协调器)的最小更新单元

#### 本质上使用的是代数效应
> 代数效应的意思就是将副作用从函数调用中分离出来。

#### 实现原理

1. 静态数据结构属性

```js
// Fiber对应组件的类型 Function/Class/Host...
this.tag = tag;
// key属性
this.key = key;
// 大部分情况同type，某些情况不同，比如FunctionComponent使用React.memo包裹
this.elementType = null;
// 对于 FunctionComponent，指函数本身，对于ClassComponent，指class，对于HostComponent，指DOM节点tagName
this.type = null;
// Fiber对应的真实DOM节点
this.stateNode = null;
```
2. 连接其他Fiber节点形成Fiber树

> 节点执行完completeWork后会返回的下一个节点。子Fiber节点及其兄弟节点完成工作后会返回其父级节点，所以用return指代父级节点。

```js
// 指向父级Fiber节点
this.return = null;
// 指向子Fiber节点
this.child = null;
// 指向右边第一个兄弟Fiber节点
this.sibling = null;
```
3. 动态工作单元属性

```js
// 保存本次更新造成的状态改变相关信息
this.pendingProps = pendingProps;
this.memoizedProps = null;
this.updateQueue = null;
this.memoizedState = null;
this.dependencies = null;

this.mode = mode;

// 保存本次更新会造成的DOM操作
this.effectTag = NoEffect;
this.nextEffect = null;

this.firstEffect = null;
this.lastEffect = null;

// 调度优先级相关
this.lanes = NoLanes;
this.childLanes = NoLanes;
```

#### 工作原理
##### 双缓存Fiber树
> 在内存中构建并直接替换的技术


```js
currentFiber.alternate === workInProgressFiber;
workInProgressFiber.alternate === currentFiber;
```


## 参考资料
- [React技术揭秘](https://react.iamkasong.com/)