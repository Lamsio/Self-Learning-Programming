#### 简介
这个布局相比其他布局而言，内容更加庞大，他是集前集中布局之总和。

该布局主要思想类似于弹簧，位于约束布局下的组件将拥有`TOP`,`LEFT`,`RIGHT`以及`BOTTOM`四种方向，设计者能够将组件的某个方向点绑定至另一个组件的方向点上，例如将组件A的LEFT绑定到组件B的RIGHT上，从而实现组件A左侧贴合组件B右侧的效果，这种思想恰似物理学中的力

在约束布局下的所有组件**必须设置约束**，否则在执行程序时组件将处于坐标轴0,0的位置

#### 基本方向约束
```text
app:layout_constraint[X]_to[Y]Of

X和Y: Start,End,Left,Right,Top,End

如: app:layout_constraintLeft_toLeftOf="@id/tv1"

将该组件的左侧点绑定至id为tv1的组件的左侧
```

#### 水平/垂直偏移
我们可以通过为组件添加`app:layout_constraintHorizontal_bias=""`属性，设置组件的偏移量，一般情况下，如果设置为0，则向左贴齐，但有些特殊情况可能有偏差，例如组件本身占据整个宽度，亦或者焦点重叠，都会使bias与预期不符。
#### 链条布局
```text
app:layout_constraintHorizontal_chainStyle=""

可选值: spread,spread_inside,packed
```
该属性产生的效果类似于css中的`justify-content`，因此不多做解释。

值得注意的一点是，只有在组件与组件相互依赖时才能够使用该布局，否则将无效。如果组件的`width`属性设置为0dp，那么能保证所有控件都能均分空间，即使其内部文本庞大，也不会影响所占宽度，我们也可以为特定几个组件设置`wrap_content`这样这些组件就能够自由伸展，但其他0dp的组件将会被压缩空间

组件间头尾链接需要用到
```
app:layout_constraintStart_toEndOf=""
app:layout_constraintEnd_toStartOf=""
```


#### 附属组件
###### Guideline 参考线
这挺好理解的，我们可以设置参考线，并将组件的某些点绑定至参考线上，方便我们设计页面，在实际运行时，参考线会被隐藏。
```text
常用属性：
orientation: 排列方式 
app:layout_constraintGuide_end: 位于参考线末尾
app:layout_constraintGuide_percent: 位于参考线的百分比位置

```
###### Barrier 