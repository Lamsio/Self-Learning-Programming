#### 介绍
我们在使用APP时，总能见到拖动条的存在，该组件能够便捷地帮助用户调整数值区间，在安卓开发中，他作为ProgressBar的子类，因此也能够调用父类方法。

![image.png](https://i.loli.net/2021/08/18/XKWoThnCL5mZcA6.png)

#### 案例代码
点击日历表，并打印所选日期

```java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        SeekBar seekBar = findViewById(R.id.sk_bar);
        TextView textView = findViewById(R.id.text_id);
        seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
            @Override
            public void onProgressChanged(SeekBar seekBar, int i, boolean b) {
                textView.setText((CharSequence) Integer.toString(i));
            }

            @Override
            public void onStartTrackingTouch(SeekBar seekBar) {
                Log.i("TAG","动了");
            }

            @Override
            public void onStopTrackingTouch(SeekBar seekBar) {
                Log.i("TAG","停了");
            }
        });
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
3. spinnersShown: 是否显示下拉菜单
4. firstDayOfWeek: 设置一周的第一天是哪一天
```