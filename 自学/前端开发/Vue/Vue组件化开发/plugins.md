#### 插件
· 功能：用于增强Vue
· 本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据

#### 定义插件
```js
// plugins.js
// 为了美观，建议不要直接定义在main.js中
export default {
	install(Vue){
		//定义全局过滤器
		Vue.filter('fill',function(value){
			return value*10;
		});

		//定义全局指令
		Vue.directive('fbind',{
			//...
		});

		//定义
	}
}
```