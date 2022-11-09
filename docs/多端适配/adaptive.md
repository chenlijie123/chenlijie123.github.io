## 大屏可视化多端适配

#### rem


- css3引入的大小单位，相对根元素html的font-size大小

通过配置项目入口文件 APP.vue 文件监听窗口大小 动态改变根元素html的font-size大小   
vw/vh = 1920/1080

```
resetFont(){
  let bascSize = 16 // 基准大小
  let basePC = baseSize/1920 // 放大、缩小比例vw/1920 = rem/16px  => 16/1920 = rem / vw  => rem = vw * (16/1920)
  let vw = window.innerWidht // 视口宽度
  let vh = window.innerHeight  // 视口高度
  // rem = vw * basePC 标准1920宽度对应font-size大小

  // 非标准尺寸换算
  let deh = (vw * 1080) /1920 // vw对应1920/1080的标准尺寸，实际应该的视口高度  
  if(vh < deh) { // 如果实际高度小于 vw对应的标准高度，则重新计算vw对应的标准视口宽度，从新计算font-size
  vw = (vh * 1920) / 1080
  }

  document.documentElement.style.fontSize = vw * basePC

  // 监听视口变化重新计算font-Size
  window.onresize = ()=> {
    this.resetFont()
  }
}
```
#### transform: scale()

```
function resize() {
  var ratioX = $(window).width() / 1920; //此处的宽高根据自己屏幕的比例修改即可
  var ratioY = $(window).height() / 1080;
  $("body").css({
      transform: "scale(" + ratioX + "," + ratioY + ")",
      transformOrigin: "left top",
      backgroundSize: "100% 100%"
  });
  $("html").css({'overflow':'hidden'})

```

#### 插件 postcss-plugin-px2rem lib-flexible

```
yarn add lib-flexible
 
yarn add postcss-plugin-px2rem --dev

// vue.config.js 配置
css: {
      loaderOptions: {
          postcss: {
              plugins: [
                  require('postcss-plugin-px2rem')({
                       rootValue: 100, //换算基数， 默认100  ，这样的话把根标签的字体规定为1rem为50px,这样就可以从设计稿上量出多少个px直接在代码中写多上px了。
                      unitPrecision: 5, //允许REM单位增长到的十进制数字。
                      propWhiteList: [],  //默认值是一个空数组，这意味着禁用白名单并启用所有属性。
                      propBlackList: [], //黑名单
                      exclude: /(node_module)/,  //默认false，可以（reg）利用正则表达式排除某些文件夹的方法，例如/(node_module)/ 。如果想把前端UI框架内的px也转换成rem，请把此属性设为默认值
                      selectorBlackList: [], //要忽略并保留为px的选择器
                      ignoreIdentifier: false,  //（boolean/string）忽略单个属性的方法，启用ignoreidentifier后，replace将自动设置为true。
                      replace: true, // （布尔值）替换包含REM的规则，而不是添加回退。
                      mediaQuery: false,  //（布尔值）允许在媒体查询中转换px。
                      minPixelValue: 3 //设置要替换的最小像素值(3px会被转rem)。 默认 0
                  }),
              ]
          }
      }
  },

// main.js 引入lib-flexible
import 'amfe-flexible'

```