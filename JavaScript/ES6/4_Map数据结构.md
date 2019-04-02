# 概要   
字典是用来存储不重复key的Hash结构。不同于集合（Set）的一点，字典使用的是[key,value]的形式来存储数据。   
   
JavaScript的对象（Object:{}）只能用字符串当做key。使用起来有一定限制。    
为了解决这个问题，ES6提供的Map数据结构。它类似与对象，也是[key,value]的集合，但是key的范围不限于字符串，各种类型的值（包括对象）都可以当做key。   

---

也就是说Object结构提供了  “字符串--值”的对应；   
Map提供了“值--值”的对应，是一种完善的Hash结构的实现。   
如果需要使用键值对的数据结构，Map比Object更合适。

```
//对于Object只能使用字符串作为key这一点，例如一下代码。

var obj = {},
    key1={b:22},
    key2={c:33};

obj[key1] = 1;
obj[key2] = 2;

//此时key1，key2都会被转成字符串“[object Object]”
console.log(obj);  //Object{[object Object] : 2} 
```
    
# 使用
### 1 创建一个Map    
```
const map = new Map([
    ['a',1],['b',2]
]);

console.log(map); // {"a" => 1, "b" => 2}
```

### 2 Map 类的属性
```
console.log(map.size); //字典长度


```

### 3 Map 类的方法   
#### set(key,value)   
设置一个键值对，然后返回整个Map结构。如果Key已经有值，则键值被更新，否则生成该键。   
map里面的key的排序顺序是按照添加的顺序排列的。
```
map.set('jd','www.jd.com')
   .set('baidu','www.baidu.com');

console.log(map);
```
   
#### get(key)   
读取key对应的键值，如果找不到key，返回undefined。

```
console.log(map.get('jd'));  //wwww.jd.com
console.log(map.get('x'));   //undefined
```
   
#### delete(key)   
删除某个键，成功返回true，失败返回false。
```
console.log(map.delete('baidu')); // true
console.log(map.delete('baidu')); // false
```
   
#### has(key)   
判断某个key是否在map中存在，返回一个布尔值。   
```
console.log(map.has('jd')) //true
```
   
#### clear()   
清除所有数据，无返回值
```
map.clear();
console.log(map);  // Map(0) {}
```
   
---

#### keys()   
返回键名的遍历器
```
const map = new Map([
    ['jd','www.jd.com'],
    ['baidu','www.baidu.com']
]);
console.log(map.keys());   // MapIterator {"baidu","jd"}
```
#### values()   
返回键值的遍历器
```
console.log(map.values());   // MapIterator {"www.baidu.com","www.jd.com"}
```
#### entries    
返回键值对的遍历器   
```
console.log(map.entries());   // MapIterator {['jd','www.jd.com'],['baidu','www.baidu.com']}
```
   
---
   
#### forEach()    
使用回调函数遍历每个成员
```
map.forEach(function(key,value,map){
    console.log(key + ':' + value); // baidu:www.baidu.com
})
```



