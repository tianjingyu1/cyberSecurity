# JavaScript（ECMAScript）
JS的运行环境是浏览器
前端安全
解释型语言
每次刷新界面，JS代码都会执行
从上到下依次执行
当直接访问JS脚本的时候，返回纯文本内容

快速入门
  JS与HTML混编
  任何位置
简单的语句
  输出语句
```
  alert();     //弹窗
  console.log();     //在控制台输出
```

## 如何在HTML中引入JS代码

1. 内部<script></script>
2. 外部type="text/javascript"

变量
  声明变量
  var          强烈建议
  var name

  变量类型
    Number
        1+1
    字符串
    布尔类型变量
    null和undefined
    null表示一个“空”的值，它和0以及空字符串''不同，0是一个数值，''表示长度为 0的字符串，而null表示“空”。
    在其他语言中，也有类似JavaScript的null的表示，例如Java也用null，Swift用nil,Python用None表示。但是，在JavaScript中，还有一个和null类似的undefined,它表示“未定义”。
    JavaScript的设计者希望用null表示一个空的值，而undefined表示值未定义。事实证明，这并没有什么卵用，区分两者的意义不大。大多数情况下，我们都应该用null，undefined仅仅在判断函数参数是否传递的情况下有用

    数组
      包含任意数据类型

  流程控制
    for 
    for in 
    while
    do while
    
    对象
     
  

DOM 文档对象模型