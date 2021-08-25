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
Bundle bundle = new Bundle();  
bundle.putString("name","value");  
Intent intent = new Intent();  
intent.putExtras(bundle);
```