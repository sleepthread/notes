前言：有一部华为平板已经系统停止更新了，版本停留在安卓6，也没办法解锁，突然有个想法，想安装Termux装个linux用，然后就在百度找教程，找遍了，结果不是版本不能用，就是源安装不了工具，最终功夫不负有心人，成功在油管上找到了解决方法，现在记录一下，以便以后需要。

https://blog.csdn.net/yinlongtao/article/details/128482601

工具下载地址：

termux-v0.79-offline-bootstraps

链接：https://pan.baidu.com/s/1qRF8_zPjIll0t7PWjom4pg 
提取码：nd3p

注意：请下载这个版本的termux，其它版本的都不好用

教程如下：

1.手机安装上termux-v0.79-offline-bootstraps软件，然后打开



2.输入 apt update 和 apt upgraded 测试 发现报错 





3.删除原sources.list.d 创建新的源

rm -rf $PREFIX/etc/apt/sources.list.d
 
echo deb https://packages.termux.dev/termux-main-21/stable main > $RPEFIX/etc/apt/sources.list

echo deb https://packages.termux.dev/termux-main-21/ stable main > $PREFIX/etc/apt/sources.list
 

4.再输入apt update 然后发现能用了

5. 输入 apt upgrade 后，第一次提示输入Y，第二次输入N ,等待完成

至此，大功告成，已经可以正常使用了

常用工具下载:

apt install git
 
apt install vim 
 
apt install python 
开启SSH登录：

apt install openssh
 
whoami  // 查看用户
 
passwd //修改密码
 
sshd  //开启ssh 服务 -p 可以指定端口号（默认8022）  
授存储权限：

termux-setup-storage # 提示输入y
termux下安装centos、ubuntu、debian、kali：

pkg install python git proot -y
 
git clone https://github.com/sqlsec/termux-install-linux
 
cd termux-install-linux
 
python termux-linux-install.py
 
cd ~/Termux-Linux/CentOS  #进入centos安装目录,或者其它系统目录
 
./start-centos.sh  #执行启动脚本
 