`Wait()`与`Notify()`常出现在多线程编程中，当线程想保留资源且希望线程能够随时重获资源时，就需要使用这两个函数。

```java
class TaskQueue {
    Queue<String> queue = new LinkedList<>();

    public synchronized void addTask(String s) {
        this.queue.add(s);
    }

    public synchronized String getTask() {
        while (queue.isEmpty()) {
        }
        return queue.remove();
    }
}
```
上面这段代码中，当我们调用`addTask()`时，能为队列添加元素，由于该方法声明了`synchronized`，因此会将资源上锁。而当我们调用