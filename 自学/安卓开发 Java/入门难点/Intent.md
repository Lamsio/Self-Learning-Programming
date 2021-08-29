#### 四大重点
1. ACTION
2. CATEGORY
3. DATA
4. EXTRAS

#### ACTION
Action:Action属性的值是一个字符串，它代表了系统中定义的一系列常用动作。通过setAction()方法或在清单文件AndroidMainfest.xml中设置。默认为：DEFAULT。
```text
ACTION_MAIN：Android Application的入口，每个android应用必须且只能包含一个此类型的Action声 明。   
ACTION_VIEW：系统根据不同的Data类型，通过已注册的对应Application显示数据。  
ACTION_EDIT：系统根据不同的Data类型，通过已注册的对应Application编辑示数据。   
ACTION_DIAL：打开系统默认的拨号程序，如果Data中设置了电话号码，则自动在拨号程序中输入此号码。   
ACTION_CALL：直接呼叫Data中所带的号码。   
ACTION_ANSWER：接听来电。   
ACTION_SEND：由用户指定发送方式进行数据发送操作。  
ACTION_SENDTO：系统根据不同的Data类型，通过已注册的对应Application进行数据发送操作。   
ACTION_BOOT_COMPLETED：Android系统在启动完毕后发出带有此Action的广播（Broadcast）。   
ACTION_TIME_CHANGED：Android系统的时间发生改变后发出带有此Action的广播（Broadcast）。   
ACTION_PACKAGE_ADDED：Android系统安装了新的Application之后发出带有此Action的广播（Broadcast）。   
ACTION_PACKAGE_CHANGED：Android系统中已存在的Application发生改变之后（如应用更新操作）发出带有此Action的广播（Broadcast）。   
ACTION_PACKAGE_REMOVED：卸载了Android系统已存在的Application之后发出带有此Action的广播（Broadcast）。
```
#### DATA
Data: DATA通常是URL格式定义的操作数据。列如:tel//。通过setData()方法设置。
#### CATEGORY
Category：Category属性用于指定当前动作(Action)被执行的环境。通过addCategory()方法或在清单文件 AndroidMainfest.xml中设置.默认为:CATEGORY_DEFAULT。
```text
 CATEGORY_DEFAULT：Android系统中默认的执行方式，按照普通Activity的执行方式执行。   
 CATEGORY_HOME：设置该组件为Home Activity。  
 CATEGORY_PREFERENCE：设置该组件为Preference。   
 CATEGORY_LAUNCHER：设置该组件为在当前应用程序启动器中优先级最高的Activity，通常为入口ACTION_MAIN配合使用。   
 CATEGORY_BROWSABLE：设置该组件可以使用浏览器启动。   
 CATEGORY_GADGET：设置该组件可以内嵌到另外的Activity中。
```
#### EXTRAS
Extras：主要用于传递目标组件所需要的额外数据。通过putExtras()方法设置.
```text

