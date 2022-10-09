## 选择器

#### css2.1

基本选择器

| 序号 | 选择器 | 含义                |
| ---- | :----- | ------------------- |
| 1    | \*     | 通用选择器 匹配全部 |
| 2    | E      | 标签/元素选择符     |
| 3    | .      | class/类选择符      |
| 4    | #      | id 选择符           |

多元素组合选择器

| 序号 | 选择器 | 含义                                       |
| ---- | :----- | ------------------------------------------ |
| 5    | E,F    | 多元、群组选择器                           |
| 6    | E F    | 后代选择符 匹配所有 E 元素内部的所有元素 F |
| 7    | E > F  | 子选择符 匹配所有 E 元素的子元素 F         |
| 8    | E + F  | 相邻选择符 匹配 E 元素之后的同级元素 F     |

猫头鹰选择符 * + * 选中有着相同父级的非第一个子元素的其他元素
```
 .parent > * + * {
  margin-left: 30px; // 类名parent元素，除第一个子元素的其他子元素添加了左边距30px
 }
 // 类似于
 .parent > div + div {
  margin-left: 30px; // parent 除第一个div的其他div加外边距30px
 }
```
属性选择符

| 序号 | 选择器       | 含义                                                                             |
| ---- | ------------ | -------------------------------------------------------------------------------- |
| 9    | E[att]       | 匹配所有具有 att 属性的 E 元素 （E 可以省略 例如[att]）                          |
| 10   | E[att=val]   | 匹配所有 att 属性等于 val 的 E 元素                                              |
| 11   | E[att~=val]  | 匹配所有 att 属性具有多个空格分隔的值 其中一个为 val 的元素                      |
| 12   | E[att\|=val] | 匹配所有 att 属性 具有多个连字符号分隔的值（hy-tit-value） 其中一个值以 val 开头 |

伪类选择符

| 序号 | 选择符        | 含义                         |
| ---- | :------------ | ---------------------------- |
| 13   | E:first-child | E 元素的第一个子元素         |
| 14   | E:link        | 未被点击的链接               |
| 15   | E:visited     | 已点击的链接                 |
| 16   | E:hover       | 鼠标经过悬停                 |
| 17   | E:active      | 鼠标按下、还未释放 E 元素    |
| 18   | E:focus       | 匹配获取当前焦点的 E 元素    |
| 19   | E:lang(c)     | 匹配 lang 属性为 c 的 E 元素 |

伪元素

| 选择器         | 含义                  |
| :------------- | --------------------- |
| E:before       | 在 E 元素之前插入内容 |
| E:after        | 在 E 元素之后插入内容 |
| E:first-line   | 匹配 E 元素的第一行   |
| E:first-letter | 匹配 E 元素第一个字母 |

---

#### CSS3

同级元素通用选择器

| 选择器 | 含义                               |
| :----- | ---------------------------------- |
| E ~ F  | 匹配任何在 E 元素之后的同级 F 元素 |

属性选择器

| 选择器        | 含义                               |
| :------------ | ---------------------------------- |
| E[att^="val"] | 属性 att 以 val 开头的             |
| E[att$="val"] | 属性 att 以 val 结尾的             |
| E[att*="val"] | 属性 att 的值包含 val 字符串的元素 |

CSS3 中与用户界面有关的伪类

| 选择器       | 含义                          |
| :----------- | ----------------------------- |
| E:enabled    | 匹配表单中激活的元素          |
| E:disabled   | 匹配表单中禁用的元素          |
| E:checked    | 匹配表单中被选中的 radio 元素 |
| E::selection | 匹配用户当前选中的元素        |

CSS3 中的结构性伪类

| 选择器              | 含义                                                     |
| :------------------ | -------------------------------------------------------- |
| E:root              | 匹配文档的根元素，对于 HTML 文档 就是 HTML 元素          |
| E:nth-child(n)      | 匹配父元素的第 n 个子元素                                |
| E:nth-of-type(n)    | 与 nth-child 相似，但仅匹配同种标签的元素                |
| E:nth-last-child(n) | 匹配父元素的倒数第 n 个子元素                            |
| E:nth-last-of-type  | 同 nth-last-child 类似，但仅匹配相同标签的最后一个子元素 |
| E:last-child        | 匹配父元素最后一个子元素                                 |
| E:last-of-type      | 类似 last-child 但匹配同标签的最后一个子元素             |
| E:first-of-type     | 类似 nth-of-type(1) ,匹配同标签的第一个子元素            |
| E:only-child        | 匹配父元素下仅有的一个子元素                             |
| E:only-of-type      | 匹配父元素下同种标签的唯一一个子元素                     |
| E:empty             | 匹配一个不包含任何子元素的元素                           |

CSS3 中的反选伪类

| 选择器   | 含义                         |
| :------- | ---------------------------- |
| E:not(s) | 匹配不符合当前元素的任何元素 |

```
E:not(:first-child):not(:last-child) {
  text-align: center;
}
```

