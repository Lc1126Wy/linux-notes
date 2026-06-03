# linux-notes
linux学习笔记
网络请求和下载：ping 测试某个服务器是否可以联通，-c为测试次数
wget:文件下载，可以在命令行中下载网络文件，-b为后台下载
curl：可以发送http网络请求，可以用来下载文件、获取信息，-O用于下载文件
cip.cc:一个公开网站，可以用于获取自己主机的地址。
端口：物理端口和虚拟端口
nmap IP地址：用于查看IP地址暴露的端口情况，安装nmap,yum -y install nmap
nmap 127.0.0.1查看本机IP地址的端口情况
netstat查看指定端口占用情况，安装netstat,yum -y install net-tolls
netstat语法：netstat -IP地址 | grep 端口号
进程管理:
ps:查看Linux系统中的进程信息
ps -ef:列出全部进程的全部信息（可以使用grep过滤）
关闭进程：kill，语法：kill -9:表示强制关闭进程
查看系统整体资源（top）；查看磁盘信息监控（df),df -h可以显示更完整的单位信息。
磁盘监控信息：
iostat：查看cpu和磁盘的相关信息
语法：iostat -x [num1] [num2]:-x表示可以显示更多信息，num1：刷新间隔；num2：刷新几次。
网络状态监控：sar;  语法：sar -n DEV num1 num2(-n查看网络，DEV表示查看网络接口）
环境变量：
env:查看当前系统中记录的环境变量
环境变量：PATH，无论/当前是什么工作目录，都能执行/usr/bin/cd这个程序。验证：使用env | grep PATH
(执行程序的搜索路径）
$：用于取变量的值，如：echo $PATH通过echo语句输出出来；echo $(PATH)ABC
自行设置环境变量：
临时设置：export 变量名=变量值
永久生效：针对当前用户生效，配置在当前用户的：~/bashrc文件中
针对所有用户生效，配置在系统的：/etc/profile文件中
通过语法source配置文件
