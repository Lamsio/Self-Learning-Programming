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

#### router-link
当我们配置完基本的设定后，我们就可以设置切换了。

