#### 简介
Drawable 指“可绘制的东西”的抽象类，被定义在 android.graphics.drawable 包下。

当我们意图定制一些效果时（如：按下按钮会更换颜色），我们会用到这个去自定义效果。

```text
获取 Drawable 对象有三种方式：
- 使用工程资源文件中保存的图像资源。
- 使用 XML 文件定义的 Drawable 属性。
- 通过构造方法构建。
```

#### 资源文件中创建Drawable对象
系统会自动为每个drawable文件夹下的资源文件生成一个格式为`R.drawable.xxx`的id号，再工程中我们可以通过这个id去获取资源的对象

假如在`res/drawable/`路径下，有一个资源文件`my_image.png`，系统将为其生成资源ID为R.drawable.my_image.

```java
ImageView i=new ImageView(this);
i.setImageResource(R.drawable.my_image);
```

但这个`R.drawable.my_image`只是一个整数而已，如果要获取Drawable对象，则需要:

```java
Resources res=mContext.getResources();
Drawable myImage=res.getDrawable(R.drawable.my_image);
```

#### XML文件中创建Drawable对象
常见的方式是在`drawable`文件夹下创建`Drawable resource file`，假设文件描述如下:

```xml
<transition xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@drawable/image_expand">
    <item android:drawable="@drawable/image_collapse">
</transition>
```

从该 XML 文件中获取 TransitionDrawable 对象的代码如下：

```java
Resources res=mContext.getResources();
TransitionDrawable transition=(TransitionDrawable);
res.getDrawable(R.drawable.expand_collapse);
ImageView image=(ImageView)findViewById(R.id.toggle_image);
image.setImageDrawable(transition);
```

#### 使用构造方法创建 Drawable 对象
以 ShapeDrawable 为例，ShapeDrawable 是 Drawable 的子类，ShapeDrawable 对象适合动态绘制二维图形。

以下代码演示了使用 ShapeDrawable 对象在自定义 View 组件上绘制一个椭圆的过程：

```java
public class CustomDrawableView extends View {
    private ShapeDrawable mDrawable;

    public CustomDrawableView(Context context) {
        super(context);

        int x = 10;
        int y = 10;
        int width = 300;
        int height = 50;

        mDrawable = new ShapeDrawable(new OvalShape());
        mDrawable.getPaint().setColor(0xff74AC23);
        mDrawable.setBounds(x, y, x + width, y + height)
    }

    protected void onDraw(Canvas canvas) {
        mDrawable.draw(canvas);
    }
}
```

绘制完成后，可通过以下代码将自定义的 View 组件设置为 Activity 的视图：
```java
CustomDrawableView mCustomDrawableView;
protected void onCreate (Bundle savedInstanceState) {
    super.onCreate (savedInstanceState); mCustomDrawableView=new CustomDrawableView (this);

    setContentView (mCustomDrawableView);
}
```

自定义的 View 组件也可以通过以下代码被放置到 XML 文件中使用：
```xml
<introducton.android.shapedrawable.CustomDrawableView
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
/>
```

#### StateListDrawable
StateListDrawable是Drawable资源的一种，可以根据不同状态，设置不同的图片效果，关键节点是`<selector>`，我们只需要将Button的background属性设置为该drawable资源，就可以轻松实现。

#### StateListDrawable 常见属性
```text
1. drawable: 引用的Drawable位图
2. state_focused: 是否获得焦点
3. state_pressed: 控件是否被按下
4. state_enabled: 控件是否可用
5. state_selected: 控件是否被选择
6. state_checked: 控件是否被勾选
7. state_checkable: 控件是否可以被勾选
8. state_window_focused: 是否获得窗口焦点
9. state_active: 控件是否处于活动状态, eg: slidingTab
10. state_single: 控件包含多个子控件时，是否只显示一个子控件

```