# 选择器
与css选择器一致。可以通过类、id、元素选择器及连接符构成组合的选择器。
> 备忘： +：相邻      ~：全部兄弟     

**可见性**    
:hidden     
:visible

**基本筛选**    
:eq    
:even   索引值为偶数的，0、2、4... 即为第一行、第三行...     
:odd    索引值为奇数的
 
# 查找
find()    
sibling()    
next()     
nextAll()    
prev()    
prevAll() 
children()      
parent()   
parents()   

# 属性
attr()    
removeAttr()    
prop()    
removeProp   
val()

# data
hasData()   
data()    
removeData()    

# 样式
.css()   
.addClass()    
.removeClass()    
.hasClass()    
.toggleClass()    

# 尺寸
width        
innerWidth    
outerWidth    
height    
innerHeight    
outerHeight    

# 拷贝
.clone()    

# 操作
## 包裹
warp()    
warpAll()    
warpInner()   

## 插入子孙 
append()    
appendTo()    
prepend()    
prependTo()    
html()    
text()    

## 插入兄弟
after()    
insetAfter()    
before()    
insetBefore()    

## 移除
remove()    
detach()    
empty()    
unwarp()    

## 替换
replaceAll()    
replaceWith()    
