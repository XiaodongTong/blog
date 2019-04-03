# 概要
> 狭义的 DOM API 仅仅包含 DOM 树形结构相关的内容。    
> DOM 中的所有的属性都是用来表现语义的属性，CSSOM 的则都是表现的属性。      

CSSOM 是 CSS 的对象模型，在 W3C 标准中，它包含两个部分：
* 描述样式表和规则等 CSS 的模型部分（CSSOM）
* 跟元素视图相关的 View 部分（CSSOM View）。


# CSSOM
在实际使用中，CSSOM View 比 CSSOM 更常用一些，因为我们很少需要用代码去动态地管理样式表。

# CSSOM View

## 1、窗体API

* moveTo(x, y) 窗口移动到屏幕的特定坐标；
* moveBy(x, y) 窗口移动特定距离；
* resizeTo(x, y) 改变窗口大小到特定尺寸；
* resizeBy(x, y) 改变窗口大小特定尺寸。
* window.open(uri,target,size) 第三个参数描述窗口的尺寸信息
```
window.open("about:blank", "_blank" ,"width=100,height=100,left=100,right=100" )
```
ps: 出于安全考虑，一些浏览器没有实现。

## 2、滚动API
### 视口滚动
在window对象上的，是顶层容器滚动提供的API，大部分移动端浏览器会对这部分api做性能优化。它和元素滚动API不同。    
* scrollX 属性，X方向上当前滚动的距离。
* scrollY 属性，Y方向上当前滚动的距离。   
     
* scroll(x,y)方法，使得页滚动到指定位置。别名scrollTo，
* scrollBy(x,y)方法，使页面滚动指定距离。

要监听视口滚动事件，我们需要在document对象上绑定scroll事件监听函数。
```
document.addEventListener("scroll",function(event){
  //......
});
```
### 元素滚动
在Element类，为了支持滚动，加入了以下API。
* scrollTop      属性，表示Y方向上的当前滚动的距离。
* scrollLeft     属性，表示X方向上的当前滚动的距离。
* scrollWidth    属性，元素滚动内容的宽度，一般>=元素宽度。
* scrollHeight   属性，元素滚动内容的高度，一般>=元素高度。
* scroll(x,y)    方法，使元素滚动到指定位置，别名scrollTo
* scrollBy(x,y)  方法，使元素滚动指定距离。

元素也支持scroll事件
```
element.addEventListener("scroll", function(event){
  //......
})
```
## 3、布局API
### 全局尺寸信息
* window.innerHeight         视口的高
* window.innerWidth          视口的宽
* window.devicePixelRatio    像素比（DPR），物理像素和css像素单位的倍率关系。
* window.screen   
> window.screen.width, window.screen.height 设备的屏幕尺寸。

### 获取Element对象的尺寸信息。     
    
* element.clientWidth\element.clientHeight
> 属性表示元素的内部宽度\高度，以像素计。该属性包括内边距，但不包括滚动条（如果有）、边框和外边距。    
> 该属性值会被四舍五入为一个整数。如果你需要一个小数值，可使用 element.getBoundingClientRect()。
* element.getBoundingClientRect()     
返回一个ClientRectd对象包含以下属性。
```
bottom	 float	Y 轴，相对于视口原点（viewport origin）矩形盒子的底部。只读。     
height	 float	矩形盒子的高度（等同于 bottom 减 top）。只读。     
left	   float	X 轴，相对于视口原点（viewport origin）矩形盒子的左侧。只读。      
right	   float	X 轴，相对于视口原点（viewport origin）矩形盒子的右侧。只读。      
top	     float	Y 轴，相对于视口原点（viewport origin）矩形盒子的顶部。只读。     
width	   float	矩形盒子的宽度（等同于 right 减 left）。只读。      
x	       float	X 轴，相对于视口原点（viewport origin）矩形盒子的左侧。只读。      
y	       float	Y 轴，相对于视口原点（viewport origin）矩形盒子的顶部。只读。   
```  


* getClientRects()    
会返回一个列表，里面包含元素对应的每一个盒所占据的客户端矩形区域.
 



