# let命令
用来声明一个变量，和var非常类似
1. 使用let声明的变量，所声明的变量只在命令所在的代码块中有效
```
{
    let a = 1;
    console.log(a); // 这里是可以使用的 
}
console.log(a);   //这里不可以使用
```
2. 使用let声明的变量，在欲解析的时候不会被提升。
```
//使用var声明变量时,可以这样写
console.log(a); // 此时输出  undefined
var a = 1;

//但是使用let时
console.log(a); // 会报错
let a = 1;

typeof c;
let c = 10; //依然会报错

let f = 10;
function fn(){
    f = 7;   //暂时性死去，会报错
    let f = 2;
}
```
3. 使用let声明的变量,不允许在作用域下声明同一个变量
```
var a= 1;
let a;
```
## 使用场景
```
//例如这样一段html代码。
<div>
    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button>4</button>
</div>
//通过dom操作获取buttion
var btns = document.querySelectAll('button');
```
如果这样写,每次点击都会打印3.

```
for(var i=0; i<btns.length; i++){
    btns[i].onclick=function(){
        console.log(i);
    }
}
```
按照以往惯例解决方案有两种：   
1 使用dom属性
```
for(var i=0; i<btns.length; i++){
    btns[i].index = 1;
    btns[i].onclick=function(){
        console.log(this.index);
    }
}
```
2 使用闭包
```
for(var i=0; i<btns.length; i++){
    (function(i){
        btns[i].onclick=function(){
            console.log(i);
        }
    })(i);
}
```
现在呢，可以使用let
```
for(let i=0; i<btns.length; i++){
    btns[i].onclick=function(){
        console.log(i);
    }
}
//在for循环中使用，let声明变量，有一个特别的现象。
//在循环语句之内 是一个父作用域，在循环体之中是一个子作用域。
```

# const 关键字
用来声明一个常量，可以简单理解成一个不可以变化的常量   
和let类似，const同样具备let的三种特点。
1.  所声明的常量在所在代码块中有效
2.  在欲解析时候不会被提升，需要先定义后使用。
3.  不允许同一作用域下，声明相同的常量
---
4.  使用const声明常量的时，必须赋值

5.  const 实际上保证的并不是变量的值不能改变，而是变量指向的内存地址不能改变。
    对于简单数据类型，直接存储的直接是值。
    对于复杂数据类型，内存位置虽然没有变化，但是内部的值是可以改变的。
```
// 例如
const obj = {a:10};
obj.a = 20;            //是可以运行的
console.log(obj.a);    //此时a = 20
```


