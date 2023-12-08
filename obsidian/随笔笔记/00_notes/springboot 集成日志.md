
在SpringBoot中它是内置了日志框架的，所以只要我们运行[SpringBoot日志](https://so.csdn.net/so/search?q=SpringBoot%E6%97%A5%E5%BF%97&spm=1001.2101.3001.7020)就会被打印在控制台上。但是输出的日志并不是开发者自己定义和打印的，还有一个问题就是控制台上面的日志是不能保存的，所以从这两个角度出发，提出来两个问题：1.开发者自定义打印日志；2.日志的持久化

https://blog.csdn.net/yahid/article/details/126959854
https://www.cnblogs.com/xiegongzi/p/16293103.html


slf4j
log4j2
logback


## 开发者自定义打印日志

自定义打印日志的步骤：

1.在程序中得到日志对象； 

2.使用日志对象的相关语法输出要打印的对象

```
private static Logger logger= LoggerFactory.getLogger(UserController.colass);

logger.info("");
```



## 日志的持久化 

日志持久化的方式有两种：

方式一：设置日志的保存路径 

```java
#配置日志目录logging:  file:    path: C:\Users\86158\Desktop\SSM框架\ssm-framework\
```

 上面这段代码的意思就是在指定路径下面创建spring.log日志文件

执行程序以后找到指定文件：

默认情况下springboot会有一个最大的日志大小限制，如果日志的文件大于默认的最大日志大小，那么springboot会从新启动一个日志 

方式二：设置日志文件的文件名

```java
#方式二：设置日志文件的文件名logging:  file:    name: spring.log
```

上面因为没有指定保存路径，所以它默认是保存在当前项目所在的目录里面：

### 使用[lombok](https://so.csdn.net/so/search?q=lombok&spm=1001.2101.3001.7020)的方式来输出日志

一：首先添加lombok框架，
二：使用@Slf4j注解输出日志
``` 
    @Slf4j 添加一个名为log的日志，使用slf4j
```