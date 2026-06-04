# linux-notes
linux学习笔记
一、   网络请求和下载
1、 ping 测试某个服务器是否可以联通,并且可以显示IP，-c为测试次数，例：ping -c 3 111.63.65.247。

2、 wget:文件下载，是 Linux非交互式命令行文件下载器，在终端内直接下载网络资源。可以在命令行中下载网络文件。
语法：wget [-b] url
选项与参数
-b（可选参数）：后台静默下载，下载日志自动保存在当前目录 wget-log 文件；
url：必填，资源的网络下载链接。
实操示例（Hadoop3.3.0 安装包下载）
 前台直接下载（实时看下载日志）wget http://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
   CTRL+C：可以终端下载，中断下载后会有残留的文件（ls查看），需要删除。例：rm -f hadoop-3.3.0.tar.gz  jdk-8u491-linux-x64.tar.gz
 后台下载（加 - b 参数）wget -b http://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
后台下载后会把输出写入至 “wget-log”，可以通过tail wget-log查看尾部状态，持续跟踪使用-f,如：tail -f wget-log。

3、 curl：可以发送http网络请求，可以用来下载文件、获取信息，-O用于下载文件，如：http://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
cip.cc:一个公开网站，可以用于获取自己主机的地址。
注意：Hadoop 下载慢原因 & 解决办法：变慢核心原因是你当前链接是Apache 官方国外源archive.apache.org，国内访问国际带宽受限，所以只有几十 KB/s，进度卡在 2%。可下载国内华为镜像（避开国外网络）： wget https://mirrors.huaweicloud.com/apache/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz

二、端口：Linux 系统总共有 65535 个端口，按用途分成 3 大类：1. 公认端口：1 ~ 1023；2. 注册端口：1024 ~ 49151；3. 动态端口：49152 ~ 65535。

1、 nmap IP地址：用于查看IP地址暴露的端口情况，安装nmap,yum -y install nmap
nmap 127.0.0.1查看本机IP地址的端口情况（127.0.0.1代表本机）

2、 netstat查看指定端口占用情况，安装netstat,yum -y install net-tolls
netstat语法：netstat -IP地址 | grep 端口号
netstat -anp :可以把系统中所有跟端口相关的或者跟网络链接相关的列出来（可以通过grep过滤查看需要的东西）例：netstat -anp |grep 22(端口号）
也可以通过进程号去查看端口的使用情况，如：netstat -anp |grep 580（进程号）
另外，也可以通过这个命判断某个端口是空闲还是被占用中，如netstat -anp |grep 12345  未显示说明系统中没有这个进程或者12345这个端口没有在使用。

三、进程管理:程序被运行启动后，操作系统会把它注册成一个进程；系统给每个进程分配唯一 PID（进程 ID 号），用来标识、管理进程。
    程序：存放在磁盘上的静态文件；
    进程：程序运行起来后，在内存里的动态实体。
ps:查看Linux系统中的进程信息
ps -ef:列出全部进程的全部信息（可以使用grep过滤） -e：显示系统所有进程   ；  -f：完整格式化输出，展示进程全字段信息
字段	含义
UID	运行进程的用户 ID（哪个用户启动）    ；   PID	当前进程唯一 ID（进程号）      ；PPID	父进程 ID，代表由哪个进程创建了本进程
C	进程 CPU 占用百分比    ；   STIME	进程启动的时    ；    TTY	启动进程的终端编号；值为?代表无终端、系统后台进程
TIME	进程累计占用 CPU 的总时长      ；    CMD	启动该进程的命令 / 程序全路径

  拓展常用搭配 ps -ef | grep 关键字   
  示例 1：查找 tail 相关进程    -->     ps -ef | grep tail
  示例 2：按进程号过滤      -->    ps -ef | grep 30001
补充说明:  grep 不只过滤进程名，PID、UID、启动时间、端口数字等任意字段内容，只要含关键字就会被匹配；


关闭进程：语法：   kill 进程id，     kill -9 进程id :  表示强制关闭某个进程。
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
