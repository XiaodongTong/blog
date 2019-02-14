首先, js是一门面向对象的语言。但与java、.net等为人熟知的，基于类的面相对象语言不同。js的面相对象是基于原型的。
> 基于类编程，只是面相对象，实现的方式之一。除此之外，还有其他方式。而js早年就选择了一个冷门的方式：原型。     
> 然而很不幸，因为一些公司政治原因，JavaScript 推出之时受管理层之命被要求模仿 Java，所以，JavaScript 创始人 Brendan Eich 在“原型运行时”的基础上引入了 new、this 等语言特性，使之“看起来更像 Java”。     
> 在 ES6 出现之前，大量的 JavaScript 程序员试图在原型体系的基础上，把 JavaScript 变得更像是基于类的编程，进而产生了很多所谓的“框架”，比如 PrototypeJS、Dojo。    
> 事实上，它们成为了某种 JavaScript 的古怪方言，甚至产生了一系列互不相容的社群，显然这样做的收益是远远小于损失的。
好在，ES6中开始支持Class的概念。

# Class的语法
```
class People {
  constructor(a,b){
    this.a = a;
    this.b = b;
    return this;
  }
  toString(){
    console.log(this.a + ' ' + this.b);
  }
}

let p1 = new People('11','22').toString(); // 11 22

console.log(People.prototype); // {constructor: ƒ, toString: ƒ}
console.log(Object.keys(People.prototype)); // []
```
上面这段代码，有以下几点说明：
1. class中的constructor是构造函数。 通过new命令创建实例时，会自动调用该方法。    
一个类必须有constructor方法，如果没有显示定义，会被默认添加一个空的。
2. 注意，类里的方法间，不能加逗号，会报错。

3. 构造函数的prototype属性，在ES6的Class上继续存在。 并且类的所有方法都定义在类的prototype属性上面。

4. 定义在类中的方法都是不可枚举的。
  
5. 生成类的实例对象的写法，跟ES5完全一样。 如果忘了加new，像调用函数一样调用Class，会报错。

# 原型的写法

```
let People = function(a,b){
  this.a = a;
  this.b = b;
  return this;
}

People.prototype = {
  constructor:People,
  toString:function(){
    console.log(this.a + ' ' + this.b);
  }
}

let p2 = new People('11','22').toString(); // 11 22

```








