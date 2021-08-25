#### 简介
可以理解为嵌入式Activity，每个Fragment拥有自己的生命周期，且只能依赖Activity存在，类似微信的界面就是通过Fragment实现的。

![image.png](https://i.loli.net/2021/08/25/VUnMsAGlYuIhJCq.png)

#### 静态Fragment
在主Activity中直接显示Fragment
```xml
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
```xml
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


```