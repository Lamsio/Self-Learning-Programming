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

```
#### 代码分析
