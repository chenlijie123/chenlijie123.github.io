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