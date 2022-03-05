## 相关API
不同的API性能也不同，因此还得视乎使用场景做出决定，以下是几个常见的API

1. GameObject.Find()
2. Transform.Find()
3. GameObject.FindWithTag()
4. GameObject.FindGameObjectsWithTag
5. Resources.FindObjectsOfTypeAll()

#### GameObject.Find()
通过名字/路径查找游戏对象

```csharp
GameObject.Find("GameObjectName");
GameObject.Find("ParentObject/ChildObject");
```

###### 注意事项
1. 无法找到隐藏对象

隐藏对象包括查找路径的任何一个父节点隐藏(active=false)

2. 如果查找不在最上层，建议合理使用路径查找，路径查找是一把双刃剑
	- 解决查找中可能出现的重名问题
	- 如果有完整路径，可以减少查找范围以及时间
	- 路径或结构调整后，影响查找
3. 如果路径查找中的一个父节点`active=false`，这个对象都将查找不到
4. 方便但效率低下（递归遍历，因此性能堪忧，切勿频繁调用）

#### Transform.Find()
可以查找隐藏对象但前提是其所在的根节点必须可见`active=true`，支持路径查找

```csharp
GameObject root = GameObject.Find("root");
root.setActive(false); //根节点为空

// 查找失败
root.transform.Find("root/ChildNode")
```

#### GameObject.FindWithTag()
针对指定Tag寻找

```csharp
// Enemy1,2,3分别设置了Enemy标签

private GameObject[] eArr;
void Start()
{
    eArr = GameObject.FindGameObjectsWithTag("Enemy");
    Debug.Log(eArr.Length); //3
}
```


#### 性能对比
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8zOTU5NDMzLTIwODQwMTM5NTg3MzRmZTAucG5n?x-oss-process=image/format,png)

## 总结
当 GameObject.Find(string name) 满足查询条件时,即可确保其能查到目标物体时候,应该推荐使用该方式,不推荐使用不是因为查找效率不高,而是查找限制大,没有Transform.Find(string path)能确保查到目标.  
还有部分开发者说查找时候要提供完整的路径比根据名字便利查找效率更高,但是上述测试结果与此结论天壤之别,可能的原因是Unity并没有为每一个GameObject物体存储完整的索引,激活的物体应该是直接存储名字提供查找,所以提供完整的路径查找对于GameObject.Find这种方式不推荐使用!!!通过完整路径查找应该使用Transform.Find(string path)查找,虽然它的效率在以上几种查找方式里看起来不是最高的,但是它查找受到的限制较小,例如不用担心在游戏逻辑中隐藏了物体而导致使用GameObject.Find查找不到的问题

所以说要做到性能最佳的查找应该将GameObject.Find(string name)和Transform.Find(string path)和Transform.GetChild(int index) 和GameObject.FindGameObjectWithTag(string tag)几种方式根据需求相结合

1.当GameObject.Find(string name) 查找条件不受限制时,用GameObject.Find  
2.当查找数量不多,且需要包含隐藏物体时,各子物体索引位置可能会发生变化时,用Transform.Find(string path)  
3.当查找数量不多,且需要包含隐藏物体时,各子物体索引能确保不变时,Transform.GetChild(int index) 效率更高  
4.当路径过长过深时,且目标物体数量较多成组时,可以为其设置Tag然后FindGameObjectsWithTag查找