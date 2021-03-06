#### Mixin
我们有两个组件并且都拥有以下的方法
```javascript
methods: {
	showName(){
		console.log(this);
	}
}
```

如果俩组件都拥有相同的东西，那么我们可以采用mixin去简化结构，具体流程如下

```javascript
// mixin.js 单独开一个mixin.js文件用于存储相同项，并暴露出去
export const mixin = {
	methods: {
		showName(){
			console.log(this);
		}
	}
}
```

在抽取相同项后，我们可以在两个组件中导入这个`mixin.js`。

```html
import {mixin} from '../mixin'

export default {
	name: 'School',
	data(){
		return {
			name: 'MPI',
			address: 'Macau'
		}
	},
	mixins: [mixin] //将混合项放入数组即可。
}
```