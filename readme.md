

### Dart （iOS部门内部分享）

google的新的操作系统说起。

下面是wiki的说明
> Fuchsia是Google开发的操作系统。 和以前該公司开发的操作系统，如基于Linux内核的Chrome OS和Android等不同，Fuchsia基于新的名为Zircon的微内核，受Little Kernel启发，用于嵌入式系统，主要使用C语言和C++编写
>
>
> Fuchsia的用户界面与应用使用“Flutter”开发。
> 
> Flutter是一个能为Fuchsia、Android和iOS进行跨平台开发的开发框架，基于Dart创建应用

Google开发Fuchsia的原因：
过去10年一直由手机主导，下一个十年将是物联网(IoT)设备主导。

详细的原因（分享可略）：
> Fuchsia 基于 microkernel 微内核，小巧但功能强大。它最初由 Android 和 ChromeOS 所依赖的 Linux 提供支持，但谷歌现在正抛弃 Linux 并创建了一个能够在通用设备上运行的微内核操作系统 —— 从嵌入式和物联网设备到智能手机、平板电脑和个人电脑。他们的计划是在未来五年内在数十亿的物联网设备中安装 Fuchsia 。秘密武器是 Fuchsia 的用户界面和应用程序，都是用 Flutter 编写的。Flutter 不仅可以简化应用开发，而且被用于开发移动和物联网设备的未来操作系统。 Flutter 将极大地改善未来几年内部开发和初创公司的前景。

个人观点：

> 综上所述，基本上可以认为Dart这门语言是Android和Fuchsia平台上的官方语言。

Fuchsia官方我就不多说了
Android原因如下：

`Android` 源代码被发现添加`Fuchsia SDK` 和`Fuchsia`设备支持。意思就是`Android`上面可以运行Fuchsia的SDK了，加上`Flutter`本身就在`Android`的底层重构了UI层，所以可以猜测是为`Fuchsia OS`的正式推广做一个过渡期。（另外一个原因他们都有同一个爹Google。）

个人感慨：


作为安卓开发者，现在学会了`Java`，又学会了`kotlin`。

作为苹果开发者，学会了`OC`，又学会了`Swift`。

现在是需要又学习一下`Dart`了，主要是为下一代的操作系统做准备，也为现在的跨平台开发`Flutter SDK`做入门的准备。（前端是挺累的...）

（Flutter 这里就不展开说了）

|语言|排名|占比|
|---|---|---|
|Java|2|16.1%|
|Swift|11|1.46%|
|Objective-C|21|0.61%|
|Dart|25|0.47%|
|kotlin|30|0.45%|

(TIOBE 2020年5月份数据)

### [Dart的中文官方网址](https://dart.cn/)

### 1. 写给有其他语言基础的Dart快速入门

#### 1.1 Dart跟其他语言的一些对比点
###### 1.1.1 字符串插值
很多语言有插值

|字符串|值|
|---|---|
|'${3 + 2}'	| '5' |
|'${"word".toUpperCase()}'	 	|'WORD'|
|'$myObject'	| myObject.toString() 的值 |

###### 1.1.2 Dart的针对null的处理
首先说明一点`Dart`没有`Swift`中的可选类型(`optional`)，但是有相似的语法

- 避免空对象访问成员

```dart
//如果 myObject 或 myObject.someProperty 为空
// 则前面的代码返回 null（并不再调用 someMethod）。
//调用访问方法
myObject?.someProperty?.someMethod()

//调用访问属性
myObject?.someProperty
//相当于 (myObject != null) ? myObject.someProperty : null

```

- 操作避空 `??`

类似Swift的**解包**  和 避空赋值运算符

```dart
print(1 ?? 3); // <-- Prints 1.
print(null ?? 12); // <-- Prints 12.
```

```dart
int a; // The initial value of any object is null.
a ??= 3;
print(a); // <-- Prints 3.
a ??= 5;
print(a); // <-- Still prints 3.
```





###### 1.1.3 Dart的闭包

简短的闭包：只有一句话。采用`javascript ES6`箭头函数的写法

```dart
bool hasEmpty = aListOfStrings.any((s) {
  return s.isEmpty;
});
//使用箭头函数
bool hasEmpty = aListOfStrings.any((s) => s.isEmpty);
```

正常的闭包

```dart
(参数) {
    闭包实现
}

```

###### 1.4 Dart展开操作符

类似`Javascript`对象的展开操作

```dart
var list = [1, 2, 3];
var list2 = [0, ...list];
assert(list2.length == 4);
```

###### 1.5 Dart的异步操作
使用 `async` 和 `await`
详细的略，具体的去看`js`就行了

###### 1.6 Dart的扩展Extension
跟Swift差不多，但是语法上有点区别


#### 1.2 Dart有意思的一些特性点

