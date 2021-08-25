#### 简介
可以理解为嵌入式Activity，每个Fragment拥有自己的生命周期，且只能依赖Activity存在，类似微信的界面就是通过Fragment实现的。

![image.png](https://i.loli.net/2021/08/25/VUnMsAGlYuIhJCq.png)

#### 静态Fragment
在主Activity中直接显示Fragment
```java
//MainActivity.java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

    }
}
```
```xml
//activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:android="http://schemas.android.com/apk/res/android">
    <fragment
        android:id="@+id/fragment1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:name="com.example.activity_learning.BlankFragment"></fragment>
</LinearLayout>
```
```java
//BlankFragment.java
public class BlankFragment extends Fragment {
    View root;
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        if (root==null){
            root = inflater.inflate(R.layout.fragment_blank,container,false);
        }

        Button btn = root.findViewById(R.id.btn);
        TextView textView = root.findViewById(R.id.textview);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                textView.setText("已点击");
            }
        });


        return root;
    }
}

```
```xml
//fragment_blank.xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".BlankFragment">

    <!-- TODO: Update blank fragment layout -->
    <TextView
        android:id="@+id/textview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="@string/hello_blank_fragment" />
    <Button
        android:id="@+id/btn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="按下我"
        >

    </Button>
</FrameLayout>

```

以上的案例是直接加载Fragment进Activity中，但实际应用中，我们往往都需要动态加载而不是静态加载。

**切记！布局文件中的Fragment标签必须包含id属性！！！！**

#### 动态加载
###### 静态与动态区别
上述静态案例我们可知，当该Activity加载时，就直接将Fragment加载到页面上，而动态加载则是通过触发某些事件从而展示相应的Fragment，例如点击不同的按钮展示不同的fragment

```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ImageButton btn,btn1,btn2,btn3;
        btn = (ImageButton) findViewById(R.id.img1);
        btn1 = (ImageButton) findViewById(R.id.img2);
        btn2 = (ImageButton) findViewById(R.id.img3);
        btn3 = (ImageButton) findViewById(R.id.img4);

        btn.setOnClickListener(this);
        btn1.setOnClickListener(this);
        btn2.setOnClickListener(this);
        btn3.setOnClickListener(this);

    }

    @Override
    public void onClick(View view) {
        switch (view.getId()){
            case R.id.img1: replaceFragment(new BlankFragment());break;
            case R.id.img2: replaceFragment(new BlankFragment2());break;
            case R.id.img3: replaceFragment(new BlankFragment3());break;
            case R.id.img4: replaceFragment(new BlankFragment4());break;
        }
    }

    private void replaceFragment(Fragment fragment){
        FragmentManager fragmentManager = getSupportFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        Log.i("ALL",fragmentManager.getFragments().toString());
        fragmentTransaction.replace(R.id.main_display,fragment);
        fragmentTransaction.addToBackStack(null);
        fragmentTransaction.commit();
    }
}
```