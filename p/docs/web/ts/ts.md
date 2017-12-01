> ## 导读
>[TypeScript 官网](http://www.typescriptlang.org)  
>[TypeScript 中文官网](https://www.tslang.cn/)  
>[TypeScript 在线编译器](http://www.typescriptlang.org/play)  
>[TypeScript Handbook（中文版)](https://zhongsp.gitbooks.io/typescript-handbook/content/)  


### [interface  接口](https://www.tslang.cn/docs/handbook/interfaces.html)  

* 类静态部分与实例部分  
类有两种类型：静态部分的类型和实例的类型。

```
interface Point {
    readonly x: number;
    readonly y: number;
}
let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error!
```

### [基础类型示例](https://www.tslang.cn/docs/handbook/basic-types.html)

```
//作用：添加按钮到body标签中
let putButton = function (text:string,info:any){
    let button = document.createElement("button");
    let p = document.createElement("p");
    button.textContent = text;
    document.body.appendChild(button);
    document.body.appendChild(p);
    button.onclick = function() {
        alert(info);
    };
}

//boolean类型
let flag:boolean;
let flag_1:boolean = false;
putButton("let flag:boolean;",flag);
putButton("let flag_1:boolean = false;",flag_1);

//number
let PI : number = 3.1415926535897932384626433;//圆周率
putButton("number>>>圆周率PI",PI);
putButton("number>>>圆直径5，周长",5*PI);

//字符串
let str_double_quotes:string = "双引号声明string";
let str_single_quote :string = '单引号声明string';
let str_accent :string = `上点号声明string`;//可内嵌${表达式}
putButton("string>>>"+str_accent+"${5*8}",`5*8的值：${5*8}`);

//数组,两种声明方式
let nums: number[] = [1, 2, 3,4];
let numList: Array<number> = nums;
putButton("数组[1,2,3,4]",numList.toString());

//元组Tuple
let dog:[string,number] = ["蝴蝶犬",5];//元组是一个数组，允许元素类型不同
dog[3] = "岁了";//数组越界不报错，因为"dog"是string|number联合类型
// dog[4] = false;//错误
putButton("元组Tuple",dog[0]+dog[1]+dog[3]);

//enum 枚举
enum Xiyouji{
    唐僧,悟空,八戒=3,沙僧,白龙马
}//手动指定索引下标
let tangseng:Xiyouji = Xiyouji.唐僧;
let wukong:string = Xiyouji[1];//手动声明索引，左边索引从零开始
let shaseng:string = Xiyouji[4];//手动声明索引，右边索引依次增加
putButton("enum>>>西游记",wukong);

//any 任意值
let 水牛:any = "shuiniu";
let shuiniu:number = 100;
水牛 = shuiniu;
putButton("any>>>水牛",水牛);

//void 空值，只能为null或undefined
let v:void = null;
v = undefined;
function f():void{ return v};//空返回值，有点奇怪
putButton("void>>>",f());

//null和undefined，默认情况下null和undefined是所有类型的子类型。其他类型的值一般都可以赋给它们。
let undef: undefined = null;
let nul: null = undefined;
putButton("null和undefined","null和undefined是所有类型的子类型");

//Never类型表示的是那些永不存在的值的类型
//never类型是任何类型的子类型，但没有类型是never的子类型
// 这意味着never可以赋值给任何类型，但没有任何类型可以赋值给never类型（除了never本身之外）
let neve:never ;//初值undefined
let go:string = neve;
//never表示永远不存在值的类型
function trueWhile():never{
    while (true){}
}
putButton("never>>>",go);
```

### 数组的解构

```
//解构数组，构造数组。
let input = [1, 2];
let [first, second] = input;//相当于使用索引声明两个变量first = input[0];second = input[1];
setElement("h1","数组的解构");
setElement("p",first+"----"+second);
//交换值
[second,first] = [first,second];
setElement("p",first+"----"+second);
//...的形式声明剩余变量。
let [o,,u,...t] = [1,2,3,4,5];//一些元素可以不必命名
setElement("p",o+"----"+u+"----"+t);
```