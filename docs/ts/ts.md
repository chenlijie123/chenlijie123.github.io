## 安装

```
  // 安装全局ts
  npm install -g typescript

  // 运行hellow.ts 文件 生成  hellow.js
  tsc hellow.ts 

```

## 简介

#### 原始数据类型 

1. number let age : number = 13 || let age: number = Number(123)
2. string let name: strign = '123
3. boolean let  boo : boolean = Boolean(123)
4. viod 空值 只能赋值 null undefined
5. null、undefined 所有类型的子集 let num: number = null / undefined

####  任意类型 any

> 声明一个变量为任意类型之后，对他的任意操作，返回的内容的的类型都是任意值
```
// 普通类型

let myFavoriteNumber: string = 'seven';
myFavoriteNumber = 7;
// index.ts(2,1): error TS2322: Type 'number' is not assignable to type 'string'.

// 任意类型

let myFavoriteNumber: any = 'seven';
myFavoriteNumber = 7;
// 不会报错

```
#### 类型推论 

> 如果定义的时候没有赋值，会推论成any类型

```
let myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
// index.ts(2,1): error TS2322: Type 'number' is not assignable to type 'string'.

let myFavoriteNumber;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
```

#### 联合推论
> 定义多个类型

```
    let myFavoriteNumber: string | number;
    myFavoriteNumber = 'seven';
    myFavoriteNumber = 7;
```
> 当不确定联合类型的变量为哪个类型时，只能访问此联合类型的所有类型里共有的方法或属性

```
function getLength(something: string | number): number {
    return something.length;
}
// index.ts(2,22): error TS2339: Property 'length' does not exist on type 'string | number'.
//   Property 'length' does not exist on type 'number'.

function getString(something: string | number): string {
    return something.toString();
}
```

> 联合类型的变量在被赋值的时候，会根据推论的规则推断出一个类型

```
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
console.log(myFavoriteNumber.length); // 5
myFavoriteNumber = 7;
console.log(myFavoriteNumber.length); // 编译时报错

// index.ts(5,30): error TS2339: Property 'length' does not exist on type 'number'.
```
#### 对象类型 -- 接口

```
  interface Person {
    name:string,
    age:number
  }

  let person: Person = {
    name:'1111',
    age:222
  }

  interface ClassName {
    name:string,
    age:number,
    readonly id: number, // 只读属性 约束存在第一次给对象赋值，而不是给只读属性赋值
    six? : string  // ? 可选属性

    [propName: string]: number // 定义所有属性名为string 值为number
    [propName: number] : any // 一旦定义为任意属性， 那么确定和可选属性必须是它的类型的子集
  }
```
#### 数组类型

```
  let arr : number[] = [123] // 类型 + []
  let arr: Array<number> = [123] // 数组泛型

  interface NumberArray { // 接口表示
    [index:number]:number
  } 

  let arr: NumberArray = [1,2,3,4]
```


#### 函数类型


```
// 函数声明


function (x: number, y:string): number | string {
  return x + y
}

// 函数表达式

let mySum = function

```
