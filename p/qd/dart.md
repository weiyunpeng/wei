# [Dart](https://github.com/dart-lang/sdk)

- 所有类型都是对象类型，都继承自顶层类型的Object,因此一切变量都是对象，数字、布尔值、函数和null也概莫能外；
- 未初始化变量的值都是null；
- 为变量指定类型，这样编辑器和编译器都能更好地理解你的意图。

#### 特性

同时支持JIT(Just In Time，即时编译) 与 AOT(Ahead Of Time，运行前编译)
>开发的时候用JIT，动态下发和执行代码。在发布的时候使用AOT,运行速度快，执行性能好。

#### 内存分配
创建对象的时候只需要在堆上移动指针，内存增长始终是线性的，省去查找可用内存的过程。

#### 垃圾回收
采用[多生代算法](https://medium.com/flutter/flutter-dont-fear-the-garbage-collector-d69b3ff1ca30)

#### 单线程模式
没有线程，只有Isolate(隔离区)。
在Dart语言中，所有的Dart代码都运行在某个isolate中，代码只能使用所属isolate的类和值。不同的isolate可以通过port发送message进行交流。isolate在它自己的事件循环(event loop)中执行代码，每个事件都可以在该isolate的微任务队列(microtask queue)中执行更小的任务。

#### Dart 变量与类型
未初始化的变量都是null。  
num有两个子类：64位的int和符合IEEE754标准的64位double。高级运算方法调用dart:math库。  
bool只有两个对象具有，**true**和**false**
string由UTF-16的字符串组成。
list数组类型，map字典类型用法与javascript类似。  
可以添加类型约束，让语义更清晰如：
```dart
// list
var arr = [1,2,3]
// 增加类型约束后
var arr = <int>[1,2,3]
// map
var map = {"name":"Tom","age":"18"}
// 增加类型约束后
var map = <String,String>{"name":"Tom","age":"18"}
```

### 信息处理

#### 常量

如果想定义不可变的变量，可以使用 *const* 和 *final*。  
const适用于编译常量，final适用于运行常量。

```dart
const num = 1;
final z = num + 1;
```

#### 函数
函数也是对象，它的类型是Function。  
函数也可以被定义为变量，作为参数使用。

```dart
bool isZero(int number) {
  return number == 0
}

void printInfo(int number,Function check) => print("$number is Zero:${check(number)}")

Function f = isZero;
int x = 0;
printInfo(x,f)
```
多参传递
```dart
// 要达到可选命名参数的用法，那就在定义函数的时候给参数加上 {}
void enable1Flags({bool bold, bool hidden}) => print("$bold , $hidden");

// 定义可选命名参数时增加默认值
void enable2Flags({bool bold = true, bool hidden = false}) => print("$bold ,$hidden");

// 可忽略的参数在函数定义时用 [] 符号指定
void enable3Flags(bool bold, [bool hidden]) => print("$bold ,$hidden");

// 定义可忽略参数时增加默认值
void enable4Flags(bool bold, [bool hidden = false]) => print("$bold ,$hidden");

// 可选命名参数函数调用
enable1Flags(bold: true, hidden: false); //true, false
enable1Flags(bold: true); //true, null
enable2Flags(bold: false); //false, false

// 可忽略参数函数调用
enable3Flags(true, false); //true, false
enable3Flags(true,); //true, null
enable4Flags(true); //true, false
enable4Flags(true,true); // true, true

```

#### 类
在类名前加下划线即可作为**private**方法使用，不加就是**public**属性。  
'_'的限制范围并不是类的访问级别，而是库访问级别。  
初始化参数支持**命名构造函数**
```dart
class Point {
  num x,y,z;
  Point(this.x, this.y) : z = 0;
  Point.bottom(num x) : this(x, 0); //重定向构造函数
  void printInfo() => print(`($x,$y,$z)`);
}

var p = Point.bottom(100);
p.printInfo();
```

#### 复用
> 继承父类,接口实现和混入（mixin）

- 继承父类：子类由父类派生，自动获取父类的成员变量和方法实现，子类可以根据需要覆写构造函数及父类方法；
- 接口实现：子类获取到的仅仅是接口的成员变量符号和方法符号，需要重新实现成员变量，以及方法的声明和初始化，否则编译器会报错。
- mixin:混入，解决多重继承的问题。

```dart
class Point {
  num x= 0, y=0;
  void printInfo() => print(`($x,$y)`);
}

// Vector 继承自Point
class Vector extends Point {
  num z = 0; 
  @override
  void printInfo() => print(`($x,$y,$z)`) //覆写了printInfo
}

//Coordinate是对Point的接口实现
class Coordinate implements Point {
  num x=0,y=0; //成员变量需要重新声明
  void printInfo() => print(`($x,$y)`);
}

// Stage
class Stage with Point{}


var xxx= Vector();
xxx
  ..x = 1
  ..y = 2
  ..z = 3; //级联运算符，等同于xxx.x=1;xxx.y=2;xxx.z=3;
xxx.printInfo(); //输出（1,2,3）

var yyy = Coordinate();
yyy
  ..x = 1
  ..y = 2;
yyy.printInfo();//输出（1,2）

print(yyy is Point); //true
print(yyy is Coordinate) // true

var zzz = Stage();
print(zzz is Point); //true
print(zzz is Stage);//true
```

#### 运算符
> 运算符也是对象成员函数的一部分。我们不仅可以覆写方法，还可以覆写或者自定义运算符。

- **?.** : p?.printInfo() 表示p为null的时候跳过，避免抛出异常。
- **??=** : a ??= value 表示a为null的时候,给a赋值value，否则跳过。
- **??** : (a != null) ? a : b 可以简化为a ?? b。