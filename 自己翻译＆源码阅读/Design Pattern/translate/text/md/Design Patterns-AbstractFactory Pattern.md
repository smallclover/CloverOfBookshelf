> [原文链接][1]
> 译者：[smallclover][2]
>个人翻译，水平有限，如有错误欢迎指出，谢谢！

## 设计模式-抽象工厂模式##

抽象工厂的核心是一个超级工厂，而这个工厂能创建其他的工厂。所以，这个超级工厂也被叫做工厂的工厂。这种类型的设计模式是创建型模式下生成对象的最好的方式之一。
在抽象工厂模式中，一个接口负责创建（抽象）与一个工厂相关的对象，不需要显示的指定它们的类。每一个被生成的工厂能按照工厂模式生产对象。



### 实现###

我们将创建`Shape`和`Color` 接口以及实现它们的具体类。接下来我们将会创建一个抽象的工厂类`AbstractFactory`。定义工厂类`ShapeFactory`和`ColorFactory`，并且继承`AbstractFactory`类。然后，创建`FactoryProducer`工厂生产者类。
`AbstractFactoryPatternDemo`，我们的`demo`类通过`FactoryProducer`来获得一个`AbstractFactory` 对象。`Demo`类通过将图形信息（圆/矩形/正方形）传递到`AbstractFactory`来获得它所需要的类型的对象。同时也可以传递颜色信息（红色/绿色/蓝色）到`AbstractFactory`来获得`demo`类所需要的类型的对象。

![image](/Design Pattern/translate/image/AbstractFactory Pattern.png)


### 第一步###

创建一个图形接口
**Shape.java**
```java
public interface Shape {
   void draw();
}
```
### 第二步###

创建实现相同接口的具体类（Shape interface）

**Rectangle.java**
```java
public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}
```
**Square.java**
```java
public class Square implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}
```
**Circle.java**
```java
public class Circle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Circle::draw() method.");
   }
}
```

### 第三步###

创建一个颜色接口。

**Color.java**
```java
public interface Color {
   void fill();
}
```
### 第四步###

创建实现相同接口的具体类（Color interface）

**Red.java**
```java
public class Red implements Color {

   @Override
   public void fill() {
      System.out.println("Inside Red::fill() method.");
   }
}
```
**Green.java**
```java
public class Green implements Color {

   @Override
   public void fill() {
      System.out.println("Inside Green::fill() method.");
   }
}
```
**Blue.java**
```java
public class Blue implements Color {

   @Override
   public void fill() {
      System.out.println("Inside Blue::fill() method.");
   }
}
```
### 第五步###
创建一个抽象类来获取与工厂相对应的Color和Shape对象。

**AbstractFactory.java**
```java
public abstract class AbstractFactory {
   abstract Color getColor(String color);
   abstract Shape getShape(String shape) ;
}
```
**第六步**


创建多个继承AbstractFactory的工厂类根据传送的信息生成具体类的对象。

**ShapeFactory.java**
```java
public class ShapeFactory extends AbstractFactory {

   @Override
   public Shape getShape(String shapeType){

      if(shapeType == null){
         return null;
      }		

      if(shapeType.equalsIgnoreCase("CIRCLE")){
         return new Circle();

      }else if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();

      }else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }

      return null;
   }

   @Override
   Color getColor(String color) {
      return null;
   }
}
```
**ColorFactory.java**
```java
public class ColorFactory extends AbstractFactory {

   @Override
   public Shape getShape(String shapeType){
      return null;
   }

   @Override
   Color getColor(String color) {

      if(color == null){
         return null;
      }		

      if(color.equalsIgnoreCase("RED")){
         return new Red();

      }else if(color.equalsIgnoreCase("GREEN")){
         return new Green();

      }else if(color.equalsIgnoreCase("BLUE")){
         return new Blue();
      }

      return null;
   }
}
```

### 第七步###

创建一个工厂生成器通过传递的Shape和Color这样的信息来生成工厂。

**FactoryProducer.java**
```java
public class FactoryProducer {
   public static AbstractFactory getFactory(String choice){

      if(choice.equalsIgnoreCase("SHAPE")){
         return new ShapeFactory();

      }else if(choice.equalsIgnoreCase("COLOR")){
         return new ColorFactory();
      }

      return null;
   }
}
```

### 第八步###

使用FactoryProducer来获得AbstractFactory，使它通过传递类型信息来获得具体类生产工厂。

**AbstractFactoryPatternDemo.java**
```java
public class AbstractFactoryPatternDemo {
   public static void main(String[] args) {

     //获得shape工厂
      AbstractFactory shapeFactory = FactoryProducer.getFactory("SHAPE");

      //获得一个circle对象
      Shape shape1 = shapeFactory.getShape("CIRCLE");

      //调用circle的draw方法
      shape1.draw();

       //获得一个rectangle对象
      Shape shape2 = shapeFactory.getShape("RECTANGLE");

       //调用rectangle的draw方法
      shape2.draw();


      Shape shape3 = shapeFactory.getShape("SQUARE");


      shape3.draw();

      //获得color factory
      AbstractFactory colorFactory = FactoryProducer.getFactory("COLOR");

      //获得red对象
      Color color1 = colorFactory.getColor("RED");

      //调用red的fill方法
      color1.fill();


      Color color2 = colorFactory.getColor("Green");


      color2.fill();


      Color color3 = colorFactory.getColor("BLUE");


      color3.fill();
   }
}
```
### 第九步###

校验输出。
```java
Inside Circle::draw() method.
Inside Rectangle::draw() method.
Inside Square::draw() method.
Inside Red::fill() method.
Inside Green::fill() method.
Inside Blue::fill() method.

```
  [1]: http://www.tutorialspoint.com/design_pattern/abstract_factory_pattern.htm
  [2]: http://www.smallclover.com
