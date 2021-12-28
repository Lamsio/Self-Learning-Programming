#### 原理图
![Vue工作原理图](https://vuex.vuejs.org/vuex.png)
[尚硅谷Vue2.0+Vue3.0全套教程丨vuejs从入门到精通_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Zy4y1K7SH?p=107)

当我们有两个组件想互相通信时，我们需要给双方都设置对方的`$emit`和`$on`才能确保双方能够互相接收对方的数据。但这种方式并不理想，倘若我们有一千个组件，这就意味着每个组件内要写999个`$emit`和`$on`方法，很显然这不可能！

此外，如果我们想用`全局代理通信`的方式实现该功能，这对于`$bus`而言压力巨大。