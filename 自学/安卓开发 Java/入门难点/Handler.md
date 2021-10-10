#### Handler
一种处理线程间交互的手段。

以下demo是当点击按钮后，原本的textview文字会发生变化
```java
public class MainActivity extends AppCompatActivity {
    Button btn;
    Thread thread;
    Handler handler;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        handler = new Handler(){
            @Override
            public void handleMessage(@NonNull Message msg) {
                super.handleMessage(msg);
                if(msg.what==0x123){
                    TextView textView = findViewById(R.id.textView);
                    textView.setText("改变");
                }
            }
        };

        btn = findViewById(R.id.button);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                thread = new Thread(new Runnable() {
                    @Override
                    public void run() {
                        handler.sendEmptyMessage(0x123);
                    }
                });
                thread.start();
            }
        });
    }

}
```

以上例子中不难发现，handler并没有与该应用程序有任何绑定行为，但却能响应处理。
不难理解，handler其实好比一个