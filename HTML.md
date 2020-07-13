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