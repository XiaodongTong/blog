# onload 与 load
## onload
```
//是页面中的所有元素（包括图片、flash）等都加载完毕后，才能执行；
//不可以同时加载多个
window.onload=function(){
    //....
}
```

## load
```
//是页面中的所有元素（包括图片、flash）等都加载完毕后，才能执行；
$(window).on('load',function(){
    //...
});

//简写
$(function(){
    //...
})

//javascript原始写法
window.addEventListener("load", function() {}, false);
```

# ready

```
// 是页面中的DOM元素加载完成后便可执行。
$(document).ready(function(){
    //...
})

//javascript原始写法
window.addEventListener('DOMContentLoader',function(){},false);
```