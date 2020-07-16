# 表单

搜索框 登录框 文件上传 注册 留言板 

向服务器提交信息（写）
收集用户信息

交互
  双向交流
读写执行
  读取 获取信息
  写入 发出信息

小技巧： 管理控制台 f12 查看器（DOM/文档对象模型/树形结构）
控制台 可以执行js代码
调试器 略过
网络 页面的网络连接
存储 存储了页面的cookie信息等

<form></form>

表单本身是一个框架，表单里会有很多控件（元素）
action  数据提交到服务器的url
        如果为空，提交到当前页面
        也可以采用绝对路径和相对路径的格式
method  提交方法
  get url中有显示,url长度有限制
  post 可以上传文件等等 HTTP请求正文中
enctype:
  application/x-www-form-urlencoded  默认值
  multipart/form-data  上传文件时，必须要写

表单元素
  大部分
  <input/> 单标签
      type 属性
        password 密码框
        text     文本框
        radio    单选框
        checkbox 复选框
        reset    重置按钮
        submit   提交按钮
        file     文件域
        hidden   隐藏内容
      下拉列表
        <select>
          <options></options>
        </select>
      文本域
        <textarea></textarea>
        可以输入回车换行符

Burp Suite
  java 环境
  java -version

[css]
  层叠样式脚本
  HTML CSS 都是前端的内容
  HTML 四梁八柱
  CSS  装修公司
  提倡HTML和CSS分离
CSS 样式
  元素内容的颜色   color
  元素内容的背景色 background-color
  字体大小        font-size
颜色对照表 
RGB[0-255][0-255][0-255]
白色 255 255 255 ffffff
黑色 0 0 0 000000

CSS与HTML进行组合的时候有三种
1. 内联样式
  把样式表写在标签内部作为，标签中的style属性值出现
2. 内部样式
3. 外部样式
  css单独存放时，后缀名.css

选择器
  css给指定标签相应的样式
  标签选择器
  类选择器
  id选择器
vulnhub vulhub

iframe

### W3C 菜鸟教程

# HTML 超文本标记语言
编写网页的语言，解释性，写出来代码直接就能运行
  编译？
     C 源代码 -> 二进制文件 -> 计算机解释执行
源文件是纯文本格式
放在web根目录下
  .html
  .htm

html的运行环境是浏览器
标记语言
  尖括号包含关键字
  标签
    标签中有属性，属性对应属性值
    单标签
    双标签

HTML文档结构
  头部   文档控制信息,包括整个页面的说明和编码等等
  身体   真正显示文档内容的部分
```
<html>
  <head>
  </head>
  <body>

  </body>
</html>
```

常用标签
  <title></title> 浏览器标签页标题
  <meta charset="utf-8"> 通知浏览器我的编码格式是utf-8
  <h1></h1> 标题
  <p></p>   段落
  <hr />    水平线
  <br />    换行标签
  <span></span>    完成文字的控制
  <div></div>      块级元素
  <a></a>          超链接   从一个页面跳转到另一个页面
    href           跳转的地址
    target         默认情况下不用写，在当前标签页打开
                   写了"_blank",在新的标签页打开
  <img>            在页面中引入图片资源
    src            给定的图片地址
                   相对路径
                   绝对路径
  块级元素与行内元素

注释
  <!-- 
      注释不会显示在前台页面，但是会出现在源代码中
  -->

特殊字符
  空格       &nbsp;
  <          &lt;
  >          &gt;
  &          &amp;
  "          &quot;

表格
  <table></table>     定义表格
  <tr></tr>           定义行
  <td></td>           定义列
  colspan="2"         跨两列