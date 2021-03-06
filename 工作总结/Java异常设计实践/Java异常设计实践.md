# Java 异常 设计实践

> 说是实践，更多的是对项目中异常体系设计的问题总结，不过，不同的项目异常的具体设计肯定是有所区别的。

## Java异常体系

下图是一张Java异常体系的缩略图，说是缩略图，实际上已经把所有可能的异常的父类列举了出来（这里我也稍微列举了一些较为常见的异常）：

![异常体系](java_exception.png)

`Throwable` 所有异常的父类（或者说是超类），就如同`Object` 是所有对象的父类。然后，`Throwable` 又有两个唯一的子类，`Exception`和`Error` ，对于`Error`这个异常，在一般的业务设计过程中是不涉及的，正如同上面图片列出的其中两个字类，`OutOfMemoryError`即我们常说的OOM和`NoClassDefFoundError`，`NoClassDefFoundError`这个错误经常出现在编译没有完全，多数情况下是IDE缓存造成的问题，此时只要清理一下缓存然后再重新编译一下，多数情况就会此问题消失。而OOM常见的情况是内存异常，通过调查JVM的快照（Dump）查看哪个类或者方法占用了大量的空间，应该很快也就明白内存溢出的原因。

很显然，上面说的张两种情况我们不该去试图捕获他们，Error及其子类更准确的说是**错误**而不是**异常**。

2020年12月5日20点34分

