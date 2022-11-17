---
date created: 2022-08-30 13:17
---

### vue+cesium-01开发环境搭建

最近做的毕设用到了cesium，这里给大家总结一下vue如何结合cesium

首先确定你使用的脚手架，vue-cli还是vite

插件 | Vite 官方中文文档 (vitejs.dev)

如果是vite，那么只需要在官方文档中找到社区插件，然后找到cesium安装即可使用

如果你是用vue-cli(大部分还是使用这个)，有三种方式可以引入cesium

**（注意：该方法对应的是vue2+vue-cli4）<u></u>~~~~****

最后可能，CDN的引入方法才最适合你的，有的时候不要死磕，时间成本很重要，遇到问题再解决。

#### 1配置webpack

**Cesium and webpack – Cesium**

第一种就是配置webpack，这种方法适合对webpack十分熟悉的大佬。
相信看这个视频的肯定webpack不熟吧
我也不熟，所以只针对小白简单科普一下。
vue-cli是基于webpack的构建vue项目的工具，也就是vue-cli搭建的项目模板，在运行时会打包、配置 、转义资源，提高效率
vue-cli在3之后就开始不再自动生成webpack.config.js，而是用手动添加vue.config.js来代替
vue-cli4搭建出来的项目不能正确打包解析cesium内文件，可以理解为cesium内文件结构的问题
如何配置webpack呢？
抄csdn（bushi）
其实就是因为cesium某些资源的路径不满足vue-cli默认打包规则，需要自定义一下。
官网的webpack示例，我也没看明白，CSDN上配置也千奇百怪。
总之我没找到比较官方的Cesium文件打包要做哪些事，估计要自己观察文件结构，结合CSDN来CTRL CV一个了。
小白不要轻易尝试，不然会出很多问题

> 说明：通过npm安装后需要配置的地方太多，所以放弃了

#### 2使用vue-cli-plugins插件

isboyjc/vue-cli-plugin-cesium: Cesium encapsulation based on Vue cli (github.com)

第二种是使用vue-cli的插件
这种方式最简单，不会出现问题，适合vue+cesium都不够熟悉的新手
这个插件是个人基于vue-cli-plugins的开发规则开发出来的，链接我也放在评论区了
使用方法也十分的简单，只需要按照要求安装即可。
需要注意的是，不要随意卸载。卸载后再安装会有语法检查不通过，通过不了就无法安装，无法安装就语法检查不通过，
通过了不了就无法安装…balabala

>说明：此模式需要vue-cli版本为3.X的，否则无法运行

#### 3使用vue-cesium

zouyaoji/vue-cesium: 🎉 Vue 2.x & Vue 3.x components for CesiumJS. (github.com)

然后就是使用vue-cesium，一个把cesium组件化的库，就像elementUI的用法一样
这种方法适合对vue和cesium都有一定程度了解的同学
使用方法是先按照文档安装，
然后根据示例，进行开发，就像Ant Design与elementUI一样。
但这种方法，我人为不适合新手，更适合给老手当生产力工具。
而且网上大部分教程都是手撸的JS。
所以，新手还是手撸js代码，比较合适。

#### 4.CDN的引入方法才最适合你的--正在测试

```
<link href="https://cesium.com/downloads/cesiumjs/releases/1.74/Build/Cesium/Widgets/widgets.css" rel="stylesheet">
<script src="https://cesium.com/downloads/cesiumjs/releases/1.74/Build/Cesium/Cesium.js"></script>
```

<https://cesium.com/ion/tokens?page=1>
在main.js中初始化 Cesium key

```
//github 登录

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI1ZmI2YmJkYS0zZThkLTRhMTUtYTQ2Mi03YmE5ZDliMWFmMTgiLCJpZCI6MTA1Mjg0LCJpYXQiOjE2NjA5MDM0NDl9.tUypGR1pmMWBPttZRcMZS6ELJ0a852rKZHoxIImG_9Q


Cesium.Ion.defaultAccessToken ='eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI1ZmI2YmJkYS0zZThkLTRhMTUtYTQ2Mi03YmE5ZDliMWFmMTgiLCJpZCI6MTA1Mjg0LCJpYXQiOjE2NjA5MDM0NDl9.tUypGR1pmMWBPttZRcMZS6ELJ0a852rKZHoxIImG_9Q'
```

原因是：在“about:blank”中阻止脚本执行，因为文档的框架已被沙盒化并且未设置“allow-scripts”权限。这个错误提示是Cesium不识别js，沙箱iframe不允许使用js。

解决方案：
解决方案：

第一种：禁用infobox。

```
const viewer = new Viewer('cesiumContainer', {
  infoBox: false, // If set to false, the InfoBox widget will not be created.
    });
```

完整代码

```
<link href="https://cesium.com/downloads/cesiumjs/releases/1.74/Build/Cesium/Widgets/widgets.css" rel="stylesheet">
	<script src="https://cesium.com/downloads/cesiumjs/releases/1.74/Build/Cesium/Cesium.js"></script>
	<script type="text/javascript">
		 window.CESIUM_BASE_URL = 'https://cesium.com/downloads/cesiumjs/releases/1.74/Build/Cesium/'
		Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI1ZmI2YmJkYS0zZThkLTRhMTUtYTQ2Mi03YmE5ZDliMWFmMTgiLCJpZCI6MTA1Mjg0LCJpYXQiOjE2NjA5MDM0NDl9.tUypGR1pmMWBPttZRcMZS6ELJ0a852rKZHoxIImG_9Q'
	</script>
```

#### 5.Vite2+Cesium+vite插件的形式，可以参考网上视频挺多的

参考：

[vue中使用cesium方法总结_赤红の果子的博客-CSDN博客_cesium vue](https://blog.csdn.net/m0_46635519/article/details/124102504)

[# Vue cli3 安装使用 cesium - 我是ed - 博客园 (cnblogs.com)](https://www.cnblogs.com/wjw1014/p/16081956.html)

[vue项目中CDN引用cesium_人生几何呢的博客-CSDN博客_cdn cesium](https://blog.csdn.net/ZcBob/article/details/121489000)

[VUE - Cesium引用 - 无心々菜 - 博客园 (cnblogs.com)](https://www.cnblogs.com/1285026182YUAN/p/16408040.html)

[vue框架集成cesium“黑科技” - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/150941280)

[vue+cesium实现页面嵌入地球 - 我是小可爱0000 - 博客园 (cnblogs.com)](https://www.cnblogs.com/wangyan0926/p/16453982.html)