CSS3 中的:target 伪类

| 选择器   | 含义                                 |
| :------- | ------------------------------------ |
| E:target | 匹配文档中特定 id 的锚点激活后的效果 |
| :target  | 所有锚点激活后的效果                 |

```
<p><a href="#news1">跳转至内容 1</a></p>
<p><a href="#news2">跳转至内容 2</a></p>
<p>请点击上面的链接，:target 选择器会突出显示当前活动的 HTML 锚。</p>
<p id="news1"><b>内容 1...</b></p>
<p id="news2"><b>内容 2...</b></p>
<p><b>注释：</b> Internet Explorer 8 以及更早的版本不支持 :target 选择器。</p>

<style>
:target { //所有锚点
  border: 2px solid #D4D4D4;
  background-color: #e5eecc;
}

#news1:target { // id为news1的 锚点
  border: 2px solid #D4D4D4;
  background-color: #e5eecc;
}
</style>
```

---

## 背景与边框

#### 半透明边框

```
  background:#2468F1 ;
  border: 40rpx solid rgba(0, 0, 0, .1);
```

![边框透明时背景色渗透](_images/back-border.png)<br/>
当边框有透明度时，背景颜色会渗透到边框下

> 解决方法 - [background-clip] : content-box | padding-box

#### 背景图偏移

背景图偏移 根据 `background-origin` 决定 默认 padding-box

```
background-origin:padding-box | content-box | border-box
background-position: center | left top | calc(100% - 10px) calc(100hv - 10px) | left 20px top | left 20px top 20px
```

---

## 弹性盒 display: flex;

![弹性盒图片示例](_images/flex.png)

#### 容器的属性

- flex-direction 主轴方向 row（默认）| row-reverse | column | column-reverse
- flex-wrap 如何换行 nowrap（默认）| wrap 换行 | wrap-reverse 换行，第一行在下面
- flex-flow flex-direction 与 flex-wrap 缩写
- justify-content 项目在主轴的对齐方式 flex-start（默认） | flex-end | center | space-between | space-around
- align-items 项目在交叉轴上对其方式 flex-start | flex-end | center | baseline | stretch(默认值) 如果项目未设置高度，或者为 auto 将占满整个容器高度
- align-content 定义多根轴线对其方式 flex-start | flex-end |center | space-between | space-around | stretch (默认值) 占满整个交叉轴

#### 项目属性

- flex-grow 放大比例 默认为 0，即如果存在剩余空间，也不放大。
- flex-shrink 缩小比例, 默认 1 即如果空间不足，该项目将缩小。
- flex-basis 占据主轴的固定空间 默认 auto
- align-self 单个项目的对其方式 可覆盖 align-items 默认为 auto | flex-satrt | flex-end | center | baseline | stretch
- order 项目的排列 默认 0
- flex 由 flex-grow flex-shrink flex-basis 缩写( 1 0 auto )后两个属性可选 auto(1 1 auto) none(0 0 auto)

---

## 单位

> 绝对单位 px 像素点

> 相对单位 em rem 基于窗口的大小来等比例缩放字号

- 1em 等于当前元素的字号，其准确值取决于作用的元素,当元素字号不存在时，用元素继承的字号参与计算
- 1rem 等于根元素 html 字号大小（root em）

> 当拿不准使用什么单位时，rem 设字号，px 设边框 em 设边距以及其他的属性

```
box {
  font-size: 16px;
  padding: 1em; // 16px
}
// 计算想要的单位例如 20px
// 计算公式 20/ font-size: 16px = 1.25em

html{
  font-size：16px;
}
// 1rem 相当于16px 不收其他元素字号的影响
```

> 视口相对单位  vw vh 窗口的可视范围
当用视口设置字体时，可以平滑的过渡字

> css的 calc() 函数 可进行动态计算长度单位运算

- 任何长度都可以进行运算 width: calc(100% - 10px)
- 支持 + - * / 运算，运算符前后要留有空格

## 媒体查询

> @media 媒体类型(不写模式all) 媒体条件 { 执行的样式 }

媒体类型

|  类型  | 含义 |
| :----: | :--: |
| screen | 屏幕 |
| print  | 打印 |
|  all   | 所有媒体（默认值） |

媒体条件

|    条件     |             含义             |
| :---------: | :--------------------------: |
|    width    |     可加（min max）前缀      |
|   height    |     可加（min max）前缀      |
| orientation | portrait 竖屏/landscape 横屏 |

> 关键词 and组合  only指定样式(可兼容旧版本浏览器，旧版本没有only关键词所以不会执行)  not 排除指定条件，取反操作
```
  html {
    font-size:1em; // 16px
  }
 @media screen (max-width:900px){
  :root {
    font-size:0.625em // 屏幕小于900px时触发 根元素字号设为 10px
  }
 }
 
 @media (min-width:600px),handheld and (orientation:landscap) {
  :root {
    font-size:0.875rem;
  }
  // 逗号分割的媒体条件都被当做独立的查询，其中一个条件满足就会执行代码
  // and 关键词 将媒体特性结合在一起形成一个查询条件 
  // 屏幕大于600px 或者 是智能设备且横屏时 根元素字号设置14px
 } 
```
## 自定义属性( css变量 )

