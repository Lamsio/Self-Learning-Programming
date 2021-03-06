#### XML
###### Outline
1. XML数据模型
2. 树结构
3. 模型关系

#### XML与G2S
XML是一款标记性语言，主要用途用于传输和存储数据，与HTML相比，HTML则是负责显示数据，XML并不会有任何展示性效果，纯粹被设计用来结构化、存储及传输信息，在XML中可以创建任意标签。

G2S(Game-to-System)是基于网络的协议，用于Slot machines与Slot information system之间的通讯，而其是依赖于XML实现的。

在XML中，其语法与HTML相似，必须拥有根节点，即类似于如下代码:
```xml
<book>
	<title>咸鱼是怎样练成的</title>
	<author>TOMMY</author>
</book>	
```
`<book></book>`标签即是根节点。

#### XML属性
XML属性类似于HTML属性 `<book total="28535"></book>`

XML属性与元素其实相似，选择取决于开发人员及规范
```xml
<person sex="female">  
<firstname>Anna</firstname>  
<lastname>Smith</lastname>  
</person>
```

```xml
<person>  
<sex>female</sex>  
<firstname>Anna</firstname>  
<lastname>Smith</lastname>  
</person>
```

以上两种皆可
#### 命名空间
在开发时，往往会几个人同时进行开发，因此我们需要保证标签名称不重复，我们可以采用命名空间的方式避免命名冲突。

```xml
<table xmlns="http://www.w3.org/TR/html4/">  
	<tr>  
		<td>Apples</td>  
		<td>Bananas</td>  
	</tr>  
</table>

```
我们只需要为根节点添加`xmlns`属性即可声明命名空间，上述代码将不会与HTML的`<table>`冲突。

#### 转义
当我们想在XML中输入纯字符<>等特殊意义字符，可以使用
```xml
   

<p>

<![CDATA[

 You can enter any characters (e.g. "<" and '>') within a CDATA section. Only the ending symbol has special meaning.

 ]]>

</p>
```


#### 笔者小想法
看完Runoob关于XML的介绍后，感觉XML类似于标签化的json数据。。。