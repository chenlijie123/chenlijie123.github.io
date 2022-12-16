## \<script> 标签

script 通过 src 找到对应 js 文件加载、执行，同时 html 不会向下解析，直到 js 执行完成，阻塞到 html，同时 JS 操作 dom 元素会找不到，dom 元素还未加载。

- src 加载外部文件
  // defer async 只有 src 加载外部文件时有效
- defer 属性 脚本会延迟到整个页面都解析完成后再执行（解析 html、下载脚本，当 html 解析完成才执行脚本）
- async 属性 脚本加载同时 html 解析，脚本加载完成直接执行，html 停止解析

js 的引入方式 ： 1.在 html 中 书写在<script></script>内部 2.通过 script 的 src 引入，书写在 body 底部防止阻塞 html 解析。

noscript 指定在不支持脚本的浏览器下替换展示的内容，可以代替 body 内的任何标签，不包含 script 标签。

#### 变量

松散类型，用来保存任何类型数据，关键字+标识符 定义了一个未初始化的变量 赋值 undefined
变量是有作用域的，函数内部设置的变量，在函数执行退出后就会被销毁，当省略 var 直接定义变量就会提升为全区变量

## 数据类型

基本数据类型 null undefined Number String Boolean 基本类型值在内存中占固定大小的空间，因此被保存在栈内存中  
复杂数据类型 Object 引用类型的值是对象，保存在堆内存中，包含引用类型值的变量实际是包含的不是对象本身，而是一个指向该对象的指针

类型检测 typeof() 这是一个操作符不是函数 ，括号可要可不要
对象或 null 检测 返回 Object 类型 ，因为特殊值 null 会被认定为空的对象引用

```
 let massage // massage 声明未定义
 // let name 未声明
 typeof massage // undefined
 typeof name // undefined
```

无论是声明还是未声明 typeof 都返回 undefined，严格来讲两个变量存在根本性差异，但他们都无法执行实际操作

#### 检测数据类型

> typeof (检测基本类型值)

```
function fn() {}
typeof(123) // Number
typeof('123') // String
typeof(true) // Boolean
typeof(null) // Object
typeof fn // function
```

> instanceof (用来检测具体的对象类型)

```
let arr = [1,2,3]
let obj = {}
function fn (){}
arr instanceof Array // true  arr.__proto__ == Array.prototype
arr instanceof Object // true  arr.__proto__.__proto__ == Object.prototype
obj instanceof Object // true
fn instanceof Object // true

// instanceof 检测原理 原型链对比 arr.__proto__ == Array.prototype
```

再续

#### 数值转换

NaN 是否为数值 检测 isNaN() 检测传入的值是否能转换数值， 不能转化数字返回 true
转换规则：基于对象调用 isNaN()函数，先调用 valueOf()方法，返回值是否可转换为数值，如果不能，再调用 toString(),在测试返回值

isNaN(String) // 传入字符，先把字符转换数字在判断是不是 NaN

```
 isNaN('hello') // == isNaN( Number('hellow')) == isNaN(NaN) == true
 isNaN('123') // == isNaN( Number('123')) == isNaN( 123 ) == false

 isNaN({}) // true
 // 等同于
 isNaN(Number({})) // true

 isNaN(['xzy']) // true
 // 等同于
 isNaN(Number(['xzy'])) // true

```

Number() 'undefined' // NaN null // 0  
字符数字返回十进制，前导零会忽略，含有十六进制 0xf，转十进制，空为零  
parseInt()取整 查找非空字符，如若第一个字符不是数字或负号，返回 NaN, 第二参数可为进制数(2 到 36 之间)  
// parseInt 转换规则 先转换字符串，在查找是否是数字不是数字就停止， 所以结果要么是十进制数字要么 NaN  
parseFloat() 只解析十进制，解析字符返回浮点数 空字符返回 NaN  
String  
字符字面量(转义序列) \n 换行 \r 回车 \' \"  
任何字符都可访问 length 属性，字符串是不可变的，一旦创建值不可变，改变某个变量保存的字符，首先要销毁原来的，然后再用另一个包含新值的字符串填充该变量

转换字符串  
toString() null nudefined 没有此方法，一般不用传参数，可以传递输出数值的基数，返回二进制、八进制、十六进制字符串  
不知要转换的值是不是 null undefined，用 String()函数转换任何类型值为字符串

Object 对象

通过 new 操作符后面加要创建的对象类型名称 创建自定义对象 let v = new Object()  
Object 的每个实例都具有下列属性和方法

constructor: 保存用于创建当前对象函数，构造函数(constructor)就是 Object()

