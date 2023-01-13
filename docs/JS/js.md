## 数据类型

> typeof 操作符 检测基本结构类型 判断一个变量是否为原始类型 null 返回 Object

`instanceof`

```
person instanceof Object // person 是不是 Object  true/false
```

#### Object

```
let O = new Object();
hasOwnProperty 判断当前对象实例上是否存在给定的属性   O.hasOwnProperty('name')
isPrototypeOf 判断当前对象是否为另一个对象的原型
toString() 返回对象的字符串
valueOf() 返回对象对应的字符串、数值或布尔值表示
```

## 循环

> while do...while for for...in for...of

```
while(expression) {} // 未定义变量初始值
do{}while(expression) // 先执行一遍代码块在判断条件
for(){} // 可以定义变量的初始值
for(const i in obj){} //遍历对象的属性 数组的索引
for(const i of arr){} //遍历数组的每项元素
break 退出循环，执行下一条代码
continue 退出循环，从循环体头部再次执行代码
```

#### 标签语句

```
label : statement
start: for(let i=0; i<count; i++){
  console.log('i',i)
}
// 循环嵌套结合break使用

start:
for(let i=0; i<10;i++){
  for(let j=0;j<10;j++){
    if(j>5){
      break start
    }
  }
}
```

#### with

将代码作用域设置给特定对象

```
let qs=location.search.subString(1)
let hostName=location.hostName
let url=location.href

<!-- with改写 -->
with (location) {
  let qs=search.subString(1)
  let hostName = hostName
  let url= href
}

```

#### switch

```
switch(i){
  case 1:
    console.log('11')
    break;
  case 2:
    console.log('22')
    break;
  default:
    console.log('default')
}
```

## Date

#### new Date()

getFullYear 年 getMonth 月 getDate 日 getDay 周几 getTime/valueOf 当前时间戳 getHours 小时 getMinutes 分 getSeconds 秒 getMilliseconds 毫秒

> ios 端 getTime() 兼容 y-m-d 转换为 y/m/d

```
new Date('yyyy-mm-dd',replace(/-/g,'/')).getTime()

new Date().tolocaleString() // 2022/9/16 17:13:12

new Date(new Date().toLocaleString()).getTime()
```

## String

- 截取

```
slice(开始位索引，结束位索引不含结束位，不存在截取到最后)
subStr(开始位索引，截取数量)
subString(开始位，结束位)
```

- 查找、替换、转换

```
indexOf('查找项'，开始位)  //从前面找满足条件的项，返回索引位
lastIndexOf('查找项'，开始位)  //从后面找满足条件的项，返回索引位
search(正则/查找项) // 返回索引位或-1
replace(匹配项，替换内容) // replace(/'匹配项'/g, '替换') 全局替换
split 字符转数组
charAt(num) 返回指定位置的字符
charCodeAt(num) 返回指定位的字符对应的Unicode值
```

- 包含

```
startsWith('包含项',开始索引位)  //是否以包含项开头 true/false
endsWith('包含项',开始结束位) // 以包含项结尾 true/false
includes('包含项'，开始索引位) // 是否存在包含项 true/false

```

- 其他方法

```
trim() //去除空格符
trimLeft() //左边开始
trimRigth() 右边开始
repeat(整数n) 复制n遍拼接在一起
// 扩展字符串到指定长度
let str = 'ccc'
padStart(6)  // '   ccc'
padStart(6,'ab')  // 'abaccc'
padEnd(6,'ab') // 'cccaba'
// 大小写转换
toLowerCase() // 字符串大写转小写
toLocaleLowerCase() // 根据本地计算机语言转换小写
toUpperCase() // 字符串转大写
toLocaleUpperCase() // 根据本地计算机语言转大写
```

## Math

```
Math.ceil() 向上取整
Math.floor() 向下取整
Math.round() 四舍五入
Math.random() 0-1之间随机数
abs 绝对值
```

## Array

> Array.from() 类数组转数组、数组深拷贝