###### 1.2.1 抓到了就按在地上摩擦 -- 级连

```dart
var button = querySelector('#confirm');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
```

可以变成如下的

```dart
querySelector('#confirm')
..text = 'Confirm'
..classes.add('important')
..onClick.listen((e) => window.alert('Confirmed!'));
```

###### 1.2.2 隐式接口
间接的实现了多继承
每一个类都隐式地定义了一个接口并实现了该接口，这个接口包含所有这个类的实例成员以及这个类所实现的其它接口。


#### 1.3 Dart必看点

###### 1.3.1 关键字
自我检查一下知道下面的关键字？

- final
- const
- finally
- async
- await
- Future
- implements
- Extension

###### 1.3.2 类的初始化
看文档


###### 1.3.3 函数声明参数的样式
这个点，文档说的不清楚。
我在这里举例，简单的说明一下。

1 . 普通的函数形式

```dart

//声明了返回值类型
String logSome(String name , int age) {
  return "name:$name---age:$age";
}

//也可以不声明返回值类型
logSome2(String name , int age) {
  return "name:$name---age:$age";
}

//跟c调用一样，不用带name，age
print(logSome("klc",18));
```

2 . 可选参数的函数形式

```dart
printUserInfo(String name , [int age]){
    if (age != null ) {
      print("name:$name---age:$age");
    } else {
      print("name:$name---age保密");
    }
}

printUserInfo("小明");
// name:小明---age保密
```

3 . 可选参数的默认值

```dart

printUserInfo(String name , [int age ,String sex = "男"]){
    if (age != null ) {
      print("name:$name---age:$age---性别$sex");
    } else {
      print("name:$name---age保密---性别$sex");
    }
}

//错误的调用形式
printUserInfo("小明","女"); //第二个参数对应的是age int


//所以一般的，null的参数放在后面声明~~~~~~~~~~~


printUserInfo(String name , [String sex = "男" , int age ]){
    if (age != null ) {
      print("name:$name---age:$age---性别$sex");
    } else {
      print("name:$name---age保密---性别$sex");
    }
}
printUserInfo("小明","男"); 
//name:小明---age保密---性别男
```

 4 . 关键字参数
 总的来说，关键字参数是建立在可选参数之上的，意思就是说`{}`里面的参数都是可选的参数。但是调用的时候需要带上形参，表示传入对应的参数。当然也可以设置默认值。
 
 另外说一句，文档中说到的，可选参数有2中，一种是**可选的位置参数**（看第3条），一种是**可选的关键字参数**（看第4条，本条）。**但两者不能同时出现在参数列表中**。
 
 ```dart
 printUserInfo(String name , {String sex = "男", int age}){
    print("name:$name---age:$age---性别$sex");
}

printUserInfo("小明"); 
//name:小明---age:null---性别男

printUserInfo("小明",age:18); 
//name:小明---age:18---性别男

//这里可以看到age和sex位置可以换，所以说是关键字参数，位置不重要。
 printUserInfo("小明",age:18,sex:"gay"); 
//name:小明---age:18---性别gay

 ```



###### 1.3.4 重要概念（摘抄文档上的`Important concepts`）

- 所有变量引用的都是 对象，每个对象都是一个 类 的实例。数字、函数以及 `null` 都是对象。所有的类都继承于 `Object` 类。

- 尽管 `Dart` 是强类型语言，但是在声明变量时指定类型是可选的，因为 `Dart` 可以进行类型推断。在上述代码中，变量 `number` 的类型被推断为 `int` 类型。如果想显式地声明一个不确定的类型，可以使用特殊类型 `dynamic`

- `Dart` 支持泛型，比如 `List<int>`（表示一组由 `int` 对象组成的列表）或 `List<dynamic>`（表示一组由任何类型对象组成的列表）
- `Dart` 没有类似于 `Java` 那样的 `public`、`protected`和 `private` 成员访问限定符。如果一个标识符以下划线 `(_)` 开头则表示该标识符在库内是私有的。

###### 1.3.5 import库

- 导入自己写的文件夹中包含的文件， `import 'Animal/Animal.dart';`这里的Animal文件夹是同目录下的文件夹。(这里要写路径，挺麻烦的，iOS基本上没写过)

- 导入系统内置的库，`import 'dart:io';`  这里库的路径是`flutter/bin/cache/dart-sdk/lib`中的各种库

- 导入pub安装的库（类似pod），使用方式看库的说明。导入的方式例如：`import 'package:http/http.dart' as http`








#### 1.4 Dart槽点
下面的槽点是我的个人观点，不代表广大大神观点。

- 一句话有分号结尾
- 类的一些初始化语法糟糕
- 开发文档结构相对来说差，对入门开发者不是太友好
- 组件文档没有做列表到目录方便查看
- 括号太多了，各种小括号，大括号，还各种嵌套







