## \<script> 标签 

script 通过src找到对应js文件加载、执行，同时html不会向下解析，直到js执行完成，阻塞到html，同时JS操作dom元素会找不到，dom元素还未加载。

- src 加载外部文件
// defer async 只有src加载外部文件时有效
- defer 属性  脚本会延迟到整个页面都解析完成后再执行（解析html、下载脚本，当html解析完成才执行脚本）
- async 属性  脚本加载同时html解析，脚本加载完成直接执行，html停止解析

js的引入方式 ： 1.在html中 书写在<script></script>内部 2.通过script的 src引入，书写在body底部防止阻塞html解析。

noscript 指定在不支持脚本的浏览器下替换展示的内容，可以代替body内的任何标签，不包含script标签。

#### 变量 

松散类型，用来保存任何类型数据，关键字+标识符 定义了一个未初始化的变量 赋值undefined
变量是有作用域的，函数内部设置的变量，在函数执行退出后就会被销毁，当省略var直接定义变量就会提升为全区变量

## 数据类型
基本数据类型 null undefined Number String Boolean 基本类型值在内存中占固定大小的空间，因此被保存在栈内存中  
复杂数据类型 Object 引用类型的值是对象，保存在堆内存中，包含引用类型值的变量实际是包含的不是对象本身，而是一个指向该对象的指针  

类型检测 typeof() 这是一个操作符不是函数 ，括号可要可不要
对象或null检测 返回 Object类型 ，因为特殊值 null 会被认定为空的对象引用
```
 let massage // massage 声明未定义 
 // let name 未声明
 typeof massage // undefined
 typeof name // undefined
```
无论是声明还是未声明 typeof 都返回undefined，严格来讲两个变量存在根本性差异，但他们都无法执行实际操作 

#### 数值转换 
NaN 是否为数值 检测isNaN() 检测传入的值是否能转换数值， 不能转化数字返回true
转换规则：基于对象调用isNaN()函数，先调用valueOf()方法，返回值是否可转换为数值，如果不能，再调用toString(),在测试返回值

Number() 'undefined' // NaN  null // 0   
字符数字返回十进制，前导零会忽略，含有十六进制0xf，转十进制，空为零  
parseInt()取整 查找非空字符，如若第一个字符不是数字或负号，返回NaN, 第二参数可为进制数  
parseFloat() 只解析十进制，解析字符返回浮点数  

String  
字符字面量(转义序列) \n 换行 \r 回车 \' \"  
任何字符都可访问length属性，字符串是不可变的，一旦创建值不可变，改变某个变量保存的字符，首先要销毁原来的，然后再用另一个包含新值的字符串填充该变量  

转换字符串  
toString() null nudefined 没有此方法，一般不用传参数，可以传递输出数值的基数，返回二进制、八进制、十六进制字符串  
不知要转换的值是不是null undefined，用String()函数转换任何类型值为字符串  


Object对象

通过new操作符后面加要创建的对象类型名称 创建自定义对象 let v = new Object()  
Object的每个实例都具有下列属性和方法  

constructor: 保存用于创建当前对象函数，构造函数(constructor)就是Object()  

hasOwnProperty: 用于检测给定的属性在当前对象实例中是否存在。参数属性名必须以字符串形式 如：O.hasOwnProperty('name')  

isPropertyOf(object) 用于检测传入的对象是否是当前对象的原型  

toLocaleString() 返回对象的字符串表示，该字符串与执行环境的地区对相应  

toString() 返回对象的字符表示  

valueOf() 返回对象的字符串、数值或布尔值表示，通常与toString()返回值相同

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
 - !== 不全等 两个操作数在不转换前就不相等时 返回true
 - 条件操作符  ?  :
 - 赋值 =   复合赋值 += -= *= /= %=
 - 逗号 ， 一条语句执行多个操作 let num1 = 1 ，num2 = 2  赋值 num = (1,2,3,4) num = 4 最后一项

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
 - for-in 精准迭代的语句 可枚举对象的属性 因对象的属性没有顺序，因此for-in
循环输出属性名顺序不可预测

- break 立即退出循环 continue退出当前循环，从循环顶部继续执行 

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
关键字function 函数名 一组参数(arg0,arg1...) 函数体{} function fn(arg0,arg1) { } 

#### 垃圾回收

执行环境负责管理代码执行过程使用的内存，自动分配、释放内存。  
原理就是找出不在继续使用的变量，释放占用的内存，垃圾收集器会按照固定的间隔时间周期执行这一操作  

- 标记清除 
当变量进入环境(在函数内声明一个变量)时，变量标记进入环境，不能释放变量占用的内存，当离开环境（函数调用结束）销毁释放内存。 垃圾收集器会给内存中变量添加标记，然后去掉环境中的变量以及被环境中变量引用的变量的标记。在此之后再被加上标记的变量将视为准备删除的变量，因为环境中的变量已经无法访问到这些变量，垃圾收集器完成内存清除工作，销毁那些带标记的值并回收他们占用的空间。

- 引用计数法 
 当声明一个变量并将一个引用类型值赋值给该变量时，这个值的引用次数为1，同一个值又赋值给另一个变量引用次数加一反之减一，当引用次数为零时，将其占用的内存回收。  
 ``` 
 // 缺点 互相引用 引用次数永远不会为0，大量内存得不到回收，转而采用标记清除法

 function fn() {
  var 0bjA = new Object()
  var objB = new Object()

  objA.someOtherObject = objB
  objB.anOtherObject = objA
 }

 ```
#### 内存泄漏、内存溢出

内存泄漏：无法释放申请的内存，导致内存不够用，最后内存溢出  
内存溢出：申请内存时，没有足够内存提供给申请者使用，导致数据无法正常存储到内存中，内存溢出  
关系： 内存泄漏最终会导致内存溢出  
区别：泄漏( 无法识别可回收数据进行及时回收，导致内存浪费) 溢出 (需要的内存无法满足，导致数据无法正常存储到内存中)

## 对象

某个特定引用类型的实例。新对象是使用new操作符后跟一个构造函数来创建的。  
var person = new Object()  
构造函数Object 创建新的实例，存放在person中，为新对象定义默认的属性和方法  

#### Object

创建： 构造函数 var person = new Object() 字面量 var person = {}