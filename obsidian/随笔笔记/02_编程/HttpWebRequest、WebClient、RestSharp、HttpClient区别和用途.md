**HttpWebRequest** 已经不推荐直接使用了，这已经作为底层机制，不适合业务代码使用，比如写爬虫的时候  
**WebClient** 不想为http细节处理而头疼的coder而生，由于内部已经处理了通用设置，某些情况可能导致性能不是很理想  
**RestSharp** 兼具强大功能和友好api很适合业务中使用  
**HttpClient** 更加适用于异步编程模型中