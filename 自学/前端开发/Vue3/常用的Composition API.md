#### Setup
1. 理解: Vue3.0中的新配置项，值为一个函数
2. setup是所有Composition API的展示舞台
3. 组件中所用到的: 数值、方法等属性都要放置在setup中
4. 注意点
	1. Vue3同时支持Vue2的数据写法和Vue3的数据写法，但不要混用，Vue2写法可以访问Vue3的数据，但是setup无法访问Vue2的配置
	2. 如果重名，setup优先
	3. setup不能是一个async函数，因为返回值不再是return的对象，而是promise，模板看不到return对象中的属性值

```js
export default {  
  name: 'App',  
  // 仅测试setup，不考虑响应式  
  setup(){  
     let name="Tommy"  
     let age = 18  
  
	 function hello() {  
	      alert(`我是${name},我今年${age}岁`)  
	 }  
  
     return {  
	      name,  
		  age,  
		  hello  
	 }  
  }  
}
```