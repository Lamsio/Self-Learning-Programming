#### 介绍
一个普通的下拉菜单功能

#### 案例代码
XML实现 下拉菜单功能

```java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
    }
}
```
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#EAEAEA"
    android:padding="16dp"
    android:orientation="vertical"
    xmlns:android="http://schemas.android.com/apk/res/android">
    <Spinner
        android:layout_height="wrap_content"
        android:layout_width="wrap_content"
        android:entries="@array/option"
        >

    </Spinner>
</LinearLayout>
```
```xml
array.xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="option">
        <item>首页</item>
        <item>产品</item>
        <item>游戏</item>
        <item>网购</item>
        <item>关于我们</item>
    </string-array>
</resources>
```

Java代码实现 下拉菜单功能

#### 代码分析
首先，我们要初始化datePicker，需要调用`datePicker.init()`方法，这个方法中有四个参数需要填写，分别是`year`、`month`、`day`和`onDateChangedListener()`，datePicker会根据我们所填写的`year`、`month`、`day`显示日期，而最后的监听器则是用来监听日期的点击事件的。当用户点击日历表上的日期时，会执行该监听函数的行为

#### DatePicker 组件属性
```text
1. calendarTextColor: 定义日历的列表文字颜色
2. datePickerMode: 定义部件外观(spinner/calendar)
3. spinnersShown: 是否显示下拉菜单
4. firstDayOfWeek: 设置一周的第一天是哪一天
```