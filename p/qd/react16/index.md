# React理念
> 践行构件大型web应用

### 主要遇到两个问题
- CPU瓶颈
- IO瓶颈

### 解决原理
```md
将同步的更新变成可中断的异步更新，并且可以根据优先级进行调整
```

### 解决方法
> 使用三层架构

- Scheduler(调度器) -- 根据任务的优先级调度任务
- Reconciler(协调器) -- 负责找出变化的组件
- Renderer(渲染器) -- 将变化的组件渲染到页面上

##### [Scheduler(调度器)](https://github.com/facebook/react/blob/1fb18e22ae66fdb1dc127347e169e73948778e5a/packages/scheduler/README.md)


核心在于根据浏览器的剩余刷新时间作为标准来控制任务是否继续进行。  


> 浏览器的刷新频率（60Hz）,即每16.6ms浏览器刷新一次。（1000ms/60Hz = 16.6 ms/Hz））

#### [Reconciler(协调器)](https://github.com/facebook/react/tree/1fb18e22ae66fdb1dc127347e169e73948778e5a/packages/react-reconciler)

核心在于执行一个可中断的过程（基础的就是每次执行判断下当前剩余时间是否够用），并为变化的虚拟DOM打上增/删/改的标记。

> Scheduler(调度器)与Reconciler(协调器)都是在内存中执行的。当所有组件都执行完Reconciler(协调器)之后，才统一交给Renderer(渲染器)执行。
> 因为除了会在浏览器运行，还会在更多比如app等平台上运行，因此react把这Scheduler(调度器)和reconciler(协调器)单独发了一个包[react-reconciler](https://www.npmjs.com/package/react-reconciler)

#### Renderer(渲染器)

渲染器就是把Reconciler(协调器)标记后的虚拟DOM（React16叫Fiber）进行同步执行DOM的操作，因为平台多样性，不展开描述。

### 思维发散
> 这三层架构在工作合作中的使用

其实对于一个公司，一个产品本质上都可以用类似的方式去做：
1. 首先由决策的人想清楚要做什么，什么是重要的，什么是不重要的可以往后面排的，也就是根据任务的优先级调度任务。
2. 决策着排好以后中间需要可以协调的人根据任务的优先级以及时间的多少变成实际可行的方案。
3. 最后把方案内容交给一线去实现。

而学习历练的过程刚好反过来：
1. 先在一线学会完成任务。
2. 然后是接到任务能标记出哪些需要做哪些需要怎么做。
3. 最后是能看明白哪些工作优先级最高，并排出合理的优先级。



## 参考资料
- [React技术揭秘](https://react.iamkasong.com/)