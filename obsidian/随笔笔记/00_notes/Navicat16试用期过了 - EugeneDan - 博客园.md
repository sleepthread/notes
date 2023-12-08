我之前下载安装的Navicat是设定定期更新的，可是一次弹出来定期更新的窗口被我不小心关掉了，就过期了，于是试着更新一下，按下面方法成功了惹

1，关闭navicat  
2，首先win+R，输入regedit。  
3，找到HKEY_CURRENT_USER-->Software-->Classes-->CLSID-->下面文件夹中有info的删除掉。没有这个文件，就去那堆文件夹里找子文件有info的，有把那个文件夹 里外都删掉，就是删E2那个。  
![](file://E:/notes/joplin/resources/66ecdb360c7b496985407466db0a7bc5.png?t=1680490287446)

4，这个是重点，网上其他文章是找到HKEY_CURRENT_USER-->Software-->PremiumSoft--data,删除data；但是我是没有data这个文件夹的，所以这边就不管。而我是把HKEY_CURRENT_USER-->Software-->PremiumSoft下面的和navicat相关的所有文件夹，PremiumSoft下面的文件夹有navicat名字都删掉。我的这个下面就只有一个Navicat文件夹，我直接把Navicat文件夹删了，就可以了。

![](file://E:/notes/joplin/resources/715e6de8deb14efea8dc317e1dc88839.png?t=1680490287577)