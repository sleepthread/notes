[http://blog.sina.com.cn/s/blog_a5e968370101crtl.html](http://blog.sina.com.cn/s/blog_a5e968370101crtl.html "http://blog.sina.com.cn/s/blog_a5e968370101crtl.html")

1、 Jacob是Java-COM Bridge的缩写，它在Java与微软的COM组件之间构建一座桥梁。使用Jacob自带的DLL动态链接库，并通过JNI的方式实现了在Java平台上对COM程序的调用。DLL动态链接库的生成需要windows平台的支持。

2、 Apache POI包括一系列的API，它们可以操作基于MicroSoft OLE 2 Compound Document Format的各种格式文件，可以通过这些API在Java中读写Excel、Word等文件。他的excel处理很强大，对于word还局限于读取，目前只能实现一些简单文件的操作，不能设置样式。

3、 Java2word是一个在java程序中调用 MS Office Word 文档的组件(类库)。该组件提供了一组简单的接口，以便java程序调用他的服务操作Word 文档。   
这些服务包括： 打开文档、新建文档、查找文字、替换文字，插入文字、插入图片、插入表格，在书签处插入文字、插入图片、插入表格等。填充数据到表格中读取表格数据 ，1.1版增强的功能： 指定文本样式，指定表格样式。如此，则可动态排版word文档。

4、 iText操作Excel还行。对于复杂的大量的word也是噩梦。用法很简单, 但是功能很少, 不能设置打印方向等问题。

5、 JSP输出样式基本不达标，而且要打印出来就更是惨不忍睹。

6、 用XML做就很简单了。Word从2003开始支持XML格式，大致的思路是先用office2003或者2007编辑好word的样式，然后另存为xml，将xml翻译为FreeMarker模板，最后用java来解析FreeMarker模板并输出Doc。经测试这样方式生成的word文档完全符合office标准，样式、内容控制非常便利，打印也不会变形，生成的文档和office中编辑文档完全一样。

7、补充一种方案，可以用类似ueditor的在线编辑器编辑word文档，在将html文件转换为xhtml文件，再转换为word。

8、利用PageOffice插件网页编辑word，还有weboffic插件等

参考网址

[http://www.officectrl.com/webofficeview.htm](http://www.officectrl.com/webofficeview.htm "http://www.officectrl.com/webofficeview.htm")

[http://www.zhuozhengsoft.com/PageOffice/](http://www.zhuozhengsoft.com/PageOffice/ "http://www.zhuozhengsoft.com/PageOffice/")

[http://www.itkeyword.com/doc/5122096026019575887/pageoffice-word](http://www.itkeyword.com/doc/5122096026019575887/pageoffice-word "http://www.itkeyword.com/doc/5122096026019575887/pageoffice-word")

[http://www.iqiyi.com/w_19rue2tp6t.html](http://www.iqiyi.com/w_19rue2tp6t.html "http://www.iqiyi.com/w_19rue2tp6t.html")

[https://www.cnblogs.com/qq742655/p/9025784.html](https://www.cnblogs.com/qq742655/p/9025784.html "https://www.cnblogs.com/qq742655/p/9025784.html")

[java生成pdf方案总结](https://www.cnblogs.com/qq742655/p/9025784.html "https://www.cnblogs.com/qq742655/p/9025784.html")

1. **Jasper Report**生成pdf：设计思路是先生成模板，然后得到数据，最后将两者整合得到结果。但是Jasper Report的问题在于，其生成模板的方式过于复杂，即使有IDE的帮助，我们还是需要对其中的众多规则有所了解才行，否则就会给调试带来极大的麻烦。

2. openoffice生成pdf：openoffice是开源软件且能在windows和linux平台下运行。

3. itext + flying saucer生成pdf：itext和flying saucer都是免费开源的，且与平台无关，结合css和velocity技术，可以很好的实现。

一般使用第三种方案比较多，它实现的步骤是非常简单的。

JAVA生成word优缺点对比

||||
|---|---|---|
|所用技术|优点|缺点|
|Jacob|功能强大|代码量大，设置样式繁琐；需要windows平台支持，无法跨平台|
|Apache POI|读写excel功能强大、操作简单|一般只用它读取word，能够创建简单的word，不能设置样式，功能太少|
|Java2word|功能强大，操作简单|能满足一般要求，不支持07格式，国人开发的，参考资料较多，需要windows平台支持|
|iText|功能全，能满足一般要求|不能直接生成或操作doc文档，只能生成rtf格式的文档，rtf也可以用word打开|
|JSP|操作简单，代码量少|能把当前页面导出简单的word，不能设置样式，美观性差，无法操作word|
|XML（最佳）|代码量少，样式、内容容易控制，打印不变形，完全符合office标准|需要提前设计好word模板，把需要替换的地方用特殊标记标出来|

JAVA生成pdf优缺点对比

||||
|---|---|---|
|所用技术|优点|缺点|
|openoffice|本身就是office软件，很容易设计一些文档模板，支持java调用实现word转换成pdf|需要先安装，设计好pdf模板样式，然后用程序来填充那些预留好的变量|
|itext|能满足要求，本身提供了一些api|无法识别很多html的tag和attribute，无法识别css，需要用其api函数来设置样式|
|**Jasper Report**|能满足要求，市面上使用的比较多，相关文档多|复杂，很难完全掌握，需要先设计模板，强依赖于IDE进行可视化编辑|
|**flying sauser****（最佳）**|能解析html和css输出成image、pdf等格式，操作简单，api强大|需要编写freemarker或velocity模板，打造html，勾画pdf的样式|