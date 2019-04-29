# 语义标签
## article
具有独立性质的文章，与body结构类似。
> 一个body内可以有多个article标签。(类似报纸的新闻专题)
## header、footer
* header 出现在前部、通常放置导航介绍性内容等 
* footer 出现在尾部、通常放置尾部版权信息、连接、作者信息等

## section
“有语义的div”，会降低h*的级别。 理论上，可以用section嵌套+h1表现标题结构。

## aside  
用于放置跟文章主体不那么相关的部分。 

## address
> 最后 footer 中包含 address，这是个非常容易被误用的标签。address 并非像 date 一样，表示一个给机器阅读的地址，而是表示“文章（作者）的联系方式”，address 明确地只关联到 article 和 body。

## abbr
用以表示缩写。
```
<abbr title="World Wide Web">WWW</abbr>.
```
## hr   
hr 表示故事走向的转变或者话题的转变，如果是视觉效果请使用css border。

##  i、em、strong、b、mark
---
* i     
 普通文本中有不同语态或语气的一段文本， 某种程度上标明一段不同特性的文本。     
比如 一个**分类学名称**、**外语习语**、**专业术语**等

* em    
语义上的**重读**现象。 详见上一篇[html语义化1](./html语义化(1).md)        

* strong     
 强烈的重要性、严重性或者紧急性。

* b     
侧重实用目的不带任何额外总要性也不暗示不同语态的一段文本。比如摘要的关键字，一段文本中的产品名。

> s： 之前表示划线的废弃标签，html5重新启用，表示错误内容。经常用于电商打折前价格。      
> i:  之前表示斜体的废弃标签，html5重新启用，表示变调      
> b:  之前表示黑体的废弃标签，html5重新启用，表示关键字      


## blockquote\q\cite    
* q     
表示一句两句的引述。
* cite      
引述文字的出处。
```
<q>话说天下大事，合久必分.....</q>
<cite>三国演义</cite>
```
* blockquote    
大段的引用

## figure\figcaption
通常一片文章中出现一张跟内容息息相关的图片，此时图片就不只是简单的img了，文字、图片相互补充。他们构成一种figure的语法现象。figure标签就是对这种语法现象的说明。     
```
<figure>
    <img src="xxxx" alt="xxx" />
    <figcaption>图1.2 xxx流程图</figcaption>
</figure>

```
## dfn   
用于名词的定义。
```
<dfn>goland</dfn> google推出的编程语言。
```

## pre、samp、code

## dl\dt\dd
一般出现在比较严肃的文章内，对术语的定义。

## main
文章主体

## menu  
上下文菜单




# 参考文档
* [[1] Text-level semantics](https://w3c.github.io/html/textlevel-semantics.html#the-em-element)    
* [[2] 从HTML5规范弄清i、em、b、strong元素的区别](http://www.cnblogs.com/charles-dxb/p/6476196.html)                
* [[3] cite,q与blockquote区别](https://blog.csdn.net/weixin_40848638/article/details/82711680)

