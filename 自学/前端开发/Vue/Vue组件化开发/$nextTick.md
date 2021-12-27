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

上面这段代码的意思是