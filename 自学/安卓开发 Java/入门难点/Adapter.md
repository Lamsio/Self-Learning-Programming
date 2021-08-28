#### 简言
每当我们尝试实现 List 时，都不可避免地要用到 Adapter ，因此，在搞懂 Adapter 前，我们需要先了解View的基本信息。

#### 逻辑
Adapter: 适配器

AdapterView: 适配器View

使用时，一般是适配器中填充数据，再将适配器配置给适配器View进行显示

#### ListView
当我们尝试列出一串数据时

![image.png](https://i.loli.net/2021/08/14/GNkMixQR3Y1gudv.png)

我们总会需要用到ListView，ListView能够很好地帮我们列出数据。

#### BaseAdapter
这是一个十分常用的Adapter，我们可以基于此类进行拓展。以下列出Adapter之间的关系

![image.png](https://i.loli.net/2021/08/14/YXys9UagKwIhljb.png)

#### ArrayAdapter
适用于每一项都是字符串的情况下

```java
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,android.R.layout.simple_list_item_1,new String[]{"小明","小红"})
```

上述代码中，构造器第一个参数是`context 上下文`，第二个是列表模板，第三个是数据源

#### 点击事件
有时，我们想为每一项都添加一个点击事件，那么我们可以使用以下代码实现事件绑定。

```java
...
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ListView ls = findViewById(R.id.listview);
        ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(this,R.array.product_list, R.layout.array_adapter_item);

        ls.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
                Toast.makeText(MainActivity.this,"索引"+l+"??:"+i,Toast.LENGTH_SHORT).show();
            }
        });
        ls.setAdapter(adapter);
    }
```

除了`setOnItemClickListener`事件外，我们也可使用`setOnItemLongClickListener`，当用户长按时就会触发。

接下来的案例会实现长按删除功能

```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        List<String> list = new ArrayList<String>();
        list.add("小号");
        list.add("大号");
        list.add("中号");

        ListView ls = findViewById(R.id.listview);
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,R.layout.array_adapter_item,list);
        ls.setAdapter(adapter);
        ls.setOnItemLongClickListener(new AdapterView.OnItemLongClickListener() {
            @Override
            public boolean onItemLongClick(AdapterView<?> adapterView, View view, int i, long l) {
                 list.remove(i);
                 adapter.notifyDataSetChanged();
                 return true;
            }
        });

    }
```

可以注意到，我在第77行写了一句`adapter.notifyDataSetChanged();`，每当我们更改源数据，必须告知系统我们更改了数据，以便提醒他更新。

#### SimpleAdapter
单单的一串文字，压根就不够我们实现需求，如果我们想添加多控件怎么办呢？

SimpleAdapter 可以很好地解决这个问题

`TestSimpleAdapter.java`
```java
    private ListView lv;
    private SimpleAdapter adapter;
    private List<Map<String,Object>> list = new ArrayList<Map<String,Object>>();
    private Map<String,Object> map;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        lv = findViewById(R.id.listview);

        for (int i = 0; i < 10; i++) {
            map = new HashMap<String,Object>();
            map.put("title","标题"+i);
            map.put("intro","内文"+i);
            list.add(map);
        }

        String[] from = {"title","intro"};
        int[] to = {R.id.title,R.id.intro};
        //参数1: 上下文对象 参数二: 数据源List<Map<String,Object>> 参数三: item对应的布局文件 参数四: 表示由map中定义的key组成的字符串类型的数组 参数五: 需要显示的控件id组成的int类型的数组
        // 一定要确保参数四和参数五 一一对应
        adapter = new SimpleAdapter(this,list,R.layout.simple_adapter_test,from,to);
        lv.setAdapter(adapter);
    }
```
`simple_adapter_test.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal">

    <TextView
        android:id="@+id/title"

        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        >

    </TextView>
    <TextView
        android:id="@+id/intro"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="28sp"
        android:padding="5dp"
        >

    </TextView>
</LinearLayout>
```

#### 自定义Adapter
虽然上面的SimpleAdapter挺常用的，但还是局限了自由度

我们该如何创建一个完完全全自定义的Adapter呢？

代码展示
```java
public class MyAdapter extends AppCompatActivity {

    private List<String> list;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        list = new ArrayList<String>();
        for (int i = 0; i < 40; i++) {
            list.add("这是第"+i+"条数据");
        }

        CustomAdapter adapter = new CustomAdapter();
        ListView lv = findViewById(R.id.listview);
        lv.setAdapter(adapter);

    }

    class CustomAdapter extends BaseAdapter{
        // 计算有多少个Item要显示在View里面
        @Override
        public int getCount() {
            return list.size();
        }
        // 获取指定Item对象
        @Override
        public Object getItem(int i) {
            return list.get(i);
        }
        //获取每个Item的ID值
        @Override
        public long getItemId(int i) {
            return i;
        }
        //获取每个Item对应的View视图
        @Override
        public View getView(int i, View view, ViewGroup viewGroup) {
            // 1. 将XML转化位View对象
            // 2. 给View对象中的控件进行赋值
            LayoutInflater inflater = LayoutInflater.from(MyAdapter.this);
            View my_view = inflater.inflate(R.layout.my_adapter,null);
            TextView textView = my_view.findViewById(R.id.myadapter_tv);
            textView.setText((CharSequence) getItem(i));
            return my_view;
        }
    }
}
```

核心思想：
1. ListView中每行Item的布局XML
2. getView方法用于定义如何处理每行数据的渲染
###### LayoutInflater
布局映射器，其作用是将XML映射为一个View对象

我们可以通过`LayoutInflater.from()`得到布局映射器对象，然后再调用其`inflate()`方法去获得XML的View对象

###### Adapter 工作原理
Adapter是ListView和数据间的桥梁

ListView在绘制时，系统先调用`getCount()`得到ListView的长度，然后根据长度调用`getView()`一行行地绘制ListView的每一项

当ListView的每一项将要显示时，都会调用Adapter中的`getView()`方法返回一个View。

ListView有多少项，就调用多少次`getView()`方法去创建每一项View，这一过程将耗时。

###### ListView的缓存原理
ListView先通过`getView()`方法请求一个View，然后请求其他可见View。`convertView`在`getView`中是空的(null)。当列表第一项滚出屏幕，并且一个新的项从屏幕底端上来时，ListView会再请求一个View，此时，convertView已经不是空值了，他的值将是滚出屏幕的第一项，之后只需要设定新的数据，然后返回convertView即可，而不是再创建一个View

#### RecyclerView.Adapter
自定义Adapter继承该类后，有以下几个方法需要重载
1. onCreateViewHolder
2. onBindViewHolder
3. getItemCount

此外，还需要为其自定义一个ViewHolder，该ViewHolder需要继承RecyclerView.ViewHolder

在自定义的ViewHolder中需要将所有需要渲染的数据写入进去

例如我预期List中每行都会渲染一个图片和文字，那么自定义ViewHolder则是如下:
```java
        class MyViewHolder extends RecyclerView.ViewHolder{

            ImageView imageView;
            TextView textView;

            public MyViewHolder(@NonNull View itemView) {
                super(itemView);
                imageView = itemView.findViewById(R.id.icon);
                textView = itemView.findViewById(R.id.name);
            }
        }
```

###### onCreateViewHolder
该方法类似于ListView的`getView()`方法，但在其之上还增加了`ViewHolder`的特性

我们在该方法中需要返回一个ViewHolder对象

```java
        @NonNull
        @Override
        public MyAdapter.MyViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
            View v = LayoutInflater.from(parent.getContext()).inflate(R.layout.each_item,null,false);
            MyViewHolder myViewHolder = new MyViewHolder(v);
            Log.i("AKBCD",myViewHolder.toString()+"是OnCreate");
            return myViewHolder;
        }
```

###### onBindViewHolder
每当有新项目生成/旧项目滚入时，就会调用该方法

```java
        @Override
        public void onBindViewHolder(MyAdapter.MyViewHolder holder, int position) {
            holder.textView.setText(mData.get(position).getIntro());
            holder.imageView.setBackgroundResource(mData.get(position).getPic());
        }

```