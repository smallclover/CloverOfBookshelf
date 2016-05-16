>[原文链接][1]
> 译者：[smallclover][2]
>个人翻译，水平有限，如有错误欢迎指出，谢谢！

## 设计模式-工厂模式##

工厂模式是Java中最常用的设计模式之一。这种类型的设计模式属于创建型模式下，创建一个对象最好的方式之一。
在工厂模式中，我们不会把创建对象的逻辑暴露给客户端，同时通过使用通用接口来创建对象引用。


## 实现##


我们将创建一个`Shape`接口以及实现这个`Shape`接口的类。接下来一步，我们会定义一个工厂类`ShapeFactory`。
`FactoryPatternDemo`，我们的demo类将通过图形工厂来获得图形对象。通过传送信息（圆、矩形、正方形）到图形工厂来获得我们所需要的类型的对象。


![clipboard.png](/img/bVtN5s)


### 第一步##


创建一个接口
**Shape.java**
```java
public interface Shape {
   void draw();
}
```

### 第二步###


创建具体的实现类来实现相同的接口（`Shape` interface）。
**Rectangle.java**
```java
public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}
Square.java
public class Square implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}
Circle.java
public class Circle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Circle::draw() method.");
   }
}
```

###第三步###



创建一个工厂基于传送的信息生成具体类的对象。

**ShapeFactory.java**
```java
public class ShapeFactory {

   //使用getShape方法获得对应图形的对象
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      }		
      if(shapeType.equalsIgnoreCase("CIRCLE")){
         return new Circle();

      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();

      } else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }

      return null;
   }
}
```

### 第四步###



使用工厂通过传送过来的类型信息获得具体类的对象。

**FactoryPatternDemo.java**
```java
public class FactoryPatternDemo {

   public static void main(String[] args) {
      ShapeFactory shapeFactory = new ShapeFactory();

      //获得圆的一个对象并调用它的draw方法。
      Shape shape1 = shapeFactory.getShape("CIRCLE");

      //调用圆的draw方法
      shape1.draw();

      //获得矩形的一个对象并调用它的draw方法。
      Shape shape2 = shapeFactory.getShape("RECTANGLE");

      //调用矩形的draw方法
      shape2.draw();

      //获得正方形的一个对象并调用它的draw方法。
      Shape shape3 = shapeFactory.getShape("SQUARE");

      ////调用的draw方法
      shape3.draw();
   }
}
```

### 第五步###


校验输出。

```java

Inside Circle::draw() method.
Inside Rectangle::draw() method.
Inside Square::draw() method.
```

  [1]: http://www.tutorialspoint.com/design_pattern/factory_pattern.htm
  [2]: http://www.smallclover.com
