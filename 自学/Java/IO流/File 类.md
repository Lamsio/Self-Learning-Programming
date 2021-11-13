#### 简介
文件是计算机系统中非常重要的存储方式。Java提供了`File`对象供开发人员进行文件相关的操作

构建`File`对象时，需要在构造参数处传入文件的路径，如:

```java
File f = new File("C:\\Windows\\notepad.exe");
```

###### 注意
在Windows系统中，我们采用`\`作为路径分隔符。

在Linux系统中，我们采用`/`作为路径分隔符。

`.`用于表示当前目录，`..`用于表示上级目录。

#### 路径的表达形式
`File`对象提供了三种路径的表达形式
1. `getPath()` — 返回构建方法中传入的路径
2. `getAbsolutePath()` — 返回绝对路径
3. `getCanonicalPath()` — 返回规范路径

#### 文件与目录
`File`对象可以表示文件，也能表示目录。即使传入的路径并不存在，对象也不会报错，开发者可以使用`isFile()`和`isDirectory()`，判断该`File`是否是一个存在的文件或目录。

除此之外，还能调用:
- `boolean canRead()`: 是否可读
- `boolean canWrite()`: 是否可写
- `boolean canExecute()`: 是否可执行
- `long length()`: 文件的字节大小

#### 创建和删除
如果`File`表示为一个文件时，可以通过`createNewFile()`创建一个新的文件，用`delete()`即可删除。
```java
File file = new File("/path/to/file");
if (file.createNewFile()) {
    // 文件创建成功:
    // TODO:
    if (file.delete()) {
        // 删除文件成功:
    }
}
```

#### 遍历文件和目录

当File对象表示一个目录时，可以使用`list()`和`listFiles()`列出目录下的文件和子目录名。`listFiles()`提供了一系列重载方法，可以过滤不想要的文件和目录：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        File f = new File("C:\\Windows");
        File[] fs1 = f.listFiles(); // 列出所有文件和子目录
        printFiles(fs1);
        File[] fs2 = f.listFiles(new FilenameFilter() { // 仅列出.exe文件
            public boolean accept(File dir, String name) {
                return name.endsWith(".exe"); // 返回true表示接受该文件
            }
        });
        printFiles(fs2);
    }

    static void printFiles(File[] files) {
        System.out.println("==========");
        if (files != null) {
            for (File f : files) {
                System.out.println(f);
            }
        }
        System.out.println("==========");
    }
}
```
和文件操作类似，File对象如果表示一个目录，可以通过以下方法创建和删除目录：

-   `boolean mkdir()`：创建当前File对象表示的目录；
-   `boolean mkdirs()`：创建当前File对象表示的目录，并在必要时将不存在的父目录也创建出来；
-   `boolean delete()`：删除当前File对象表示的目录，当前目录必须为空才能删除成功。