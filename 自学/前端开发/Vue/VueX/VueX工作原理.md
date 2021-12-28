#### 原理图
![Vue工作原理图](https://vuex.vuejs.org/vuex.png)
[尚硅谷Vue2.0+Vue3.0全套教程丨vuejs从入门到精通_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Zy4y1K7SH?p=107)

当我们有两个组件想互相通信时，我们需要给双方都设置对方的`$emit`和`$on`才能确保双方能够互相接收对方的数据。但这种方式并不理想，倘若我们有一千个组件，这就意味着每个组件内要写999个`$emit`和`$on`方法，很显然这不可能！

此外，如果我们想用`全局代理通信`的方式实现该功能，这对于`$bus`而言压力巨大，因此也不是一个好的选择。

于是变诞生了VueX插件，他的思想是将各组件公用的东西抽出到独立的VueX空间中，这类似于远程仓库的概念。

#### 组成介绍
VueX本质上由三个部分组成，分别是**Actions**,**Mutations**和**State**.

1. Actions - 负责管理接收到的行为
2. Mutations - 负责处理公共数据
3. State - 负责存储公共数据

执行流程是，当Vue组件想更改公共数据时，会调用`this.$store.dispatch([动作名],[数据])`，该请求会告知**Actions**，**Actions**会调用`commit([动作名],[数据])`方法将请求转给**Mutations**进行处理，**Mutations**在接收到请求后会处理指定数据并将最终值存储在**State**中

```js
//引入VueX  
import Vuex from "vuex";  
import Vue from "vue";  
  
Vue.use(Vuex);  
// 用于响应组件内的动作  
const actions = {  
    plus(context,value){  
        context.commit('PLUS',value)  
    }  
}  
// 用于操作数据  
const mutations = {  
    PLUS(state,value){  
        state.sum += value;  
	}  
}  
// 用于响应组件内的动作  
const state = {  
    sum : 0,  
}  
  
export default new Vuex.Store({  
    actions,  
	mutations,  
	state  
})
```