```
// 改变原数组
shift() 删除第一项 返回删除的元素
pop() 删除最后一项 返回删除项
unshift() 首位添加一项 返回新数组长度
push() 添加最后项 返回新长度
sort() 数组排序
reverse() 反转
splice(开始位必填，删除几个选填/0，替换项item 选填) 删除、添加、替换

// 不改变原数组
concat() 合并
every() 检测每项是否满足条件 一项不满足返回false 不再进行检测 ，都满足返回true
some（） 一项满足返回true 都不满足false
filter（）创建新数组 由满足条件的项组成的新数组
map（）返回新数组 由处理后的每项组成的
slice（开始位索引，结束位索引 ）// 返回截取指定项 不包含结束位，无结束位则截取到最后
join（分隔符） 转字符串
reduce 求和
 let arr=[1,2,3,4,5,6]
 arr.reduce((初始值，当前元素，当前元素索引，当前元素对应的数组对象)=>{},传给函数的初始值)

```

- 断言函数

find 返回匹配的项 findIndex 返回匹配项的索引

```
findIndex 、find((匹配项，索引，数组本身)=>{ 匹配逻辑} ) // 查到后不会再对后面的项做匹配

```

## 事件

#### 事件模型

```
<div id="box">
  <button class="btn" onclick="btnClick()">事件函数方法一</button>
  <button class="button" id="targetID">事件函数方法二</button>
  <button class="btn" id="btnssss">事件函数方法三</button>
</div>
```

- 方案一 on + click
```
function btnClick(event){
  // 监听click事件
}
```

- 方案二 onclick 
```
let btn = document.querySelector('.button')
btn.onclick = function(event){
  // 监听click事件
}
```
- 方案三
```
let btn = document.querySelectorAll('.btn')[1]

btn.addEventListener(
  'click',
  function(event){
    // 监听click函数
  },
  {
    captrue:false, //冒泡时触发监听函数
    once: true // 只触发一次
  })
```
#### 事件传播

div -> botton 从上层到底层，捕获阶段  
botton 在目标节点上触发，目标阶段  
botton -> div 从底层回传到上层，冒泡阶段

```
target.addEventListener('事件类型'，监听函数，函数配置)

// capture:false 事件传播的冒泡阶段触发监听函数
// captrue:true 事件传播的捕获阶段触发监听函数


```
#### 事件代理 

> 事件传播中，冒泡阶段事件会上传到父节点，所以监听函数定义在父节点

```
 let box = document.querySelector('#box')

 box.addEventListener(
  'click',
  function(event) {
    // 监听函数

  },
  false
 )
 
  // event.stopPorpagation() // 阻止当前监听函数不再传播，不影响当前节点上其他监听函数

  // event.stopImmediatePropagation() // 彻底取消事件，不再触发后续的监听函数
```
#### 事件类型

- 鼠标事件 click mousedown mouseup dblclick 

监听事件触发顺序 mousedown mouseup click dblclick(双击最后触发)  


#### 移动事件

- mousemove 鼠标在节点内部移动触发，持续触发应该限制触发频率
- mouseenter 进入节点时触发，父节点内部进入子节点不会
- mouseover 进入节点触发，父节点内部进入子节点会再次触发
- mouseout 离开节点触发，父节点内部离开子节点会触发
- mouseleave 离开节点触发，父节点内部离开子节点不会触发

- contextmenu 鼠标右键触发
- wheel 鼠标滚轮触发

#### event位置属性

- offsetX offsetY 相对于点击元素左上角位置
- clientX clientY 相对于浏览器左上角位置
- screenX screenY 相对于显示屏左上角位置
- pageX pageY 相对于文档左上角位置

#### 文本 链接 图片 节点拖拽
> 节点拖拽必须设置 `draggable="true"`

- dragstart 拖拽开始
- dragend 拖拽结束
- drag 拖拽持续触发 默认间隔几百毫秒
- dragenter 拖拽进入节点触发
- dragover 拖拽到当前节点上时，当前节点持续触发
- dragleave 拖拽离开当前节点，当前节点触发

#### 窗口事件 

- scroll 滚动事件

- resize 窗口缩放事件