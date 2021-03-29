## proxy hook

[Proxy](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

## reactive实现原理

* 创建响应式代理对象，Proxy 对象。
* get方法中收集依赖。
* 在set方法中通知视图更新。

## CSSOM

CSSOM，即CSS Object Model，CSS对象模型，是对CSS样式表的对象化表示，同时还提供了相关API用来操作CSS样式。

## range

#### Range 对象
Range 对象表示文档中的连续范围。
#### document.createRange()
createRange() 方法创建 Range 对象。
#### Element.getBoundingClientRect()
返回元素的大小及其相对于视口的位置，如果是标准盒子模型，元素的尺寸等于width/height + padding + border-width的总和。如果box-sizing: border-box，元素的的尺寸等于 width/height。
#### insertNode()
在范围的开头插入一个节点，