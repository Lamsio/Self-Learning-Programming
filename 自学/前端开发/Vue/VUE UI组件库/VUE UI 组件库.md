#### VUE UI 组件库
移动端:
1. [Vant - 轻量、可靠的移动端组件库 (youzan.github.io)](https://youzan.github.io/vant/#/zh-CN/)
2. [cube-ui Document (didi.github.io)](https://didi.github.io/cube-ui/#/zh-CN)
3. [Mint UI (mint-ui.github.io)](https://mint-ui.github.io/#!/zh-cn)

主机端:
1. [Element - 网站快速成型工具](https://element.eleme.io/#/zh-CN)
2. [NutUI - 移动端 Vue2、Vue3、小程序 组件库 (jd.com)](https://nutui.jd.com/#/)
3. [iView - A high quality UI Toolkit based on Vue.js (iviewui.com)](https://www.iviewui.com/)

#### 引入优化
由于上述几个常用的VueUI库，在官网内都有详细使用说明，因此不在此笔记内细说了。

以ElementUI为例，当我们在`main.js`中使用`Vue.use()`进行引用时，会将ElementUI中所有组件都引入进来，但实际上我们并不需要用到那么多组件，因此我们需要优化一下引入的组件。

我们可以借助 [babel-plugin-component](https://github.com/QingWei-Li/babel-plugin-component)，实现按需引入。

具体流程可以参考: [组件 | Element](https://element.eleme.cn/#/zh-CN/component/quickstart)

注意，其中的`.babeirc`已经变为了`babel.config.js`

```js
//以下是最新的babel.config.js配置
module.exports = {  
  presets: [  
    '@vue/cli-plugin-babel/preset',  
	["@babel/preset-env", { "modules": false }],  
  ],  
  "plugins": [  
    [  
      "component",  
	 {  
        "libraryName": "element-ui",  
		"styleLibraryName": "theme-chalk"  
	 }  
    ]  
  ]  
}
```