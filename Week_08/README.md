## 浏览器基础渲染流程

我们看到的页面都是一个图片形式，专业点的说法叫做位图（Bitmap），然后经过显卡转换为我们可以识别的光信号。整个的过程就是从 URL 转换为 Bitmap 的过程，先发送请求到服务器，然后服务器返回 HTML，浏览器解析 HTML，然后构建 DOM 树，计算 CSS 属性，然后进行排版，最后渲染成位图，然后经过操作系统或硬件的 API 完成视图的显示。

![浏览器基础渲染流程示例图片](https://github.com/lujiajian1/Frontend-09-Template/blob/main/Week_08/img/%E6%B5%8F%E8%A7%88%E5%99%A8%E5%9F%BA%E7%A1%80%E6%B8%B2%E6%9F%93%E6%B5%81%E7%A8%8B.png)

## 有限状态机处理字符串

* 每一个状态都是一个机器（机器互相解耦）
    * 在每一个机器里，我们可以做计算、存储、输出.....
    * 所有的这些机器接受的输入是一致的
    * 状态机的每一个机器本身没有状态，如果我们用函数来表示的话，它应该是纯函数（无副作用）
* 每一个机器知道下一个状态
    * 每个机器都有确定的下个状态（Moore）
    * 每个机器根据输入决定下一个状态（Mealy）

```js
//每个函数是一个状态
function state(input) {
    //函数参数就是输入
    return next;//返回值作为下一个状态，返回的也是函数
}
//调用
while (input) {
    //获取输入
    state = state(input); //把状态机的返回值作为下一个状态
}
```

## ISO-OSI七层网络模型

![七层网络模型示例图片](https://github.com/lujiajian1/Frontend-09-Template/blob/main/Week_08/img/2.png)


## 第一步：http请求总结

* 设计一个HTTP请求的类
* content type是一个必要的字段，要有默认值
* body是KV格式
* 不同的content-type影响body的格式

## 第二步：send函数总结

* 在Request的构造器中收集必要的信息
* 设计一个send函数，把请求真实发送到服务器
* send函数应该是异步的，所以返回Promise

## 第三步发送请求

* 设计支持已有的connection或者自己新建connection
* 收到数据传给parser
* 根据parser的状态resolve Promise

## 第四步：ResponseParser总结

* Response必须分段构造，所以我们要用一个ResponseParser来"装配"
* ResponseParser分段处理ResponseText，我们用状态机来分析文本的结构

## 第五步：BodyParser总结

* Response的body可能根据Content-Type有不同的结构，因此我们会采用子Parser的结构来解决问题
* 以TrunkedBodyParser为例，我们同样用状态机来处理body的格式


# 补充

## 设计模式：状态模式