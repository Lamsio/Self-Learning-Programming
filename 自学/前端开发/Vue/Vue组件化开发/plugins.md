#### 插件
· 功能：用于增强Vue
· 本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据

#### 定义插件
```js
// plugins.js
// 为了美观，建议不要直接定义在main.js中
export default {
	install(Vue,x,y,z){//后面可以跟一大堆参数
		//定义全局过滤器
		Vue.filter('fill',function(value){
			return value*10;
		});

		//定义全局指令
		Vue.directive('fbind',{
			//...
		});

		//定义混入mixin
		Vue.mixin({
			data(){
				glo_position_x = 0;
				glo_position_y = 0;
			}
		});

		//为Vue原型添加方法(vm/vc都能使用)
		Vue.prototype.hello = ()=>{alert('你好啊')}
	}
}
```


#### 使用插件
使用者只需要在`main.js`中使用`Vue.use(plugin_name,[参数])`就能够调用插件
