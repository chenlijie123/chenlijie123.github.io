#

## flutter

#### 基础组件

- Text

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Title Name',
      home: Scaffold(
        body: Center(
          child: Text(
            // '测试显示的内容测试显示的内容测试11显示的内容测试显示的内容测试显示的内容测试显示的内容测试显示的内容测试显示的内容测试显示的内容测试11显示的内容测试显示的内容测试显示的内容测试显示的内容测试显示的内容测试显示的内容测试显示的内容测试11显示的内容测试显示的内容测试显示的内容测试显示的内容测试显示的内容',
            '测试显示的内容测试显示my name xxx的内容测试11显示的内测试显示的内容测试显示的内容测试11显示的内',
            // 文本对齐方式（center居中，left左对齐，right右对齐，justfy两端对齐）
            // textAlign: TextAlign.right,
            // 文本方向（ltr从左至右，rtl从右至左）
            // textDirection: TextDirection.ltr,
            // 设置容量为2行
            // maxLines: 2,
            //文字超出屏幕之后的处理方式  TextOverflow.clip剪裁   .fade 渐隐  .ellipsis省略号
            // overflow: TextOverflow.ellipsis,

            style: TextStyle(
                // 设置字体样式
                // 大小
                fontSize: 20.0,
                // 字体颜色
                // color: Color.fromARGB(255, 255, 125, 125),
                // color: const Color(0xfff2c2b2),
                color: Colors.purpleAccent,
                //none无文字装饰，lineThrough删除线，overline文字上面显示线，underline文字下面显示线
                // decoration: TextDecoration.underline,
                // 文字装饰线颜色
                // decorationColor: Colors.red,
                // 修饰线类型
                // decorationStyle: TextDecorationStyle.dashed,
                // 文字加粗
                fontWeight: FontWeight.bold,
                // 文字倾斜、正常
                fontStyle: FontStyle.italic,
                // 字母间隙
                wordSpacing: 50.0),
          ),

          // text 组件添加点击事件
          child: GestureDetector(
            onTap: () {
              print('text 点击了按钮');
            },
            child: Text('text文案'),
          ),

          // text片段拼接
          child: Text.rich(
            new TextSpan(
              text: 'text片段1',
              style: TextStyle(color: Colors.red),
              children: [
                new TextSpan(
                  text: '片段2',
                  style: TextStyle(
                    fontWeight: FontWeight.bold,
                    color: Colors.purpleAccent,
                  ),
                ),
                new TextSpan(
                  text: '片段3',
                  style: TextStyle(
                    fontWeight: FontWeight.w200,
                    color: Colors.greenAccent,
                  ),
                ),
              ],
            ),
          ),
        ),
        // backgroundColor: Colors.grey,
      ),
    );
  }
}

```

- container

```
class BoxWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Text('container组件文案展示'),
      // 对齐方式
      // alignment: AlignmentDirectional.bottomStart,
      // 装饰样式
      decoration: BoxDecoration(
        // 底色与图片 形成滤镜模式
        // backgroundBlendMode:
        // 底色背景色
        color: Colors.lightBlue,
        // 边框样式
        // border: Border.all(
        //   width: 5,
        //   color: Colors.redAccent,
        // ),
        // border: Border(
        //   left: BorderSide(width: 4, color: Color.fromRGBO(0, 0, 0, 1)),
        //   bottom: BorderSide(width: 4, color: Color.fromRGBO(125, 0, 0, 1)),
        // ),
        // border 圆角
        // borderRadius: BorderRadius.circular(20),
        borderRadius: BorderRadius.all(Radius.circular(20)),
      ),
      width: 200,
      height: 200,
      padding: EdgeInsets.all(20),
      margin: EdgeInsets.all(10),
    );
  }
}
```
