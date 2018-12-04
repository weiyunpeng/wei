## 模拟 call 实现

> call() 方法调用一个函数, 其具有一个指定的 this 值和分别地提供的参数(参数的列表)。

与 apply()的区别：

```
call() 和 apply()的区别在于，call()方法接受的是若干个参数的列表，而apply()方法接受的是一个包含多个参数的数组
```

模拟实现：
ES3 版

```es3
Function.prototype.call = function (context) {
    // this 参数可以传 null 或者 undefined，此时 this 指向 window
    var context = context || window;
    context.fn = this;

    var args = [];
    for(var i = 1, len = arguments.length; i < len; i++) {
        args.push('arguments[' + i + ']');
    }
    var result = eval('context.fn(' + args +')');

    delete context.fn
    return result;
}
```

ES6 版

```
Function.prototype.call = function(context) {
    context = context || window;
    context.fn = this;

    let args = [...arguments].slice(1);
    let result = context.fn(...args);

    delete context.fn;
    return result;
};
```
>[点击查看apply模拟实现](apply.md)