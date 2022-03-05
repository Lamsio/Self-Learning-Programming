## Input
Input主要是处理外部输入的一个类，例如键盘输入或者鼠标等方式...

常用的方法有:
1. GetKey()
2. GetKeyDown()
3. GetKeyUp()
4. GetMouseButton()
5. GetMouseButtonDown()
6. GetMouseButtonUp()

值得注意的是，以上方法都会返回bool类型

`GetKey()`和`GetMouse()`的触发条件是长按，其余的则是单点。

因此，倘若你想做组合键，请务必先使用`GetKey/Mouse`然后再使用单点触发。

```csharp
    // Update is called once per frame
private void Update()
{
    if (Input.GetKey(KeyCode.A) && Input.GetKeyDown(KeyCode.S))
    {
        Debug.Log("trigger");
    }
}
```