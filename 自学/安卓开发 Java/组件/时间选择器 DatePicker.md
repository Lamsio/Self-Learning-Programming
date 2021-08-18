#### 介绍
有时，我们想为程序添加一个时间选择器，方便用户选择时间而不是手动输入，安卓为开发者提供了一个类叫做`DatePicker`，该类可以定义一个日历表，从而方便用户进行日期选择，效果如下。

![image.png](https://i.loli.net/2021/08/18/XKWoThnCL5mZcA6.png)

#### 案例代码
点击日历表，并打印所选日期

```java
public class MainActivity extends Activity {

    private int year,month,day;
    private DatePicker datePicker;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        datePicker = findViewById(R.id.date);
        Calendar calendar = Calendar.getInstance();
        year = calendar.get(Calendar.YEAR);
        month = calendar.get(Calendar.MONTH);
        day = calendar.get(Calendar.DAY_OF_MONTH);
        datePicker.init(year, month, day, new DatePicker.OnDateChangedListener() {
            @Override
            public void onDateChanged(DatePicker datePicker, int i, int i1, int i2) {
                MainActivity.this.year = i;
                MainActivity.this.month = i1;
                MainActivity.this.day = i2;
                show(year,month,day);
            }
        });
    }
    private void show(int year,int month,int day){
        String str = year+"年"+(month+1)+"月"+day+"日";
        Toast.makeText(MainActivity.this,str,Toast.LENGTH_SHORT).show();
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
        <DatePicker
            android:id="@+id/date"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:calendarTextColor="@color/purple_700"
            android:headerBackground="@color/purple_700"
            >

        </DatePicker>
</LinearLayout>
```
#### 代码分析
首先，我们要初始化datePicker，需要调用`datePicker.init()`方法，这个方法中有四个参数需要填写，分别是`year`、`month`、`day`和`onDateChangedListener()`，datePicker会根据我们所填写的`year`、`month`、`day`显示日期，而最后的监听器则是用来监听日期的点击事件的。当用户点击日历表上的日期时，会执行该监听函数的行为

#### DatePicker 组件属性
```text
1. calendarTextColor: 定义日历的列表文字颜色
2. datePickerMode: 定义部件外观(spinner/calendar)
```