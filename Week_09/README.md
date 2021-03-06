# HTML 解析
## 第一步

* 为了方便文件管理，我们把parser单独拆到文件中
* parser接受HTML文本作为参数，返回一颗DOM树

## 第二步

* 我们用FSM来实现HTML的分析
* 在HTML标准中，已经规定了HTML的状态
* Toy-Browser只挑选其中一部分状态，完成一个最简版本

## 第三步

* 主要的标签有：开始标签，结束标签和自封闭标签
* 这一步暂时忽略属性

## 第四步

* 在状态机中，除了状态迁移，还要加入业务逻辑
* 在标签结束状态提交标签 token

## 第五步

* 属性值分为单引号，双引号，无引号三种
* 属性结束时，把属性加到标签 token 上

## 第六步

* 从标签构建 dom 树的基本技巧是用栈
* 遇到开始标签时创建元素并入栈，遇到结束标签出栈
* 自封闭节点可视为入栈后立刻出栈
* 任何元素的父元素是它入栈前的栈顶

## 第七步

* 与自封闭标签处理类似
* 多个文本节点需要合并

# CSS 计算

## 第一步：收集 CSS 规则

* 遇到 style 标签时，把 css 规则保存起来
* 调用 css parser 来分析 css 规则

## 第二步：添加调用

* 当创建一个元素后（startTag），立即计算 css
* 理论上，当分析一个元素时，所有 css 规则已经收集完毕
* 真实浏览器中，可能遇到写在 body 的 style 标签，需要重新 css 计算的情况，这里忽略

## 第三步：获取父元素序列

* 在 computeCSS 中，必须知道元素的所有父元素才能判断元素与规则是否匹配
* 从上一步骤的 stack 可以获取本元素的所有父元素
* 父元素的顺序应该从内到外

## 第四步：选择器与元素的匹配

* 选择器也要从当前元素向外排列
* 复杂选择器拆成针对单个元素的选择器，用循环匹配父元素队列

## 第五步：计算选择器与元素匹配

* 根据选择器的类型和元素的属性，计算是否与当前元素匹配
* 只实现了三种基本选择器，实际浏览器要处理复合选择器

## 第六步：生成 computed 属性

* 一旦选择匹配，就应用选择器到元素上，形成 computedStyle

## 第七步：css 优先级

* css 规则根据 specificity 和后来优先规则覆盖
* specificity 是一个四元组，越左边权重越高
* 一个 css 规则的 specificity 根据包含的简单选择器相加而成
