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

#### 数据类型
基本数据类型 null undefined Number String Boolean 
复杂数据类型 Object 

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

#### 操作符 
一元操作符：只能操作一个值 ++ -- 前置（先自增后运算）、后置（先运算后自增） 