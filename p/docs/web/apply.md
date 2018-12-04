## 模拟 apply 实现

> apply() 方法调用一个函数, 其具有一个指定的 this 值和一个包含多个参数的数组。


模拟实现：
ES3 版

```
Function.prototype.apply = function (context, arr) {
    var context = context || window;
    context.fn = this;

    var result;
    // 判断是否存在第二个参数
    if (!arr) {
        result = context.fn();
    } else {
        var args = [];
        for (var i = 0, len = arr.length; i < len; i++) {
            args.push('arr[' + i + ']');
        }
        result = eval('context.fn(' + args + ')');
    }

    delete context.fn
    return result;
}
```

ES6版：

```
Function.prototype.apply = function (context, arr) {
    context = context || window;
    context.fn = this;

    let result;
    // 判断是否存在第二个参数
    if (!arr) {
        result = context.fn();
    } else {
        result = context.fn(...arr);
    }

    delete context.fn
    return result;
}
```

>[点击查看call模拟实现](call.md)