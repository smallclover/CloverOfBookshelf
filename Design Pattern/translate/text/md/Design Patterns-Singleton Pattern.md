> [原文链接][1]

> 译者：[smallclover][2]

>个人翻译，水平有限，如有错误欢迎指出，谢谢！


## 设计模式-单例模式##

单例模式是Java中最简单的设计模式之一。这种类型的设计模式，是创建型模式下创建对象的最好方式之一。
这个模式涉及到一个单独的类，它负责创建一个对象，并且同时确保只有唯一的一个对象能被创建。这个类提供唯一的方法直接访问这个对象而无需实例化对象。

### 实现###


我们创建一个SingleObject类。SingeObject类有一个私有的构造器和一个它自身的静态实例对象。
SingleObject类提供一个静态的方法，外部可以是使用它来获得SingleObject的静态实例。SingletonPatternDemo, 我们的demo类将通过SingleObject类来获得SingleObject 对象。

 ![image](/Design Pattern/translate/image/Singleton Pattern.png)

#### 第一步####

创建一个Singleton 类。

**SingleObject.java**
```java
public class SingleObject {

   //创建SingleObject的对象
   private static SingleObject instance = new SingleObject();

   //使构造函数私有，外界将无法实例化该类
   private SingleObject(){}

   //获得唯一可用的对象
   public static SingleObject getInstance(){
      return instance;
   }

   public void showMessage(){
      System.out.println("Hello World!");
   }
}
```
#### 第二步####

从单例类获得唯一的对象。

**SingletonPatternDemo.java**
```java
public class SingletonPatternDemo {
   public static void main(String[] args) {

      //非法构造
      //编译错误，构造函数SingleObject()不可见。
      //SingleObject object = new SingleObject();

      //获得唯一可用对象
      SingleObject object = SingleObject.getInstance();

      //展示信息
      object.showMessage();
   }
}
```
#### 第三步####
校验输出。
```java
Hello World!
```

  [1]: http://www.tutorialspoint.com/design_pattern/singleton_pattern.htm
  [2]: http://www.smallclover.com
