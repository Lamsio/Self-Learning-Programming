#### 两者区别
###### Bundle 存数据
```java
Bundle bundle = new Bundle();  
bundle.putString("name","value");  
Intent intent = new Intent();  
intent.putExtras(bundle);
```
###### Bundle 取数据
```java
Bundle bundle = this.getIntent().getExtras();  
String str=bundle.getString("USERNAME");
```

#### 总结
Intent旨在传递数据，Bundle旨在存取数据

Intent内部还是调用Bundle来实现数据传递，只是封装了一层而已