- 定义在代码块中(作用域)
- 以两个横杠开头 var()调用，第二个参数为默认值

```
:root {
  --border: 1px solid red;
  --main-font: 16px;
}
.box {
  font-size: var(--main-font); // 16px
  color: var(--color,blue); //--color未声明，取默认值blue
  border: var(--border); // 1px solid red
} 

```
## 边距折叠、失效

当盒子存在上下外边距时，上下盒子的边距会折叠(无论否同级盒子,子元素也会与外部盒子边距重叠)，以大的边距为准。

- 子元素重叠与外部相邻盒子重叠，外部盒子overflow:hidden/display:flex/重叠部位加padding
- disolay:table-cell, table-cell不具备外边距，所以不会外边距重叠(不推荐使用，改变盒子类型对布局有影响)

## 层叠

###### 冲突解决规则

- 样式来源
- 选择器优先级
- 代码顺序

#### inherit 继承 initial 重置

```
.fater {
  color: red;
}
.son {
  color: inherit; // 继承父元素color样式
}

.son {
  color: initial; // 重置color ，默认black
}
```

## 盒模型

宽度

```
box-sizing: content-box // 默认值 宽度表示内容
box-sizing: border-box // 宽度包含内边距和边框

```

高度百分比设置 要给父元素设置一个高度 才会起效

###### 等高列 css 表格 flexbox

并排盒子高度等高，一个改变，其他的盒子高度跟着改变

css 表格 display: table

```
 box{
  display:teble;
  border-spacing：单元格左右间距，单元格上下间距；
  box1{
    width:30%;
    display:table-call;
  }
  box2{
    width:70%;
    display:table-cell;
  }
 }
```
flexBox display:flex;

```
box {
  display:flex;
}
```

## 垂直居中

- vertical-align: middle 只影响行内元素或table-cell的对齐，对于行内元素内容忽略
- 容器高度不固定 用上下相同的内边距撑开盒子，使内容垂直居中
- disply：table-cell vertical-align:middle 内容垂直居中
- display: flex, align-items:center 垂直居中
- 只有文本，使用行高居中

## 布局 

> 浮动 初衷以实现文字围绕浮动元素、图片 

高度塌陷，浮动后元素脱离正常文档流，造成容器高度塌陷
- clear:both; 浮动元素后加div标签 设置clear属性，both全部清除，left清除左浮动，right清除右浮动
- 塌陷容器使用伪元素 ::after
```
 box::after{
  display:block; // 设块元素
  content：" "; // 让元素站位
  clear：both; // 清浮动
 }
```
> BFC 块级格式化上下文 独立区域与外部隔离

1. 包含内部所有的外边距，不会与bfc外部区域产生边距折叠
2. 包含内部所有的浮动元素，添加clear属性只会清除自身所在bfc内的浮动
3. 不会和bfc外的浮动元素重叠

成为bfc盒子的条件
- float：left或rigth 不为none即可
- overflow：hidden、auto、scroll，不为visible即可
- display 块级容器的属性
- position：absolute、fixed

## 定位与层叠上下文
  
  position：fixed // 固定定位，相对于视口位置  初始包含块为视口
  position：absolute // 绝对定位，相对于最近的包含块
  position：relative // 常用于给绝对定位创建一个包含块  
#### z-index

1、z-index只在定位元素上生效，不能控制静态元素
2、定位元素加z-index可以创建层叠上下文

层叠上下文：给一个定位元素加上z-index，就会变成一个新的层叠上下文的根(z-index:auto不会)，所有后代元素就是这个层叠上下文的一部分
`z-index：0` 与`z-index：auto` 同级，html后书写的在上面，auto不会生成新的层叠上下文

###### 排列顺序
- 层叠上下文的根
- z-index为负数的定位元素（及子元素）
- 非定位元素
- z-index为auto的定位元素（及子元素）
- z-index为正数的定位元素（及子元素）

#### 浏览器渲染过程
1、生成DOM树：解析html 根据文档定义创建DOM树
2、生成CSSOM树：解析CSS，生成CSSOM树
3、构建渲染树：将DOM树、CSSOM树构建成渲染树
4、布局阶段：浏览器计算布局（元素位置、大小），计算层级、图层绘制、合并，GPU绘制
5、绘制阶段：遍历渲染树，遇到script标签停止渲染，优先加载JS代码（JS线程和DOM渲染线程公用同一个线程，JS可能改变DOM结构，导致重绘）
6、DOM渲染完成

#### 粘性定位 position：sticky

粘性定位：相对定位和固定定位混合，跨越阈值前相对定位，阈值后固定定位
```
  position:sticky;
  top:10;

```
距离