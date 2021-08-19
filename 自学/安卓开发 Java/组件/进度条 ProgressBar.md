#### 介绍
有时，我们想为程序添加一个进度条，进度条分为两种，一种是实时进度条(横条)，另一种是等待进度条(衔尾蛇)。

在这份笔记中将会举例以上两种情况的使用。


#### 案例代码
每次点击按钮，进度条+10

```java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ProgressBar progressBar = findViewById(R.id.progress_test);
        Button btn = findViewById(R.id.btn);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                progressBar.setProgress(progressBar.getProgress()+10);
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
        <ProgressBar
            android:id="@+id/progress_test"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            style="?android:attr/progressBarStyleHorizontal"
            >
        </ProgressBar>
        <Button
            android:id="@+id/btn"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="点我"
            >

        </Button>
</LinearLayout>
```
#### 代码分析
首先，我们要初始化datePicker，需要调用`datePicker.init()`方法，这个方法中有四个参数需要填写，分别是`year`、`month`、`day`和`onDateChangedListener()`，datePicker会根据我们所填写的`year`、`month`、`day`显示日期，而最后的监听器则是用来监听日期的点击事件的。当用户点击日历表上的日期时，会执行该监听函数的行为

#### DatePicker 组件属性
```text
1. style="?android:attr/progressBarStyleHorizontal" 实时进度
2. style="?android:attr/progressBarStyleSmall" 小的衔尾蛇
3. style="?android:attr/progressBarStyleLarge" 大的衔尾蛇
4. max: 进度条最大值
```