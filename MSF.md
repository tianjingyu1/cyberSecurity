# Metasploit

是一个开源的渗透测试开源软件，也是一个逐步发展成熟的漏洞研究与测试代码开发平台，此外也将成为支持整个渗透测试过程的安全技术集成开发与应用环境。

- 技术架构

辅助模块
渗透攻击模块
攻击载荷模块
空指令模块
编码器模块
后渗透攻击模块
免杀模块


MSF-软件更新

[apt-get update]
[apt-get install metasploit-framework]
一个模块就是一个rb脚本

meterpreter
- 常用基本命令

命令                解释
background          将Meteroreter终端隐藏在后台
sessions            查看已经成功获取的会话。-i 选项，切入后台会话
shell               获取系统的控制台shell
quit                关闭当前的Meterpreter会话，返回MSF终端
pwd                 获取目标机上当前的工作目录
cd                  切换目录
ls                  查看当前目录下内容
upload              上传文件
cat                 查看文件内容
edit                编辑文件
download            下载文件
search              搜索文件
ifconfig/ipconfig   查看网卡信息
route               查看路由信息，设置路由
sysinfo             查看系统信息
getuid              获取当前用户id
ps                  查看进程
getpid              查看当前进程
migrate             切换进程
execute             执行文件
kill                终结指定PID的进程
shutdown            关机
screenshot          屏幕快照