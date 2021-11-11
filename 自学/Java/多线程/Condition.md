#### Condition
为了取代死板的`synchronized`，Java 5开始提供了[[ReentrantLock]]，但我们知道在`synchronized`中，我们可以搭配`wait()`和`notify()`实现随时唤醒与等待。

这种功能我们如何在`ReentrantLock`中实现呢？

