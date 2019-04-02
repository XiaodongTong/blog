ES5中包含5个原始类型，分别是：
*  Undefined
*  Null
*  Boolean
*  Number
*  String

ES6中又增加了一个Symbol。

# 创建
通常我们通过一个Symbol()函数来创建一个Symbol实例。
```
let s1 = Symbol();
```
Symbol()函数可以传一个参数，用于写一点console的描述信息。
```
let s2 = Symbol("description");
```
每个Symbol实例都是唯一的，因此比较两个Symbol实例时，总会返回false;
```
let s1 = Symbol('d');
let s2 = Symbol('d');

s1 === s2  //false
```

**如何在各个windows间，创建&获取 一个全局的共享的Symbol？**    
此时需要使用Symbol.for()，它可以创建 或者 获取window间全局的Symbol实例。  
Symbol.for()有点类似，单例模式。
```
let g1 = Symbol.for('global_1');
let g2 = Symbol.for('global_1');

g1 === g2;  // true
```

# 应用场景

我们都知道js不像java一样有public，private这样的访问修饰符。那么在对象中如何控制某个属性不被外部访问到？   
我们尝试一下使用Symbol。
```
  let obj = {
    [Symbol('pwd')]:'xxx',
    name:'russell'
  };
  
  Object.keys(obj); // ['name'];
  
  for(let key in obj){
    console.log(key);  // output: name
  }
```
如上所示，Symbol类型的key是不能通过Object.keys()、for in来枚举的。 
还不止这些，当我们使用JSON.stringify()，把对象序列化成JSON字符串时同样没有Symbol属性。

```
let obj = {
  [Symbol('pwd')]:'xxx',
  name:'russell'
};
JSON.stringify(obj); //{"name":"russell"}
```
利用这一特点，我们可以把一些不需要对外操作和访问的属性用Symbol来定义。 让“对内操作”和“对外选择性输出”变得更加优雅。















