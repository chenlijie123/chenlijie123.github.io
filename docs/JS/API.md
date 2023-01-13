## 数组 API

#### 静态方法

- Array.isArray() 返回布尔值，表示是否为数组

#### 实例方法

- valueOf() 所有对象都拥有的方法，对对象求值，数组的 valueOf 方法返回数组本身

- toString() 所有对象通用方法，数组的 toString 返回字符串数组

- push() 数组末尾添加项，返回添加后的数组长度

- pop() 数组末尾删除项，返回删除的项

- shift 数组首位删除，返回首位删除的项

- unshift 数组首位添加项，返回添加后的数组长度

- join() 数组转字符串，不传分隔参数，默认逗号分隔

- concat() 数组的合并

- reverse() 数组翻转

- slice() 数组截取返回截取项 无参数全部截取，参数 1 为截取起点，参数 2 为截取终点，不包含终点位

- splice() 删除、截取、替换 参数(起始位，删除个数，替换内容) 返回删除项

- sort() 数组排序 可传入对比函数 function(a,b){ return a - b }

- map(function(elem，index，arr){ return }，回调函数内部 this 指向对象 ) 跳过空位,返回执行结果组成的新数组

```map
  let arr1 = []
  [2,4,6,8,10,,12,undefined,14,null,,16].map(function(elem,index,arr){
    // elem 每一项 index索引 arr数组本身

    this.push(elem * 2) // this为arr1 等同于 arr1.push(elem * 2)
    return elem * 2

  },arr1) // 回调函数内部this指向了arr1
  // [4, 8, 12, 16, 20, empty, 24, NaN, 28, 0, empty, 32]
```

- forEach(function(elem,index,arr){},回调内部 this 指向对象) 跳过空位,没有的返回值

- filter(function(elem,index,arr){},this 指向的对象) 返回满足条件项组成的的数组

```filter
let obj = {
  MAX : 3
}
[2,4,5,7,9,0,,null,undefined,23].filter(function(elem,index,arr){
  if(elem > this.MAX) return elem
},obj)

//  [4, 5, 7, 9, 23]
```

- some(function) 一项满足条件返回 true every() 每一项满足返回 true

- reduce(function(prev,cur,index,arr){},初始值)

- reduceRight(function(prev,cur,index,arr){},初始值) 从后往前

```
let arr1 = [1,2,3,4,5,6,7,8,9,10]
  let total =  arr1.reduce(function(prev,cur,index,arr){
    // prev 数组第一个成员，有初始值时为初始值
    // cur 数组第二个成员，有初始值时为数组第一个成员
    // index, cur的索引位
    // arr 数组本身
      return prev + cur
    },10)
 console.log(total) // 65

//
```

- indexOf(查找项，起始位) 查找数组中是否存在某项，存在返所在索引位，不存在返-1

- lastIndexOf(查找项，起始位) 查找某项在数组中最后存在的位置，存在返索引不存在-1


## Number API

#### 实例方法

> 123.实例方法 报错 .被解析成小数点  应该用() 或者 ..

- toString() 数值转字符串

```
 234.toString() // 报错 .被解析成小数点，没解析成属性调用

 (234).toString()  // '234'

 234..toString()  // '234'
```
 
- toFixed()  先返回指定数小数，四舍五入，再转成字符串

- toExponential() 将数字转为科学计数法形式 (10).toExponential() // '1e+1'

## 字符串 API

#### 实例方法

- charAt(位置) 返回指定位字符 类似于根据下标返回对应项

```
'abcdefghig'.charAt(2) // 'c'
'abcdefghig'[2] // 'c'

'abcdefghig'.charAt(20) // ''
'abcdefghig'[20] // undefined

```

- charCodeAt(位置) 返回对应的unicode码

- concat 合并

- slice(开始位，结束位) 截取，负数从后面开始

- substring(开始，结束) 截取，负数转0

- substr(开始位，长度) 截取

- indexOf() 查找字符第一次出现位置，返索引 不存在返-1

- lastindexOf() 查找最后一次出现位置，返索引，不存在返-1  

- trim() 去除两端空格

- toLowerCase() 字符转小写

- toUpperCase() 字符转大写

- match() '查找内容' 返数组 ['fgh', index: 3, input: 'asdfgh'] 找不到返null

- search() 类似match 返回第一个找到的索引位置，找不到返-1

- replace('查找项'，'替换项') 替换找到的字符， 可用正则

- split() 字符分割返回字符组成的数组

## Math 

#### 静态方法

- Math.abs() 绝对值 
- Math.ceil() 向上取整 
- Math.floor() 向下取整
- Math.max() 最大值
- Math.min() 最小值
- Math.pow() 幂运算
- Math.sqrt() 平方根
- Math.round() 四舍五入
- Math.random() 0-1之间伪随机数 可能等于0，一定小于1

## Date 对象

#### Date 静态方法

- Date.now() 返回当前时间距离时间零点的毫秒数

- Date.parse() 解析日期字符串，返回改时间距离时间零点的的毫秒数

#### 实例方法

Date的实例对象除了valueOf 和 toString 还可以分为三类  
- `to`类：从Date对象返回一个字符串，表示时间
- `get`类：获取Date对象的日期和时间
- `set`类：设置Date对象的日期和时间

#### 节流函数

```
  throttle(fn,time=1000) {
    let flag = true // 设置开关
    return function() { // 返回函数
      if(!false) return false // 开关关闭 阻止执行
      flag = false // 关闭开关

     // fn.apply(this,arguments) 立即执行

      setTimeout(()=>{
        flag = true // 打开开关
      //  fn.apply(this,arguments)  延期执行
      },time)
    }
  }
```