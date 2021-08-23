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
我们可以通过为组件添加`app:layout_constraintHorizontal_bias=""`属性，设置组件的偏移量，一般情况下，如果设置为0，则向左贴齐，但有些特殊情况可能有偏差，例如组件本身占据整个宽度，亦或者焦点重叠，都会使bias与yu'qi'bu'f