# 概要
## 介绍：   
集合是由一组无序且唯一的项组成的，这个数据结构使用了与有限集合相同的数学概念，应用在计算机的数据结构中。   
ES6提供了数据结构Set。它类似于数组，但是没有重复的值。    
## 特点：   
key与value相同，没有重复的value。   

# 创建
```
const s = new Set([1,2,3]);
```

# 方法
## 添加
```
//添加一个数据，返回set结构本身。
Set.add(value);
//例
s.add('1').add('2').add('c');
console.log(s);
```
## 删除 delete
```
//删除指定数据，返回一个布尔值，表示是否删除成功！
Set.delete(value);
//例
console.log(s.delete('1'));  //true
console.log(s);
```
## 判断是否存在  has
```
//判断该值是否为Set的成员，返回一个布尔值
Set.has(value); 
//例
console.log(s.has('1')); // true
console.log(s.has('a')); // false
```
## 清空 clear
```
//清空所有数据，没有返回值。
Set.clear();
//例 
s.clear(); 
console.log(s);
```
## 返回键值的遍历器 values
```
 s.values();
```
## 返回键值对的遍历器 entries
```
s.entries();
```
## 使用回调函数，遍历每个成员 forEach
```
s.forEach(function(value,key,set){
    console.log(value);
});
```

# 属性
```
console.log(s.size); 
```