hasOwnProperty: 用于检测给定的属性在当前对象实例中是否存在。参数属性名必须以字符串形式 如：O.hasOwnProperty('name')

isPropertyOf(object) 用于检测传入的对象是否是当前对象的原型

toLocaleString() 返回对象的字符串表示，该字符串与执行环境的地区对相应

toString() 返回对象的字符表示

valueOf() 返回对象的字符串、数值或布尔值表示，通常与 toString()返回值相同

## 强制转换 
#### Number() 原始类型

- 数值 --> Number(213) //213
- 字符 --> NUmber('12z') // NaN Number('123') // 123
- 空字符 --> Number('') // 0
- 布尔值 --> Number(true) // 1 false // 0
- undefined --> Number(undefined) // NaN
- null --> Number(null) // 0

> parseint('234ab') // 234  区别于  Number('234ab') // NaN

Number() 引用类型对象

- Number({a:1}) // NaN
- Number([1,2,3]) // NaN
- Number([5]) // 5

#### Number() 转换对象规则

第一步：调用对象自身的 valueOf(),返回原始类型直接 Number()，不再进行后续步骤  
第二步：如果 valueOf 返回还是对象，改用调用对象自身的 toString()方法，返回原始类型数据直接 Number 转换，返回对象就报错

```
var obj={ a:1 }
Number(obj) // NaN

// 等同于
if( typeof obj.valueOf() === 'object'){  // 判断第一步调用对象自身valueOf 是否返回object
  Number(obj.toString())  // valueOf返回对象，调用对象自身toString
}else {
  NUmber(obj.valueof()) // valueOf返回基础类型 直接Number() 转换
}

// 默认情况下对象的valueOf() 返回对象本身, toString() 返回对象类型字符串 '[object object]'

Number({}) // NaN
{}.valueOf() // {}
{}.toString() // '[object object]'
Number('[object object]') // NaN

Number([]) // 0
[].valueOf() // []
[].toString() // ''
Number('') // 0
```

#### String() 原始类型

- String(123/'123'/true/undefined/null) 原始类型值全部转为字符串 '123'/'123'/'true'/'undefined'/'null'

#### Strign() 引用类型 对象

与 Number()转换类似，只是互换了 valueOf 和 toString 的顺序

第一步：调用对象自身的 toString(),如果返回原始类型直接 String()  
第二步：如果返回对象，调用对象自身的 valueOf()，返回原始类型 String()转换，返回对象报错

```
String({})
{}.toString() // '[object object]'

String([])
[].toString() // '' 空
String('') // ''空
```

强制更改 toString()返回的结果

```
 var obj ={
  valueOf:function() { return 3 },
  toString: function() { return {} }
 }

String(obj)
obj.toString() // {} 返回对象时调用对象自身valueOf()
obj.valueOf() // '3'  返回对象报错，返回原始类型调用String('3')
```

#### Boolean()

Boolean() 转换规则较为简单 除了以下五个值返回 false，其余都为 true

> 另外所有对象布尔值都为 true

- undefined // false
- null // false
- NaN // false
- 0 // 包含 -0 +0 false
- '' // false

```
Boolean(true) // true
BOOlean(false) // false

```

## 自动转换(隐式转换)

待续

## 错误机制处理

#### Error 实例对象
- message 错误提示信息
- name 错误的名称（非标准属性）
- stack 错误的堆栈（非标准属性）

```
var err = new Errow('错误信息')
err.message // '错误信息'

```

#### 原生错误类型
- SyntaxError 对象 解析时语法错误

````
// 变量名错误
var 1a;
// Uncaught SyntaxError: Invalid or unexpected token

// 缺少括号
console.log 'hello');
// Uncaught SyntaxError: Unexpected string
````

- ReferenceError对象 引用一个不存在的变量时发生的错误

```
// 使用一个不存在的变量
unknownVariable
// Uncaught ReferenceError: unknownVariable is not defined

```

- RangeError对象 一个值超出范围时发生的错误

```
// 数组长度不得为负数
new Array(-1)
// Uncaught RangeError: Invalid array length
```

- TypeError对象 对象是变量或者参数不是预期类型时发生的错误

```
new 123
// Uncaught TypeError: 123 is not a constructor

var obj = {};
obj.unknownMethod()
// Uncaught TypeError: obj.unknownMethod is not a function

```

- URIError对象 URI相关函数的参数不正确时抛出的错误

```
decodeURI('%2')
// URIError: URI malformed
```

#### throw语句
作用为手动中断程序执行并抛出错误

