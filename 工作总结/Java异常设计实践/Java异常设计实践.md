# Java 异常 设计实践

> 说是实践，更多的是对项目中异常体系设计的问题总结，不过，不同的项目异常的具体设计肯定是有所区别的。

## Java异常体系

下图是一张Java异常体系的缩略图，说是缩略图，实际上已经把所有可能的异常的父类列举了出来：

![异常体系](C:\Users\drago\Desktop\java_exception.png)

`Throwable` 所有异常的父类（或者说是超类），就如同`Object` 是所有对象的父类。然后，`Throwable` 又有两个唯一的子类，`Exception`和`Error` 