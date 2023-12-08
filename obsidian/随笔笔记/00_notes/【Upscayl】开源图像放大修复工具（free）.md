## 什么是 Upscayl ？

Upscayl 是一款通过 AI 模型进行图片放大并补全像素的工具。它的特点是：

- 开源免费；本地安装；
- 操作简单，4步搞定。虽然只提供英文界面，但是相信小白也可以轻松上手；
- 图片放大效果显著，尤其是，支持锐化图片，据说效果甚至优于 Photoshop；
- 跨平台，支持 windows / macOS 和 Linux 三大操作系统；
- 支持图像批处理，妥妥生产力工具。

最新版本下载网址：[https://github.com/upscayl/upscayl/releases/tag/v2.5.5](https://link.zhihu.com/?target=https%3A//github.com/upscayl/upscayl/releases/tag/v2.5.5)

## Upscayl 操作指南

Upscayl的 操作方法非常符合直觉，主要分为 4 个步骤：  
步骤1：点击【SELECT IMAGE】，选择待放大的图片（即原图）。  
步骤2：在【Select Upscaling Type】选择图片放大类型。

- REAL-ESRGAN：提高图片的清晰度；
- FAST REAL-ESRGAN：相比 REAL-ESRGAN 选项出图更快，只做锐化处理；
- REMACRI：增强图片效果；
- ULTRAMIX BALANCED：提高图片色彩饱和度；
- ULTRA SHARP：提高图片清晰度和锐化边缘；
- DIGITAL ART：提高颜色和纹理细节；

在这里，用户只需选择预设的放大类型，大大简化了操作难度，但是相应的，无法进行更加专业、细化的手动调节。  
步骤3：点击【SET OUTPUT FOLDER】选择导出文件夹。可不选择，默认保存在与原图相同的路径下。  
步骤4：点击【UPSCAYL】执行放大。  
放大效果说明  
示例说明：  
原图：由 Midjourney 输出；  
放大类型：DIGITAL ART，提高颜色和纹理细节。

![](https://pic4.zhimg.com/v2-3f9a9a7d28357d57002098c0a74003b7_b.jpg)

第一次放大：

- 原图尺寸：1115 × 625
- 放大尺寸：4460 × 2500
- 放大用时：大概 3 ~ 4 分钟
- 效果说明：

![](https://pic1.zhimg.com/v2-16bbb45ef4c748ba4f82bd21f3be9780_b.jpg)

整体对比。上图：放大前；下图：放大后。对于原图的整体提升效果显著，整个画面更加清晰。

![](https://pic2.zhimg.com/v2-5a13173ad6eadf34481744f874465f7d_b.jpg)

放大图片 100% 显示的细节对比。上图：放大前；下图：放大后。原有细节丢失，填充细节不足，感觉会比较假。  
第二次放大：

- 原图尺寸：4460 × 2500
- 放大尺寸：17840 × 10000
- 放大用时：极度缓慢，大概需要，15min
- 对比效果：

![](https://pic2.zhimg.com/v2-d6496ffa8195dcbe0aa2f8ed1a7a5041_b.jpg)

左上图：放大前；左下图：第一次放大后；右图：第二次放大后。用电脑浏览器显示，第二次放大和第一次放大，效果差别不明显，但是尺寸放大很多。  
当然，选择不同的放大类型，最终输出的图像效果也会有很大不同。

![](https://pic4.zhimg.com/v2-bffc2355aff69e3702cc85ce9d384653_b.jpg)

上图：放大类型设置为 DIGITAL ART，提高颜色和纹理细节；  
下图：放大类型设置为 REAL-ESRGAN，提高图片的清晰度；  
REAL-ESRGAN 的效果比 DIGITAL ART 好很多，不仅使原图的清晰度得到了很大的提升，细节也被很好地保留下来。  
其他的放大类型，就不在此一一介绍了，有兴趣的朋友不妨亲自体验下。  
个人使用感受  
之所以会想要找一款好用的图片放大工具，是因为，本人作为一名业余的斜杠图库摄影师，突然产生了一个“很鸡贼”的想法：有没有一种可能，使用 Midjourney 生成创意图片入库销售？  
不过现实的问题是，Midjourney 输出图片的视觉效果虽然酷炫，图片质量却不尽如人意——手机端姑且还能勉强用用，Web 端都很够呛，何况商用场景？关键要解决，如何在保证图片显示质量不降反升的情况下，小图变大图？  
总之，大概思路就是这样式儿的：  

![](https://pic4.zhimg.com/v2-67acf36afa86a702c034b906d1ec9d37_b.jpg)

初次体验 Upscayl 时，放大类型设置为 DIGITAL ART，看到输出结果时，会觉得：果然还是想多了；体验过 Real-Esrgan 之后，感觉又行了。  
  
Upscayl 算是完成度很高的 AI 应用了，更加难能可贵的是，竟然还开源免费的。  
官网链接：[https://www.upscayl.org](https://link.zhihu.com/?target=https%3A//www.upscayl.org/)  
Github 主页：[https://github.com/upscayl/upscayl](https://link.zhihu.com/?target=https%3A//github.com/upscayl/upscayl)  
默认安装的是 4x 模型，如果需要放大 2 倍或 3 倍的时候，需额外下载对应模型才能生效。如果没有对应模型你选择输出 2x 或 3x 时，会出现下面这种奇怪的拼接效果。

![](https://pic2.zhimg.com/v2-0bfa36c125fd09891740b6cd1ba5c1f5_b.jpg)

2x 和 3x 相关模型下载地址：[https://github.com/upscayl/upscayl/tree/main/models](https://link.zhihu.com/?target=https%3A//github.com/upscayl/upscayl/tree/main/models)

发布于 2023-07-05 03:23・IP 属地上海