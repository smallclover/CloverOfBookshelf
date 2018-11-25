> [原文链接][1]

> 译者：[smallclover][2]

>个人翻译，因为英语水平的原因可能会词不达意，十分欢迎各位读者指出其中的错误，希望能对读者有1%的用处，谢谢！

# 设计模式-装饰器模式#

装饰器模式允许使用者将新功能添加到现有的对象而不需要改变它的数据结构。这种类型的设计模式来源于结构型模式，该设计模式将会去包装一个现有的类。
这种设计模式会常见一个装饰器类，它包装了原始类，并且在不改变原始类的方法的基础之上添加额外的新的功能。
我们将通过下面的例子来展示如何使用装饰器模式，在接下来的例子中我们将用颜色来装饰图形，但不需要修改图形的类。


## 实现##

我们将创建一个Shape接口和实现该接口的具体类。然后在创建一个抽象的`ShaperDecorator`类，该类也实现了`Shape`接口，并且持有一个`Shape`类的对象。
`RedShapeDecorator` 作为具体类实现了`ShapeDecorator`。`DecoratorPatternDemo`，作为我们的demo类将会去使用`RedShapeDecorator`去装饰`Shape`对象。

![clipboard.png](/Design Pattern/translate/image/Decorator Pattern.png)

### 第一步###

创建接口

**Shape.java**
```java
public interface Shape {
   void draw();
}
```

### 第二步###

创建具体的类来实现`Shape`接口

**Rectangle.java**
```java
public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Shape: Rectangle");
   }
}
```
**Circle.java**
```java
public class Circle implements Shape {

   @Override
   public void draw() {
      System.out.println("Shape: Circle");
   }
}
```
### 第三步###

创建抽象的装饰器类实现`Shape`接口。

**ShapeDecorator.java**
```java
public abstract class ShapeDecorator implements Shape {
   protected Shape decoratedShape;

   public ShapeDecorator(Shape decoratedShape){
      this.decoratedShape = decoratedShape;
   }

   public void draw(){
      decoratedShape.draw();
   }
}
```

### 第四步###

创建具体的装饰器类，该类继承了`ShaperDecorator`类。

**RedShapeDecorator.java**
```java
public class RedShapeDecorator extends ShapeDecorator {

   public RedShapeDecorator(Shape decoratedShape) {
      super(decoratedShape);		
   }

   @Override
   public void draw() {
      decoratedShape.draw();	       
      setRedBorder(decoratedShape);
   }

   private void setRedBorder(Shape decoratedShape){
      System.out.println("Border Color: Red");
   }
}
```

### 第五步###

使用`RedShapeDecorator`装饰`Shape`对象。

**DecoratorPatternDemo.java**
```java
public class DecoratorPatternDemo {
   public static void main(String[] args) {

      Shape circle = new Circle();

      Shape redCircle = new RedShapeDecorator(new Circle());

      Shape redRectangle = new RedShapeDecorator(new Rectangle());
      System.out.println("Circle with normal border");
      circle.draw();

      System.out.println("\nCircle of red border");
      redCircle.draw();

      System.out.println("\nRectangle of red border");
      redRectangle.draw();
   }
}
```
### 第六步###

检验输出
```java
Circle with normal border
Shape: Circle

Circle of red border
Shape: Circle
Border Color: Red

Rectangle of red border
Shape: Rectangle
Border Color: Red
```

  [1]: http://www.tutorialspoint.com/design_pattern/decorator_pattern.htm
  [2]: http://www.smallclover.com
