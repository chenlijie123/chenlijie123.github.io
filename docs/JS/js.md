## 数据类型

> typeof操作符 检测基本结构类型 判断一个变量是否为原始类型 null返回Object

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

getFullYear年 getMonth月 getDate日 getDay周几 getTime/valueOf当前时间戳 getHours小时 getMinutes分 getSeconds秒 getMilliseconds毫秒 

> ios端 getTime() 兼容 y-m-d 转换为y/m/d

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
#### 转换
```

```