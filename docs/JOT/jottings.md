#### export与export default区别

- export与export default都可以导出常亮、函数、模块等
- 通过 import 引入
- 在一个文件中 export import有多个 export default只能有一个
- 通过`export`导出 导入时要用 {} 包裹，且不能自定义名称，`export defaule`导出，引入时不用{}，并且可以自定义名字

> export
```
// one.js
export const a='aaaa'
export function calc(a,b) {
  return a+b
}

// two.vue
import {a,calc} from 'one.js'

created(){
  console.log(a)
  calc(10,15)
}
```

> export defaule

```
// one.js
export default const a = 'bbbbb'

// two.vue
import b from 'one.js'

created(){
  console.log(b) // 'bbbbb'
}
```
