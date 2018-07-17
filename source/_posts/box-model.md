---
title: box-model
date: 2018-07-17 09:22:57
tags:
---

# 盒模型

![box model](/images/boxdim.png)

* **Margin(外边距)** - 边框外的区域，外边距是透明的。
* **Border(边框)** - 围绕在内边距和内容外的边框。
* **Padding(内边距)** - 清除内容周围的区域，内边距是透明的。
* **Content(内容)** - 盒子的内容，显示文本和图像。

## Margin 属性

margin-top 与 margin-bottom 无法作用于非替换行内元素。

example:

<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/gw6cbvfe/embedded/html,css,result/"
        allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>
        
## Collapsing margins（外边距合并）

两个或多个盒子的margin如果相邻会发生外边距合并。外边距合并现象只发生在垂直方向上的margin，水平方向上的margin不会发生。

两个margin符合以下条件时会发生外边距合并：

* 在正常流内且处于同一个块格式化上下文的块级盒子的margin
* 没有行内盒，没有使用'clear'属性，没有padding，没有border分隔它们
* margin在垂直方向上符合以下任一种情况：
    - 某盒子的top margin与它第一个在正常流内的子级盒子的top margin
    - 某盒子的bottom margin与它下一个兄弟盒子的top margin
    - 父级盒子的bottom margin 与它的最后一个子级盒子的bottom margin，且父级盒子的height为auto
    - 某盒子的top margin与bottom margin，这个盒子不产生新的块格式化上下文，且min-hegith为0，且height为0或auto，且没有子级元素或子级元素都不在正常流内

上述规则可推导出以下三种常见情况：

### 相邻的兄弟元素之间

元素的bottom margin与相邻元素的top margin会发生外边距合并。兄弟元素的外边距合并不受border与padding影响，因为它们的margin并没有被分隔。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/de1nsqm6/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

如果元素浮动起来，那外边距合并会失效，因为它生成了新的块格式化上下文。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/khv1xjcn/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

如果元素的positon为absolute，那外边距合并会失效，因为它生成了新的块格式化上下文。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/fbcwL0pq/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

如果元素是inline-block，那么外边距合并会失效，因为inline-block生成的是行格式化上下文。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/bk5cu2me/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### 父元素与其第一个子元素之间

父元素的top margin与其第一个子元素的top margin会发生外边距合并。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/9mc1L2wo/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

如果元素浮动起来，那外边距合并会失效，因为它生成了新的块格式化上下文。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/urq2txn9/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

如果元素的positon为absolute，那外边距合并会失效，因为它生成了新的块格式化上下文。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/g59pserd/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

如果元素是inline-block，那么外边距合并会失效，因为inline-block生成的是行格式化上下文。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/urq2txn9/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

如果父元素的overflow属性不是visible，那么外边距合并会失效。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/xyna287w/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### 父元素与其最后一个子元素之间

父元素的bottom margin与其最后一个子元素的bottom margin会发生外边距合并的首要条件是父元素的height为auto。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/r2savt8g/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

影响外边距合并的因素与上述父元素与其第一个子元素之间外边跟合并的影响因素一样。不再举例。

### 空的块级元素

如果一个块级元素中不包含任何内容，且min-height为0，且height为0或者auto，且在其 margin-top 与 margin-bottom 之间没有边框、内边距、行内内容将它们分隔，则该元素的上下外边距会合并。如下例子：
<iframe width="100%" height="300" src="//jsfiddle.net/qw8880000/4dj9w8a1/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### 一些需要注意的情况

* 根元素不会发生外边距合并。
* 上述情况的组合会产生更复杂的外边距合并。
* 即使某一外边距为0，这些规则仍然适用。因此就算父元素的外边距是0，第一个或最后一个子元素的外边距仍然会“溢出”到父元素的外面。
* 如果参与合并的外边距中包含负值，合并后的外边距的值为最大的正边距与最小的负边距（即绝对值最大的负边距）的和。
* 如果所有参与合并的外边距都为负，合并后的外边距的值为最小的负边距的值。这一规则适用于相邻元素和父子元素。