```
var x = -1

if(x <= 0) {
  throw new Error('x 必须为正数')
}
// Uncaught Error: x 必须为正数
```

#### try...catch结构 
对错误捕捉并选择是否往下执行

```
try{
  throw new Error('出错了')
}catch(e){
  console.log(e)
}
// '出错了'
// try 出错，catch捕获到错误e

try{
  代码块;
}catch(e){
  // 出错时的错误处理
}.finally{
  // catch 代码块结束之前会先执行finally代码块
}

```


## 操作符

- 一元操作符：只能操作一个值 ++ -- 前置（先自增后运算）、后置（先运算后自增）
- == != 操作符 ，比较前 先转换操作数 强制转换在比较相等 null == undefined // true NaN == NaN // false

```
// 相等运行 不强制转换为数字
 null == 0 // false
 undefined == 0 // false
 null == undefined // true null/undefined 或者自身相比为true

// 关系运算符 强制Number() 转换 Number(null) 0  Number(undefined) NaN
 null >= 0 // true
 undefined >= 0 // false

```

- === 全等 两个操作数在未转换情况下就相等时返回 true
- !== 不全等 两个操作数在不转换前就不相等时 返回 true
- 条件操作符 ? :
- 赋值 = 复合赋值 += -= \*= /= %=
- 逗号 ， 一条语句执行多个操作 let num1 = 1 ，num2 = 2 赋值 num = (1,2,3,4) num = 4 最后一项

## 语句

- if(){} else if(){} else {}

- do{}while() 后测试循环语句 代码块执行完后才测试条件

```
do{
 i += 2
}while(i < 10)

// i < 10 执行i += 2， 至少执行一次

```

- while() {} 前测试循环语句 while（条件） {代码块}

```
var i = 0
while(i<10){
 i +=2
}
```

- for(){} 前测试循环 ，具备执行前初始化变量和定义循环后要执行的代码能力

```
for(var i=0; i<10 ; i++){ // 初始化表达式 控制表达式 循环后表达式  全部省略会创造无限循环 for(; ;){}
 代码块
}
```

- for-in 精准迭代的语句 可枚举对象的属性 因对象的属性没有顺序，因此 for-in
  循环输出属性名顺序不可预测

- break 立即退出循环 continue 退出当前循环，从循环顶部继续执行 return 退出函数打断循环

```
for(let i=0; i<10;i++) {
  if(i == 3) break // 跳出当前所在整个循环，如果是循环嵌套break处在内部循环就只能跳出内部循环
  if(i == 3) continue // 跳出本次循环，返回循环结构的头部，开始下次循环
  if(i == 3) return // Uncaught SyntaxError: Illegal return statement
  // return 跳出函数，for循环要处在函数内部，才会打断循环
}

 // 命名外层循环

one：
   for (let i = 0; i < 10; i++) {
        for (let j = 0; j < 10; j++) {
           if(j == 3) break one //跳出 名为one的循环体
        }
      }
```

- with 将代码作用域设置到一个特定的对象中

```
let qs = location.search.substring(1)
let hostName = location.hostname
let url = location.href
// with 固定作用域给特定对象
with(loaction){
  let qs = search.substring(1)
  let hostName = hostname
  let url = href
}
```

- switch

```
 switch(expression) {
  case value: 代码块  // expression === value 全等 执行代码块 break跳出循环
    break;
  case value1：
  case value2: 代码块 // 多个case合并，只要满足一个执行代码块
    break;
  case value: 代码块 // value 可以为常量、变量、表达式
    break;
  default 代码块 // expression都不满足value 执行默认default 代码块
 }

```

## 函数

- 封装多条语句，任意地方调用
  关键字 function 函数名 一组参数(arg0,arg1...) 函数体{} function fn(arg0,arg1) { }

- Function 关键字
  function fn(){}

- 函数表达式
  var fn = function () {}

- 构造函数
  var fn = new Function()

同一个函数多次被声明，后面的会覆盖前面的声明

```
 function fn() {
  console.log(1)
 }

 fn() // 2

function fn() {
  console.log(2)
 }

 fn() // 2

 // 后一次的函数声明覆盖了前面一次。而且，由于函数名的提升,前一次声明是无效的
```

- 函数名的提升

```
f();

function f() {} // 不会报错
```

```
fn()
var fn = function() {} // 报错

等同于
var fn // 声明未赋值 undefined
fn() // 报错
fn = funtion() {}

```

> 如果同时采用 function 命令和赋值语句同时声明一个函数，最后采用的是赋值语句的定义

```
var f = function () {
  console.log('1');
}

function f() {
  console.log('2');
}

f() // 1
```

