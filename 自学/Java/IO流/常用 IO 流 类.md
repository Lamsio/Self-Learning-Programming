## InputStream/OutputStream
#### File
FileInputStream, FileOutputStream是比较常用的IO类，其作用是读取指定文件中的内容

#### Buffered
在平常的底层流的使用中，效率低下，CPU与IO的互动慢。我们把多个字节的数据丢入内存中，让CPU能与其直接互动，提高效率。