#### 介绍
在一些网购或者外卖平台的评分系统，往往采用星级评分，这组件能够更直观地告诉用户评分机制，从而帮助他们完成评分。

#### 案例代码
点击星星，打印评分

```java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        RatingBar ratingBar = findViewById(R.id.rating);
        TextView textView = findViewById(R.id.text_id);
        ratingBar.setOnRatingBarChangeListener(new RatingBar.OnRatingBarChangeListener() {
            @Override
            public void onRatingChanged(RatingBar ratingBar, float v, boolean b) {
                textView.setText((CharSequence) Float.toString(ratingBar.getRating()));
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
        <RatingBar
            android:id="@+id/rating"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:numStars="6"
            ></RatingBar>
        <TextView
            android:id="@+id/text_id"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="文字"
            >

        </TextView>
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