> 变量提升与函数提升以及优先级

变量提升

```
console.log(str)
var str= '123'
console.log(str)

解析

var str // 声明str
console.log(str) // undefined
str = '123' // str赋值
console.log(str) // '123'
```

函数提升 ：只有函数式声明才会存在函数提升

```
 function foo(){} 解析 var foo = function() {}


 console.log(bar)
 console.log(bar())
 var bar = 456
 function bar (){
  consele.log(123)
 }
 console.log(bar)
 bar = 123
 console.log(bar)
 console.log(bar())

 解析

 var bar = function(){ console.log() }

```

#### 参数

- 同名参数 取后面的

```
function f(a,a) {
  console.log(a)
}

f(1,2) // 2
f(1) // undefined

```

- arguments 对象 包含函数运行时所有参数，只在函数内部使用
  与数组关系 arguments 很像数组，其实是对象，数组专有的方法不能直接使用，要先转换成数组

```
 var args = Array.protoType.slice.call(arguments)

 或者

 var args = []
 arguments.forEach(item=>{
  args.push(item)
 })
```

#### 闭包

闭包最大的特点就是可以记住它诞生的环境

- 读取其他函数内部变量

```
function f1() {
  var n=999
  function f2() {
    console.log(n)
  }
  return f2()
}
f1() // 999 f2就相当于闭包
```

- 让变量始终保存在内存中

```
function inc(start) {
  return function() {
    return start ++
  }
  }
  var ins = inc(5)
console.log(ins()); // 5
console.log(ins()); // 6
console.log(ins()); // 7

```

#### 垃圾回收

执行环境负责管理代码执行过程使用的内存，自动分配、释放内存。  
原理就是找出不在继续使用的变量，释放占用的内存，垃圾收集器会按照固定的间隔时间周期执行这一操作

- 标记清除
  当变量进入环境(在函数内声明一个变量)时，变量标记进入环境，不能释放变量占用的内存，当离开环境（函数调用结束）销毁释放内存。 垃圾收集器会给内存中变量添加标记，然后去掉环境中的变量以及被环境中变量引用的变量的标记。在此之后再被加上标记的变量将视为准备删除的变量，因为环境中的变量已经无法访问到这些变量，垃圾收集器完成内存清除工作，销毁那些带标记的值并回收他们占用的空间。

- 引用计数法
  当声明一个变量并将一个引用类型值赋值给该变量时，这个值的引用次数为 1，同一个值又赋值给另一个变量引用次数加一反之减一，当引用次数为零时，将其占用的内存回收。  
  缺点 互相引用 引用次数永远不会为 0，大量内存得不到回收，转而采用标记清除法

```
 function fn() {
  var 0bjA = new Object()
  var objB = new Object()

  objA.someOtherObject = objB
  objB.anOtherObject = objA
 }
```

#### 内存泄漏、内存溢出

- 内存泄漏：无法释放申请的内存，导致内存不够用，最后内存溢出
- 内存溢出：申请内存时，没有足够内存提供给申请者使用，导致数据无法正常存储到内存中，内存溢出
- 关系： 内存泄漏最终会导致内存溢出
- 区别：泄漏( 无法识别可回收数据进行及时回收，导致内存浪费) 溢出 (需要的内存无法满足，导致数据无法正常存储到内存中)

## 对象

某个特定引用类型的实例。新对象是使用 new 操作符后跟一个构造函数来创建的。  
var person = new Object()  
构造函数 Object 创建新的实例，存放在 person 中，为新对象定义默认的属性和方法

#### Object

创建： 构造函数 var person = new Object() 字面量 var person = {}

> 转换方法 toLocaleString()、toString()、valueOf()

所有对象都具有 toLocaleString()、toString()、valueOf() 方法，valueOf 返回的还是数组本身，toString 会返回由数组中每个值以逗号分割组成的字符串，显示调用数组的 toString()，其实就是调用数组每一项的 toString()方法，toLocaleString()经常返回与 toString()和 valueOf()方法相同的结果，但是实际调用的是数组每一项的 toLocalString()方法

对象方法有两类，一种是Object本身的方法，一种是Object的实例方法  

对象属性描述
```
{
  value: undefined , //  属性值 默认undefined
  writable：true, // 属性值是否可改变
  enumerable:true, // 属性是否可遍历
  configurable：true // 表示属性的的可配置性
  get：undefined， // 表示该属性的取值函数（getter），默认为undefined
  set: undefined // 表示该属性的存值函数（setter），默认为undefined
}
```
## 数组

