## 基本格式
```
<type>(<scope>):<subject>
//空一行
<body>
```
## 范例
```
fix(ES6): 修改错别字

修改错别字......
```
## 说明
``` 
type(必须)、scope(可选)、subject(必须)
//空一行
body(可选)
```
**1. type**   
用于说明 commit 的类别，目前只允许使用下面几种标识： 

* feat  (新功能)
* fix  (改bug)
* docs  （写文档）
* style  (格式化)    
* refactor  (重构)    
* test  （增加测试）
* chore  （构建工具变动）   

---
**2. scope**  
用于说明commit影响的范围，与具体业务相关。例如业务逻辑层、数据连接层、移动端、web端等。

---
**3. subject**    
subject是 commit 目的的简短描述，不超过50个字符。
一句话说清楚，本次提交的记录是干嘛用的。

---
**4. Body**  
是对本次 commit 的详细描述，可以分成多行。 如果subject可以说清楚，body部分可以省略。

---

[AngularJS commit规范](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#)
