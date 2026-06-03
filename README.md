# linux-notes
linux学习笔记
网络请求和下载：ping 测试某个服务器是否可以联通，-c为测试次数
wget:文件下载，可以在命令行中下载网络文件，-b为后台下载
curl：可以发送http网络请求，可以用来下载文件、获取信息，-O用于下载文件
cip.cc:一个公开网站，可以用于获取自己主机的地址。
端口：物理端口和虚拟端口
nmap IP地址：用于查看IP地址暴露的端口情况，安装nmap,yum -y install nmap
nmap 127.0.0.1查看本机IP地址
netstat查看指定端口占用情况，安装netstat,yum -y install net-tolls
netstat语法：netstat -IP地址 | grep 端口号
