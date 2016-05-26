> [原文链接][1]

> 译者：[smallclover][2]

>个人翻译，水平有限，如有错误欢迎指出，谢谢！

# 设计模式-原型模式#

原型模式是指创建对象的副本，同时保持性能。这种类型的设计模式是创建型设计模式下创建对象最好的方式之一。

这个模式需要实现一个原型接口，并通知它创建一个当前对象的一个副本。这种模式在直接创建一个对象代价非常高昂的时候使用。例如，在执行代价较高的数据库操作后创建对象。我们可以缓存对象，在下次请求时返回该对象的一个副本，并更新数据库从而减少数据库的调用。

***译注***：
- 1.关于原型模式为何会提高性能？
- 2.关于Java的深拷贝和浅拷贝。

 引用来自脚本之家、CSDN博客
> [原型模式][3]
> [深拷贝与浅拷贝][4]


![clipboard.png](/Design Pattern/translate/image/Prototype Pattern.png)


## 实现##
我们将创建一个抽象的Shape类和继承这个抽象类的子类`Shape`。接下来声明一个类`ShapeCache`，该类把`Shape`对象在存储在`HashTable`中，当被请求时返回它们的副本。
`PrototypPatternDemo`，我们的`democlass`将使用`ShapeCache`类来获得`Shape`对象。


### 第一步###

创建一个抽象类`Shape`实现`Cloneable`接口。

**Shape.java**
```java
public abstract class Shape implements Cloneable {

   private String id;
   protected String type;

   abstract void draw();

   public String getType(){
      return type;
   }

   public String getId() {
      return id;
   }

   public void setId(String id) {
      this.id = id;
   }

   public Object clone() {
      Object clone = null;

      try {
         clone = super.clone();

      } catch (CloneNotSupportedException e) {
         e.printStackTrace();
      }

      return clone;
   }
}
```

### 第二步###

创建具体类继承`Shape`类。

**Rectangle.java**
```java
public class Rectangle extends Shape {

   public Rectangle(){
     type = "Rectangle";
   }

   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}
```
**Square.java**
```java
public class Square extends Shape {

   public Square(){
     type = "Square";
   }

   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}
```
**Circle.java**
```java
public class Circle extends Shape {

   public Circle(){
     type = "Circle";
   }

   @Override
   public void draw() {
      System.out.println("Inside Circle::draw() method.");
   }
}
```

### 第三步###

创建一个类从数据库中得到具体类，并且把它们存储在一个`HashTable`中。

**ShapeCache.java**
```java
import java.util.Hashtable;

public class ShapeCache {

   private static Hashtable<String, Shape> shapeMap  = new Hashtable<String, Shape>();

   public static Shape getShape(String shapeId) {
      Shape cachedShape = shapeMap.get(shapeId);
      return (Shape) cachedShape.clone();
   }

   // for each shape run database query and create shape
   // shapeMap.put(shapeKey, shape);
   // for example, we are adding three shapes

   public static void loadCache() {
      Circle circle = new Circle();
      circle.setId("1");
      shapeMap.put(circle.getId(),circle);

      Square square = new Square();
      square.setId("2");
      shapeMap.put(square.getId(),square);

      Rectangle rectangle = new Rectangle();
      rectangle.setId("3");
      shapeMap.put(rectangle.getId(), rectangle);
   }
}
```

### 第四步###

PrototypePatternDemo 使用 `ShapeCache` 类从HashTable中获得诸多图形的克隆副本。
**PrototypePatternDemo.java**
```java
public class PrototypePatternDemo {
   public static void main(String[] args) {
      ShapeCache.loadCache();

      Shape clonedShape = (Shape) ShapeCache.getShape("1");
      System.out.println("Shape : " + clonedShape.getType());		

      Shape clonedShape2 = (Shape) ShapeCache.getShape("2");
      System.out.println("Shape : " + clonedShape2.getType());		

      Shape clonedShape3 = (Shape) ShapeCache.getShape("3");
      System.out.println("Shape : " + clonedShape3.getType());		
   }
}
```

### 第五步###

校验输出
```java
Shape : Circle
Shape : Square
Shape : Rectangle
```

  [1]: http://www.tutorialspoint.com/design_pattern/prototype_pattern.htm
  [2]: http://www.smallclover.com
  [3]: http://blog.csdn.net/zhengzhb/article/details/7393528
  [4]: http://www.jb51.net/article/48201.htm
