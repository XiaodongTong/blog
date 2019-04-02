## 概要   
js中的数组、对象，加上ES6中增加的Map、Set四种数据集合。 Iterator提供了一种机制，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作。（依次操作）   

**作用：**   
> * 为各种数据结构提供了统一的，简便的访问接口。   
> * 使得数据结构的成员能够按照某种顺序排列。   
> * ES6中增加了遍历命令 for...of循环，Iterator接口主要供for...of消费

## 原理
> 1. 创建一个指针对象，指向当前数据结构的起始位置。 遍历器对象本质上是一个指针。
> 2. 第一次调用next方法，返回数据结构的第一个对象。
>    第二次调用next方法，返回数据结构的第二个对象。依次向下。
> 3. 不断调用next方法，直到它指向数据结构的结束位置。  每次执行next方法，都会返回一个具有value和done属性的对象。value是当前成员的值，done是一个表示是否结束循环的布尔值。


**手写Iterator接口**   
```
function iterator(arr){
    let index = 0;
    return {
        next:function(){
            return index < arr.length ?
            {value:arr[index++], done:false}:
            {value:undefined, done:true};
        }
    }
}
let arr = [1,2,3];
let it = iterator(arr);
```
## 使用

### 凡是具有Symbol.iterator属性的数据结构都具有 Iterator接口   

```
let arr = [1,2,3];
let set = new Set(['1','2']);
let map = new Map([['a':1],['b':2]]);

//Array Iterator {}
console.log( arr[Symbol.iterator]() );

//SetIterator {'1','2'}
console.log( set[Symbol.iterator]() );

//MapIterator {["a",1],["b",2]}
console.log( map[Symbol.iterator]() );          

//Object{value:1 , done:false }
arr[Symbol.iterator]().next();   

```
### for...of循环
数据   

```
 let arr = [1,2,3];
 /*
 * output: 1
 *         2  
 *         3  
 */
 for (let i of arr){
     console.log(i);
 }
```
Map   
```
  let m = new Map();
  m.set('a',1);
  m.set('b',2);

  for(let [key,value] of m){
      console.log(key,value);
  }
```