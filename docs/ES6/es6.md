
## let 和 const 命令

- let 声明变量，类似 var, 区别 有作用域，不存在变量提升，同作用域不可重复声明
- const 声明常量 ，常量值不可改变，有作用域，不存在变量提升，同作用域不可重复声明
- 暂时性死区（TDZ）let 声明变量之前，该变量都不可用，否则报错 ReferenceError

## 解构赋值

#### 数组的解构赋值

```
let [a, [b], c] = [1, [2], 3]
a // 1
b // 2
c // 3
```

```
let [a,,c]= [1,2,3]
a // 1
c // 3
```

```
let [a, ...b] = [1,2,3,4,5]
a // 1
b // [2,3,4,5]
```

```
let [a, b] = [1]
a // 1
b // unddfined
```

```
let [a, b] = [1,2,3] //不完全解构
a // 1
b // 2
```

```
let [a, [b], d] = [1, [2, 3], 4] //不完全解构
a // 1
b // 2
d // 4
```

#### 默认值

```
let [a=1] = []
a // 1
```

> 解构允许默认值，使用严格相等运算符（===），判断一个位置是否有值，只有当一个数组成员严格相等 undefined，默认值才会有效

```
let [a = 1] = [undefined]
a // 1
let [a = 1] = [null]
a // null
```

> 默认值为表达式，惰性求值

```
function f() {
  console.log('aaa')
}
let [a = f()] = [1]
a // 1 a对应位置能取到值所以不会执行函数
```

> 默认值可以引用解构赋值的其他变量,但该变量必须已经声明

```
let [x = 1, y = x] = []   // x=1 ,y=1
let [x = 1, y = x] = [2]  // x=2,y=2
let [x = 1, y = x] = [1, 2] // x=1,y=2
let [x = y, y = 1] = [] // ReferenceError: y is not defined  x用y做默认值，y还未声明
```

#### 对象解构赋值

> 数组解构赋值是按照顺序位置，对象是根据属性名相同赋值

赋值机制 先找同名属性，在赋值给对应变量

```
let {foo , bar} = { foo:1 , bar:2} //foo:1,bar:2
let {foo:foo1, bar:bar1} = {foo:1,bar:2} // foo1:1,bar1:2 foo是匹配模式 foo1才是变量
```

#### 字符串解构赋值

```
const [a,b,c,d,e] = 'hello'  // 先转换成一个类似数组的对象
a // 'h'
b // 'e'
c // 'l'
d // 'l'
e // 'o'

let {length：len} = 'hello' // len 5
```
#### 函数解构赋值
```
function add([x, y]){
  return x + y;
}
add([1, 2]); // 3

[[1, 2], [3, 4]].map(([a, b]) => a + b);
// [ 3, 7 ]

function move({x = 0, y = 0} = {}) {
  return [x, y];
}
move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]
```

## 字符串扩展

#### 模板字符串 ``

 `${变量}`  `空格 保留  ` 

#### 新方法
> indexOf 查找新方法
```
let s = 'hello world'
includes('查找项',开始位置)  
startsWith('查找项'，开始位)
endsWith('查找项'，前n个字符)
```
> repeat方法返回一个新字符串，表示将原字符串重复n次。padStart() padEnd() 补全
```
'x'.repeat(3) // 'xxx'
'x'.padStart(5,'ab') // ababx
'x'.padEnd(5,'ab') // xabab
 ```
> at() 返回索引位对应的字符

