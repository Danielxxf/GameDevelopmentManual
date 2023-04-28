# 游戏引擎（Game Engine）
游戏引擎是一种软件开发工具，用于快速创建和开发游戏。它是一种包括多种功能和工具的开发平台，可以被游戏开发者用来构建游戏中的不同元素，例如图形渲染、物理引擎、音频处理、动画与动态效果、人工智能等方面。
## 虚幻4（Unreal Engine）
## Unity Engine
### 生命周期函数

有些人问继承MonoBehaviour的类，都可以自动调用Start、Update方法，那可以将其写成虚方法吗?这样派生类都可以进行重载实现？

答：其实我们查看MonoBehaviour类的定义，发现MonoBehaviour 中看不到这些函数，派生类也并没有特别的override或者new关键字，也不能base.Start()，所以Start、Update 方法并不属于 MonoBehaviour 类。

那为什么派生类只要写了这些函数，都可以自动调用呢。

答：我们知道Unity大致上分为两个部分，大部分核心逻辑使用Cpp开发，之后包装一层C#，把C#接口开放给开发者。
在 Runtime时候，引擎CPP部分会去检测继承MonoBehaviour的类，如果发现有实现这些函数则会注册进列表，后面游戏中引擎仅仅需要简单地遍历列表，执行这些方法就行。这样调用，和正常函数调用性能差不多，绕过了虚拟机内部一大堆的处理

这样实现的优点：
1、内存。空函数也是占内存的，不是所有派生的MonoBehaviour都需要实现，只是按需实现。如果MonoBehivour作为基类声明了所有的Start、Update这种空函数，那么每个对象都都会有一大量的空函数，这就很浪费了。
2、性能。Unity主循环会遍历所有的MonoBehaviour，调用空的函数，虽然函数为空，但是call的时候也是会有消耗的。

所以Unity做了一件事，在cpp层实现了个类似C# 反射的机制，其实就是直接去找Start、Update的函数指针。如果这个MonoBehaviour有实现Start，那么就调，没那么就不调。MonoBehaviour自身就干干净净的不包含这些函数的定义。让用户自己按需声明。
————————————————
版权声明：本文为CSDN博主「神游天外」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/wjxxaut/article/details/107982560

https://www.zhihu.com/question/388043251

### 
## Cocos 2d-x