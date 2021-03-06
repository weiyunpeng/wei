## 关于vue和react使用总结
>没有最好的只有比较合适的

### 从业务开选

- 项目偏前端重视觉交互，界面设计和交互体验的，vue的数据双向绑定和符合切图仔的写法呈现方式会提高不少效率。
- 项目偏业务重逻辑和可控性，react的函数式编程以及数据的手动更新会更严谨一些。


### 从研发人手来选

这里直接从diff算法里来窥斑见豹吧，目前来看vue的diff性能要比react高。

#### vue  
Vue2的核心Diff算法采用了双端比较的算法，同时从新旧children的两端开始进行比较，借助key值找到可复用的节点，再进行相关操作。相比React的Diff算法，同样情况下可以减少移动节点次数，减少不必要的性能损耗，更加的优雅。
Vue3.x借鉴了 ivi算法和 inferno算法。在创建VNode时就确定其类型，以及在mount/patch的过程中采用位运算来判断一个VNode的类型，在这个基础之上再配合核心的Diff算法，使得性能上较Vue2.x有了提升。(该算法中还运用了动态规划的思想求解最长递归子序列)

#### react
react做了三个策略 

1. 策略一（tree diff）:

 - 对树分层，同层对比。这里vue和react一样映射到开发功能的时候主要就是确保key的唯一性。
 - 夸层级只有删除和创建。这里映射到开发功能的时候就是对于某些功能的显示与隐藏选择用true/false还是hidden。

2. 策略二（component diff）:
 - 同类组件，当两个组件没变化的时候走策略一，当有变化的时候react需要手动使用shouldComponentUpdate来判断,而vue是根据算法自动处理的。
 - 不同类组件，那就是直接替换。

3. 策略三（element diff）

 - 从左往右依次对比，利用元素的index和标识lastIndex进行比较，如果满足index < lastIndex就移动元素，删除和添加则各自按照规则调整；当一个集合把最后一个节点移动到最前面，react会把前面的节点依次向后移动，而Vue只会把最后一个节点放在最前面，这样的操作来看，Vue的diff性能是高于react的。

>综上所述，当人手比较新或者偏ui的时候选vue上手成本和开发效率相对较高。当人手比较成熟老练而且偏后端的时候选react你会觉得更可控。