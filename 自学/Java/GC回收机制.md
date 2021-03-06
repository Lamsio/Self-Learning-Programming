下面就对[Java](http://lib.csdn.net/base/javase "Java SE知识库")中的垃圾回收和静态类型做一些总结：

### 一、Java中的[内存](https://so.csdn.net/so/search?q=%E5%86%85%E5%AD%98&spm=1001.2101.3001.7020)分配

> 1、stack(栈)，用于装变量和引用类型。如基本类型和引用类型的引用变量。   
> 2、heap(堆) ，用于装new出来的值。   
> 3、用来装[静态变量](https://so.csdn.net/so/search?q=%E9%9D%99%E6%80%81%E5%8F%98%E9%87%8F&spm=1001.2101.3001.7020)的区域。如static变量，字符串常量。   
> 4、用来装代码的区域。

### 二、[垃圾回收](https://so.csdn.net/so/search?q=%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6&spm=1001.2101.3001.7020)时机

> 1、栈上的变量一旦声明，出作用域即会被回收。   
> 2、堆里的对象，没有任何变量(栈上变量或静态区域的变量)指向这个对象的时候就会被回收，这个对象被标记为“垃圾对象”等待回收GC   
> 3、GC是只回收堆空间，检查定时回收（频率由GLR决定）。   
> 4、调用GC.Collect();“直接”回收对象（必须等GC处理完目前的任务，才来处理该任务）。

### 三、[静态成员](https://so.csdn.net/so/search?q=%E9%9D%99%E6%80%81%E6%88%90%E5%91%98&spm=1001.2101.3001.7020)的垃圾回收

  静态成员一般也可以分为静态基本类型和静态引用类型。   
  静态基本类型存储在在静态变量区域；静态引用类型的引用存储在静态变量区域，而实例（具体内容）存储在堆上。静态成员只存在一份，静态成员加载时机：类加载的时候（第一次访问），这个类中所有静态成员就会被加载在静态存储区，同时存储在[静态变量区域的成员一旦创建，直到程序退出才会被回收](http://blog.csdn.net/oTengYue/article/details/48108995#)。（注：如果是引用类型，如[static](https://so.csdn.net/so/search?q=static&spm=1001.2101.3001.7020) student myst=new student()，myst=null这时候，在静态存储区里面存的是一个地址（myst），这个地址指向在堆里面创建的student实例对象，当myst=null的时候，在静态存储区里面的变量会一直存在，但是在堆里面的student实例对象因为没有变量指向它，所以会被回收）。因此如果不用的静态引用类型可以通过设置=null方式让GC可以回收其堆上的空间。

### 四、单例模式中静态成员不会被垃圾回收机制回收

  单例模式中静态成员的声明由于静态的机制不会被GC回收，而对应的堆上实例对象在外部无法直接设为null，所以不会被垃圾回收机制回收。当然除非人为地断开单例中静态引用到单例对象的联接，否则jvm垃圾收集器是不会回收单例对象的