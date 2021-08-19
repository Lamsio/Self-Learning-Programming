#### 介绍
我们在使用APP时，总能见到拖动条的存在，该组件能够便捷地帮助用户调整数值区间，在安卓开发中，他作为ProgressBar的子类，因此也能够调用父类方法。

#### 案例代码
拖动按钮，打印当前数值

```java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        SeekBar seekBar = findViewById(R.id.sk_bar);
        TextView textView = findViewById(R.id.text_id);
        seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
            // 当拖拽时
			@Override
            public void onProgressChanged(SeekBar seekBar, int i, boolean b) {
                textView.setText((CharSequence) Integer.toString(i));
            }
			// 当点击按钮时
            @Override
            public void onStartTrackingTouch(SeekBar seekBar) {
                Log.i("TAG","动了");
            }
			// 当松开按钮时
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
        <SeekBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:max="100"
            android:id="@+id/sk_bar"
            >
        </SeekBar>
        <TextView
            android:id="@+id/text_id"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="文字"
            >

        </TextView>
</LinearLayout>
```

#### SeekBar 组件属性
参考[[进度条 ProgressBar]]的属性