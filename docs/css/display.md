## 弹性盒 display: flex;

#### 容器的属性
- flex-direction 主轴方向  row（默认）| row-reverse | column | column-reverse
- flex-wrap 如何换行  nowrap（默认）| wrap 换行 | wrap-reverse 换行，第一行在下面
- flex-flow flex-direction与flex-wrap 缩写 
- justify-content 项目在主轴的对齐方式 flex-start（默认） | flex-end | center | space-between | space-around  
- align-items项目在交叉轴上对其方式 flex-start | flex-end | center | baseline | stretch(默认值) 如果项目未设置高度，或者为auto 将占满整个容器高度
- align-content 定义多根轴线对其方式 flex-start | flex-end |center | space-between | space-around | stretch (默认值) 占满整个交叉轴

#### 项目属性
- flex-grow 放大比例 默认为0，即如果存在剩余空间，也不放大。
- flex-shrink 缩小比例, 默认1 即如果空间不足，该项目将缩小。
- flex-basis 占据主轴的固定空间 默认auto
- align-self 单个项目的对其方式 可覆盖 align-items 默认为auto
