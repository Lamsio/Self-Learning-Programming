## Main函数与代码块
`public static void main(String[] args){}`是最常见的入口函数，该函数是有JVM调用的

#### 类加载时机
1. 创建对象实例
2. 创建子类对象实例
3. 使用其静态成员

#### 代码块
代码块分为静态代码块以及普通代码块。

静态代码块有且只有一次执行，它随类加载执行，而普通代码块会在每次创建对象时执行。

普通代码块在创建对象时会被调用，如果是调用其静态成员则不会。

```java
//静态
static{

}
//普通
{

}
```

#### 静态成员与静态代码块优先级
两者优先级是一致的，因此执行顺序取决于书写的先后次序