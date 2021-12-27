这是一个十分好用的周期类小工具，假设我们想实现“点击文本可以编辑”的效果时，我们可能需要以下的代码实现

```js
methods: {  
  clickText(index){  
      this.dataArr[index].isEdit=true;  
	  this.$nextTick(function () {  
	      this.$refs.inputTitle[index].focus()  
      })  
  }  
}
```

上面这段代码的意思是，当我们点击本文时，触发`clickText`方法，`isEdit`变量是用于判断是否进入编辑模式的，如果为`true`则隐藏`p`标签显示`input`标签，下面有一段

```js
	  this.$nextTick(function () {  
	      this.$refs.inputTitle[index].focus()  
      })  
```

这段代码的执行涉及到了先后顺序，在`$nextTick()`函数中的代码将会被延后到页面渲染完成时执行，由于在渲染前无法获取指定`input`的焦点，如果我们不这样设置，`this.$refs.inputTitle[index].focus()`将会无法生效（因为还没渲染，怎么执行？）