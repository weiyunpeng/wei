# Dart

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

```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:async';
import 'dart:isolate';

void main() {
  runApp(new SampleApp());
}

class SampleApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Sample App',
      theme: new ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: new SampleAppPage(),
    );
  }
}

class SampleAppPage extends StatefulWidget {
  SampleAppPage({Key key}) : super(key: key);

  @override
  _SampleAppPageState createState() => new _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {
  List widgets = [];

  @override
  void initState() {
    super.initState();
    loadData();
  }

  showLoadingDialog() {
    if (widgets.length == 0) {
      return true;
    }

    return false;
  }

  getBody() {
    if (showLoadingDialog()) {
      return getProgressDialog();
    } else {
      return getListView();
    }
  }

  getProgressDialog() {
    return new Center(child: new CircularProgressIndicator());
  }

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
        appBar: new AppBar(
          title: new Text("Sample App"),
        ),
        body: getBody());
  }

  ListView getListView() => new ListView.builder(
      itemCount: widgets.length,
      itemBuilder: (BuildContext context, int position) {
        return getRow(position);
      });

  Widget getRow(int i) {
    return new Padding(padding: new EdgeInsets.all(10.0), child: new Text("Row ${widgets[i]["title"]}"));
  }

  loadData() async {
    ReceivePort receivePort = new ReceivePort();
    await Isolate.spawn(dataLoader, receivePort.sendPort);

    // The 'echo' isolate sends it's SendPort as the first message
    SendPort sendPort = await receivePort.first;

    List msg = await sendReceive(sendPort, "https://jsonplaceholder.typicode.com/posts");

    setState(() {
      widgets = msg;
    });
  }

// the entry point for the isolate
  static dataLoader(SendPort sendPort) async {
    // Open the ReceivePort for incoming messages.
    ReceivePort port = new ReceivePort();

    // Notify any other isolates what port this isolate listens to.
    sendPort.send(port.sendPort);

    await for (var msg in port) {
      String data = msg[0];
      SendPort replyTo = msg[1];

      String dataURL = data;
      http.Response response = await http.get(dataURL);
      // Lots of JSON to parse
      replyTo.send(JSON.decode(response.body));
    }
  }

  Future sendReceive(SendPort port, msg) {
    ReceivePort response = new ReceivePort();
    port.send([msg, response.sendPort]);
    return response.first;
  }

}
```

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
