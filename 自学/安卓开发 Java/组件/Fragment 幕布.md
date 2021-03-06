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
//MainActivity.java

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

```xml
//activity_main.xml

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <FrameLayout
        android:id="@+id/main_display"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintHeight_percent="0.9"
        ></FrameLayout>
    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintTop_toBottomOf="@id/main_display"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintHeight_percent="0.1"
        android:orientation="horizontal"
        >
        <ImageButton
            android:id="@+id/img1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintHorizontal_chainStyle="spread"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintEnd_toStartOf="@id/img2"
            android:src="@mipmap/ic_launcher"
            android:background="@android:color/transparent"
            >
        </ImageButton>
        <ImageButton
            android:id="@+id/img2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:layout_constraintLeft_toRightOf="@id/img1"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintStart_toEndOf="@id/img1"
            app:layout_constraintEnd_toStartOf="@id/img3"
            android:src="@mipmap/ic_launcher"
            android:background="@android:color/transparent"
            >
        </ImageButton>
        <ImageButton
            android:id="@+id/img3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:layout_constraintLeft_toRightOf="@id/img2"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintStart_toEndOf="@id/img2"
            app:layout_constraintEnd_toStartOf="@id/img4"
            android:src="@mipmap/ic_launcher"
            android:background="@android:color/transparent"
            >
        </ImageButton>
        <ImageButton
            android:id="@+id/img4"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:layout_constraintLeft_toRightOf="@id/img3"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toEndOf="@id/img3"
            android:src="@mipmap/ic_launcher"
            android:background="@android:color/transparent"
            >
        </ImageButton>
    </androidx.constraintlayout.widget.ConstraintLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
```
以上是简略代码，以上代码实现了每当用户点击不同的按钮，都会展示不同的内容

 ###### 获取Fragment的三种方式
```java
fragmentManager = getSupportFragmentManager();
// 通过id查找对应的Fragment实例
fragment1 = (StudyFragment) fragmentManager.findFragmentById(R.id.fragment_study1);
// 通过tag找到对应的Fragment，在动态加载和静态加载中都可以使用
 secondFragment = (SecondFragment) fragmentManager.findFragmentByTag("fragment_second");
// 获取添加到FragmentManager的所有Fragment，通过index访问，0代表最早添加的Fragment
fragmentManager.getFragments()
```
 
 ###### FragmentManager如何管理Fragment
 每次我们对Fragment的操作都需要通过FragmentTransaction，我们知道，Fragment继承自FragmentActivity，开发者希望我们在使用Fragment的时候只需要关注对Fragment的操作，而Fragment的管理则交由FragmentActivity的FragmentManager来实现。
 
 在FragmentAactivity这个类下面，当我们调用getSupportManager的时候
 ```java
public class FragmentActivity extends BaseFragmentActivityJB implements
        ActivityCompat.OnRequestPermissionsResultCallback,
        ActivityCompatApi23.RequestPermissionsRequestCodeValidator {
    ···
final FragmentController mFragments = FragmentController.createController(new HostCallbacks());
    
    ···

    public FragmentManager getSupportFragmentManager() {
        return mFragments.getSupportFragmentManager();
    }
    ···
}
 ```
 我们可以看到FragmentActivity下有个**FragmentController**，这个类定义了所有对Fragment的管理操作，包含了我们的Activity在`onCreate`,`onResume`,`onDestroy`等各种生命周期或回调对Fragment的影响，都由这个类来控制的。
 
 ###### FragmentTransaction的常见方法
 ```java
#将一个fragment实例添加到Activity里面指定id的容器中
add(Fragment fragment, String tag)
add(int containerViewId, Fragment fragment)
add(int containerViewId, Fragment fragment, String tag);
 #将一个fragment实例从FragmentManager的FragmentList中移除
remove(Fragment fragment);
#只控制Fragment的隐藏
hide(Fragment fragment)
#只控制Fragment的显示
show(Fragment fragment)
#清除视图，从containerid指定的Added列表移除，FragmentList依然保留
detach(Fragment fragment)
#创建视图，添加到containerid指定的Added列表，FragmentList依然保留
attach(Fragment fragment)
#替换containerViewId中的fragment，它会把containerViewId中所有fragment删除，然后添加当前的fragment
replace(int containerViewId, Fragment fragment)
replace(int containerViewId, Fragment fragment, String tag)
```
 