> [原文链接][1]

> 译者：[smallclover][2]

> 希望对大家有所帮助！Thanks for your watching

# 门面模式#

门面模式隐藏系统的复杂性同时会提供一个接口给用户，使得用户可以使用该系统。这种类型的设计模式属于结构型模式的一种，它将会添加一个接口到现有的系统当中，用户通过该接口使用系统，从而隐藏了系统的复杂性。
该模式涉及一个单独的类，该类会向客户提供简单的方法并且代替用户去调用那些在系统中存在的类的方法。这样用户就不会接触到系统是如何实现的，从而隐藏了系统的复杂性。

实现


我们将创建一个Shape接口，并且创建具体的类实现它。接下来我们需要声明一个门面类ShapeMaker。
ShapeMaker类代替用户去调用这些具体的类。FacadePatternDemo，我们的demo类将通过使用ShapeMaker类来展示这些结果。

![image](/Design Pattern/translate/image/Facade Pattern.png)

## 第一步##

创建一个接口。

**Shape.java**
```java
public interface Shape {
   void draw();
}
```
## 第二步##

创建具体的类实现Shape接口。

**Rectangle.java**
```java
public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Rectangle::draw()");
   }
}
```
**Square.java**
```java
public class Square implements Shape {

   @Override
   public void draw() {
      System.out.println("Square::draw()");
   }
}
```
**Circle.java**
```java
    public class Circle implements Shape {

       @Override
       public void draw() {
          System.out.println("Circle::draw()");
       }
    }
```
## 第三步##

创建一个门面类。

**ShapeMaker.java**
```java
public class ShapeMaker {
   private Shape circle;
   private Shape rectangle;
   private Shape square;

   public ShapeMaker() {
      circle = new Circle();
      rectangle = new Rectangle();
      square = new Square();
   }

   public void drawCircle(){
      circle.draw();
   }
   public void drawRectangle(){
      rectangle.draw();
   }
   public void drawSquare(){
      square.draw();
   }
}
```

## 第四步##

使用门面类画各种各样的图形。

**FacadePatternDemo.java**
```java
public class FacadePatternDemo {
   public static void main(String[] args) {
      ShapeMaker shapeMaker = new ShapeMaker();

      shapeMaker.drawCircle();
      shapeMaker.drawRectangle();
      shapeMaker.drawSquare();		
   }
}
```
## 第五步

校验输出
```java
Circle::draw()
Rectangle::draw()
Square::draw()
```

  [1]: http://www.tutorialspoint.com/design_pattern/facade_pattern.htm
  [2]: http://www.smallclover.com
