#### VueRouter
当我们想实现切换组件的功能时，我们可以使用VueRouter，该功能极其常见，例如页面的选项卡就是用VueRouter实现的。

#### 安装
1. 控制台: `npm i vue-router`
2. 项目的`main.js`文件中导入并`Vue.use(VueRouter)`使用该插件
![[Pasted image 20211228174051.png]]
3. 在`src`目录下创建`router`文件夹，并在其下面创建`index.js`配置文件
```js
import VueRouter from "vue-router";  
import About from "@/components/About";  
import Home from "@/components/Home";  
  
export default new VueRouter({  
    routes: [  
        {  
            path: '/',  
			component: Home  
		},  
		{  
            path: '/about',  
			component: About  
		}  
	]  
});
```

#### router-link & router-view
当我们配置完基本的设定后，我们就可以设置切换了。

```js
//App.vue
<template>  
    <div id="app">  
	 <router-link to="/about">关于</router-link>  
	 <router-link to="/home">主页</router-link>  
	 <router-view></router-view> 
	</div>
</template>
```

当运行时，`router-link`标签会被渲染成`a`标签，其中的`to`属性指明了要切换的组件的`path`，而`router-view`标签则是用于显示该组件。如果你想点击标签后高亮，你可以为`router-link`标签添加`active-class`属性，该标签用于决定被选择时的样式。

###### 注意
当我们点击`关于`时，就会展示About组件，此时，原本的Home组件就被会销毁！


#### 路由组件与一般组件
需要通过VueRouter调用的组件被称为路由组件，而一般组件则是不依赖路由就能展示的组件。按照官方的要求，路由组件建议放置在`src->pages`文件夹下，而一般组件就放在`src->components`文件夹下。