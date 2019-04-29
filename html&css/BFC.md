# 规则
1. 同一个BFC内的块，在垂直方向上顺序排列。
2. BFC不会与float元素重合。
3. 计算BFC高度时，内部的浮动元素也会参与计算。
4. 属于同一个BFC内的box，垂直方向的margin会发生重叠。
5. BFC内的元素会紧贴左边。

# 产生条件
* 根元素
* float: left/right     
* display: inline-block/table-cell/table-caption
* overflow: 不为visible
* position: absolute/fixed

