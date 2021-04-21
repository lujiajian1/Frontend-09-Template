## 第一步

* 为了方便文件管理，我们把parser单独拆到文件中
* parser接受HTML文本作为参数，返回一颗DOM树

## 第二步

* 我们用FSM来实现HTML的分析
* 在HTML标准中，已经规定了HTML的状态
* Toy-Browser只挑选其中一部分状态，完成一个最简版本