- 数组本质为特殊对象 length 属性，返回成员数量，键名为次序排列的整数，非字符串键名自动转为字符串

```
  var arr = ['a','b','c']
  Object.keys(arr) // ['0','1','2']
```

- length 属性

```
// 删除
var arr= ['a','b','c']
arr.length // 3

arr.length = 2
arr //['a','b']


```

- 空位

```
var a = [1,,1]
a.length // 3
a[1] // undefined
// 数组的空位是可以读取的，并且不会影响length长度

delete 可以删除一个数组成员，形成空位

delete a[2]
a // [1,,,] // [1,empty,empty]
```

- in forEach for...in... while

```
// in 检查键名是否存在的运算符

var arr = [1,2,3]
2 in arr // true

for...in 不仅遍历数组的数字键，还会遍历非数字键，所以不推荐使用
```

- 空位与 undefined 的区别
  遍历数组是会忽略空位，undefined 不会

- 类似数组的对象（对象的所有键名是正整数或零，并且具备 length 属性）例如 arguments 对象、string 字符串、大多数 DOM 元素集

```
 var args = (function (a,b) {return arguments }('a','b,','c','d'))

 args.length // 4
 args instanceof Object // true
```

- 类数组对象转数组 Array.prototype.slice.call()

```
 var arr = Array.prototype.slice.call(类数组)

 // 除了转为新数组，类数组对象还可以通过call（）使用数组方法，把数组方法绑定到对象上面

 // forEach 方法
 function logArgs(){
   Array.prototype.forEach.call(arguments,function (ele,i) {
     console.log( i + '.' + ele)
   })
 }
 // 在arguments对象上调用forEach方法 等同于

 function logArgs(){
   for(var i=0;i<arguments.length;i++) {
     console.log(i + '.' + arguments[i])
   }
 }

 // 字符串

 var str = Array.prototype.slice.call('abc')
 str.forEach(function(ele){
   console.log(ele)
 })
 // a
 // b
 // c

 // 或者

 function logStr() {
   Array.prototype.forEach.call('abc',function(ele,i){
     console.log(i + '--' + ele)
   })
 }
 logStr()
 // 0 -- a
 // 1 -- b
 // 2 -- c

```

## 本地存储

#### localStorage sessionStorage

localStorage 长久有效的本地存储，只能存储字符串格式数据，大小 5MB，扩展了 cookie 的 4k
sessionStorage 会话结束时清空数据

> localStorage sessionStorage API

- setItem('key','value') 设置 JSON 格式数据 value = JSON.stringify(value)
- getItem('key') 获取 JSON 格式的字符串 JSON.parse(localStorage.getItem('key'))
- removeItem('key') 删除
- clear() 全部清空
- key(n) 获取第 n 个 key 名
- length 获取键值对数量有多少

```
  const info = ['13xx', 188, null, undefined, false, [123, 22, '44']]
  localStorage.setItem(infoName,JSON.stringify(info))
  const strVal = localStorage.getItem('infoName')
  const str = JSON.parse(strVal)
  console.log(typeof str, str) //  object (6) ['13xx', 188, null, null, false, Array(3)]
```

#### lockr 轻量级库 与 localStorage 的交互

```
  npm i lockr --s
```

或者

```
  <script src="https://raw.githubusercontent.com/tsironis/lockr/master/lockr.js" type="text/javascript"></script>
```

```
  import Lockr from 'lockr'

  const info = ['13xx', 188, null, undefined, false, [123, 22, '44']]
  Lockr.set('infoName',info)
  arr = Lockr.get('infoName')
  console.log(typeof arr, arr) //  object (6) ['13xx', 188, null, null, false, Array(3)]

  Arr = JSON.parse(localStorage.getItem('infoName))
  console.log( typeof Arr,Arr)
  object {data: (6) ['13xx', 188, null, null, false, Array(3)]}
```

- set('key',value) 设置 value => 类型可以是 String/Number/Array/Object
- get('key') 获取 key 对应的 value
- prefix 给添加的 key 键添加前缀锁

```
 lockr.prefix('lockr')
 lockr.set('info',123321)
 lockr.get('info') // 123321

 localStorage.getItem('info') //null
 localStorage.getItem('lockrinfo') // '{"data":123321}'
```

- rm('key') 删除
- sadd('key',val) 在 key 对应的 value 原有的基础上，往末尾添加 val
- sismember('key',val) 判断 key 对应的 value，val 是否在 value 中存在 true/false 不支持数组、对象的查找
- srem('key', val) key 对应的 value 值，移除 value 内的 val 值 ，不支持数组、对象
- getAll() 获取全部的 localStorage 数据
