事件的发送和接收可以在项目中的任何地方

这里我使用字符串作为一个事件对象,当然你创建一个任意对象或者使用`Int`都可以

=== "发送事件"
    ```kotlin
    sendEvent("发送事件给当前")
    ```

=== "接收事件"
    ```kotlin
    receiveEvent<String>() {
        tv_event.text = it
    }
    ```

<br>

!!! note
    只要`sendEvent`的参数类型和`receiveEvent`的泛型类型匹配即可成功收发事件, 可以是任何对象(包括布尔类型或者字符串)

## 标签
有时候事件类型可能出现重叠或者叫复用, 我们可以通过加标签来区分事件

创建一个对象作为事件
```kotlin
data class MyEvent(val name:String, val age:Int)
```

=== "发送事件"
    ```kotlin
    sendEvent(MyEvent("吴彦祖", 24), "sexy_man_tag")
    ```

=== "接收事件"
    ```kotlin
    receiveEvent<MyEvent>("sexy_man_tag") {
        tv_event.text = it.name // it 即为MyEvent对象
    }
    ```


- 接受者传入的标签可以是多个, 但是发送了标签就一定要和接受者匹配至少一个标签, 否则无法成功接收到事件
- 标签命名建议遵守规范, 例如`refresh_tag`, 全部有个后缀`_tag`, 方便你到时候全局搜索标签来定位事件