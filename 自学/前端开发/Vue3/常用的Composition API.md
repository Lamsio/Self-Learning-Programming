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
  // Vue3的写法
  setup(){  
     let name="Tommy"  
     let age = 18  
  
	 function hello() {  
		  age = 20;
	      alert(`我是${name},我今年${age}岁`);
	 }  
  
     return {  
	      name,  
		  age,  
		  hello  
	 }  
  },
  // Vue2的写法
  data(){
	return {
		numb: 100
	}
  }
}
```

#### Ref
如果我们运行上述代码会发现一个很奇怪的事情，当我们点击按钮触发`hello()`时，输出的年龄依旧是18，在Vue3中我们需要手动地将属性套用`ref`类型，也就是说每个属性都得改成`ref(属性)`

我们更改上述代码得到以下代码：
```js
import {ref} from "vue";
export default {  
  name: 'App',  
  // 仅测试setup，不考虑响应式  
  // Vue3的写法
  setup(){  
     let name= ref("Tommy")  
     let age = ref(18)  
  
	 function hello() {  
		  age.value = 20;
	      alert(`我是${name},我今年${age}岁`);
	 }  
  
     return {  
	      name,  
		  age,  
		  hello  
	 }  
  },
}
```

此外，在函数中若要修改值，也必须是`[属性名].value`才能修改。

#### Reactive
Ref用于将常规数据类型（String，number...）响应化，而Reactive则是用于将对象、数组类型响应化。

一种模拟Vue2 data的写法
```js
export default {  
  name: 'App',  
  // 仅测试setup，不考虑响应式  
  setup(){  
    let data = reactive({  
        name: 'LKK',  
		age: 18  
  })  
    function hello() {  
      data.name = 'ZHQ';  
	  data.age = 17;  
  }  
    return {  
      data,  
	  hello  
	 }  
  },  
}
```

基于这种方式，我们可以用`data.[数据名]`实现数据调用

#### Computed
在Vue2中我们是通过以下方法实现`computed`的
```js
import Main from './components/Main.vue'  
  
export default {  
  name: 'App',  
  components: {  
    Main  
  },  
  computed: {  
      
  }  
}
```

但在Vue3中，我们需要在`setup()`下调用`computed()`实现计算属性。
```js
import {computed, ref} from "vue";  
export default {  
  name: 'App',  
  // 仅测试setup，不考虑响应式  
  setup(){  
     let data=ref("");  
  let fulldata = computed(()=>{  
      return data.value+"才是数据";  
  })  
     return {  
       data,  
	   fulldata  
     }  
  },  
}
```

还有个特点是，在Vue3中，计算属性不再是只读，还可以主动更改值。

```js
let fulldata = computed({
	get(){
		return data.value+"才是数据";
	},
	set(value){
		data.value = value;
	}
})
```