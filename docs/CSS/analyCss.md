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