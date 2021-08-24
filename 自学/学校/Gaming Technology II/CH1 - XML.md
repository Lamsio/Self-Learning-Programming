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
XML属性类似于HTML属性，