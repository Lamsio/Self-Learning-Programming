#### 简介
在Java中，我们如果需要执行IO流操作就需要依赖`InputStream`和`OutputStream`。我们常用`FileInputStream`从文件中读取数据，我们也使用`ServletInputStream`从HTTP请求中获取数据，如果我们想从TCP连接中获取数据，也能使用`Socket.getInputStream()`获取对应数据。

