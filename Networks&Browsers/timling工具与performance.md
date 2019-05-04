
# Chrome开发者工具里的Timling
在Chrome浏览器的开发者工具里的**Network**抓包工具，相信大家再熟悉不过。     
但，我相信很多人跟我一样，不太了解抓包工具里每个请求对应的数据参数的具体含义。我今天要做的，就是跟大家一道逐一研究一下各部分内容的含义。   


![timling](/images/2019-05-04-11-16-16.png)
## Queueing
文件请求的排队时间，在**http/1.x**基础上，必须按照顺序请求文件。   

> 如果您对此部分内容不太清楚，建议阅读我整理的关于[HTTP](HTTP.md)的内容。


## Stalled 
是浏览器得到要发出这个请求的指令到请求可以发出的等待时间。等什么呢？一般是等待可复用的TCP连接释放。      

其实，这同样涉及**http/1.x**的问题，http/1.1有http管道，但管道同样有大小限制。   
chrome一次性只能处理6个tcp请求。其他的请求必须等待6个请求完成，这个等待时间是构成stalling的主要部分，所以说，前端开发时候，要使用cdn，要减少同一个域名下的tcp请求，

stalled时间长，多半是一些网络问题。



## DNS Lookup 
时间执行DNS查找。每个新域页面请求-DNS查找一个完整的往返。     
DNS查询的时间，当本地DNS缓存没有的时候，这个时间可能是有一段长度的；    
但是第二次访问，由于浏览器的DNS缓存还在，这个时间就为0了。（或者绑定HOST）   

> 如果您对此部分内容不太清楚，建议阅读我整理的关于[DNS](DNS.md)的内容。

## Initial connection 
建立TCP连接的时间，就相当于客户端从发请求开始到TCP握手结束这一段，我的理解是TCP握手时间。      

> 如果您对此部分内容不太清楚，建议阅读我整理的关于[TCP](TCP.md)的内容。      

## Request sent
请求第一个字节发出前到最后一个字节发出后的时间，也就是**上传时间**。通常GET请求速度非常快的。      

## Waiting（TTFB（Time To First Byte））   
请求发出后，到收到响应的第一个字节所花费的时间,发送请求完毕到接收请求开始的时间;       
这个时间段就代表**服务器处理和返回数据**，以及**网络延时时间**了。     
服务器优化的目的就是要让这个时间段尽可能短。      

通常的做法有：      
* MySql建立索引，优化SQL语句，减少慢查询，提高响应速度   
* 对热门资源构建缓存，提高响应速度       
* 构建CDN（内容分发网络），减少网络延迟      

等一系列手段吧。   

## Content Download 
收到响应的第一个字节，到接受完最后一个字节的时间，就是下载时间。

> 通常不会太长，如果时间特别长，可以关注一下文件大小。在保证展示效果的基础上，尽量用压缩比高的图片格式。相同展示效果的基础上，用jpg明显小于png。    
> 对了google有一个新的图片格式**webp**，图片尺寸会降低50%左右。

如果感兴趣的话可以阅读一下[探究WebP一些事儿](https://aotu.io/notes/2016/06/23/explore-something-of-webp/)


# performance API
performance是window对象上的一个属性，多数浏览器支持（IE9+）。您可以直接在Console中执行**performance**，就会看到如下图的输出。    

![performance](/images/2019-05-04-15-48-14.png)    

> 说明：**memory不是通用的属性，只在Chrome浏览器中存在**。下图（另一个浏览器的截图）就没有。
> ![performance没有memory](/images/2019-05-04-15-54-09.png)
---

好，接下来介绍performance是干什么用的。     
**performance是一个ES5提出的，可以获取到微秒级别(10^-9)的后台事件的时间点数据的API**。   
他主要由两大部分构成**navigation**和**timing**。我们今天主要研究这两块儿内容。

## performance.navigation

```
navigation: {
      /**  
        * 0   即 TYPE_NAVIGATENEXT 正常进入的页面（非刷新、非重定向等）
        * 1   即 TYPE_RELOAD       通过 window.location.reload() 刷新页面
        * 2   即 TYPE_BACK_FORWARD 通过浏览器的前进后退按钮进入的页面（史记录）
        * 255 即 TYPE_UNDEFINED    非以上方式进入的页面
        */
        type: 0   
        redirectCount: 0, // 如果有重定向的话，页面通过几次重定向跳转而来
    },
```

## performance.timing
**注意：这张图是Chrome 开发者工具里的Timing的示意图**。而下面的属性则是performance.timing的属性。

结合上文，您应该可以根据performance.timing提供的**时间点**计算出来DNS lookup、Initial connection等各个部分的耗时。**end-start**

![timing](/images/2019-05-04-16-15-28.png)

* **fetchStart**：发起获取当前文档的时间点

---

* **domainLookupStart**：返回浏览器开始DNS查询的时间
* **domainLookupEnd**：返回浏览器结束DNS查询的时间

---

* **connectStart**：浏览器向服务器请求文档，开始建立连接的时间
* **connectEnd**：浏览器向服务器请求文档，建立连接成功的时间

---

* **requestStart**：开始请求文档的时间（注意没有requestEnd）;
* **responseStart**：浏览器开始接收第一个字节数据的时间，数据可能来自于服务器、缓存、或本地资源；
* **responseEnd**：浏览器接收最后一个字节数据的时间，或连接被关闭的时间；
---
对照完了chrom开发者工具，你会发现还有很多属性没介绍。      
这是因为：chrom开发者工具咱们是从network下进去的，它更关注网络性能。performance关注的是整个网页从请求到展示的整个流程。     
其实performance的图里包含刚刚提到的那些参数，之所以放一张开发者工具的图，是为了跟以前的知识产生关联。   

---

那么接下来，上完整的performance的图。

![performance](/images/2019-05-04-16-32-21.png)

---

* **unloadEventStart**：卸载上一个文档开始的时间；     
* **unloadEventEnd**：卸载上一个文档结束的时间；  
 
---
* **domLoading**：浏览器把document.readyState设置为“loading”的时间点，开始构建dom树的时间点；
* **domInteractive**：浏览器把document.readyState设置为“interactive”的时间点，DOM树创建结束；

* **domContentLoadedEventStart**：文档发生DOMContentLoaded事件的时间；
* **domContentLoadedEventEnd**：文档的DOMContentLoaded事件结束的时间；
* **domComplete**：浏览器把document.readyState设置为“complete”的时间点；

---

* **loadEventStart**：文档触发load事件的时间；
* **loadEventEnd**：文档触发load事件结束的时间




# 参考文献
* [chrome----timing含义解释](https://blog.csdn.net/qq_20881087/article/details/56682525)
* [MDN对performance.timing各个属性的解释](https://developer.mozilla.org/zh-CN/docs/Web/API/PerformanceTiming)
* [前端知识普及之页面加载](https://www.tuicool.com/articles/uyE7Bvf)
* [HTML5 performance 前端加载性能初探](https://www.xuanfengge.com/h5-performance-front-end-load-performance-of.html)
