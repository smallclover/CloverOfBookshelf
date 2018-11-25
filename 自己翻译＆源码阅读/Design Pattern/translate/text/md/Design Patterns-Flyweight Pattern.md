> [原文链接][1]

> 译者：[smallclover][2]

> 希望对你有所帮助，谢谢！



  [1]: http://www.tutorialspoint.com/design_pattern/flyweight_pattern.htm
  [2]: http://www.smallclover.com

# 设计模式-享元模式

享元模式主要用来减少对象的数量（复用我们内存中已存在的对象，减少在系统创建对象实例），以此来减少对内存资源的占用，从而提高系统的性能。这种类型的设计模式属于结构型模式的一种，该模式会提供相应的方法使我们达到减少对象数量目的，从而改善应用的对象结构。

享元模式会复用那些内存中已经存在且与请求对象相似的对象，而不是去创建新的对象，那些已经存在的对象会以某种方式存储，如果没有发现与请求匹配的对象时将会创建新的对象。我们将演示该模式，通过只使用5个对象在不同位置画20个的圆的方式。只会使用5种颜色，因为我们需要颜色属性来检测已经存在的Circle对象。

## 实现


我们将创建一个接口Shape，然后一个具体的类Circle实现Shape接口。接下来我们会声明一个工厂类ShapeFactory。

ShapeFactory有一个存储Circle 的HashMap，该数据结构的key是color，value是Circle对象。无论请求要求ShapeFactory创建何种颜色的Circle对象，它都会检查Circle对象是否存在于HashMap，如果Circle对象被发现，那么就直接返回；否则会创建一个新的对象，并且把它存储在HashMap以备将来使用，然后返回该对象到客户端。

FlyWeightPatternDemo, 我们的demo类，将通过ShapeFactory来获取Shape对象，demo类通过传送(red / green / blue/ black / white)信息到ShapeFactory来获取它所需要的颜色的圆。

![clipboard.png](/Design Pattern/translate/image/Flyweight Pattern.png)

# 第一步

创建一个接口Shape

**Shape.java**
```java
public interface Shape {
   void draw();
}
```
# 第二步

创建具体的类来实现Shape接口

**Circle.java**
```java
public class Circle implements Shape {
   private String color;
   private int x;
   private int y;
   private int radius;//半径

   public Circle(String color){
      this.color = color;		
   }

   public void setX(int x) {
      this.x = x;
   }

   public void setY(int y) {
      this.y = y;
   }

   public void setRadius(int radius) {
      this.radius = radius;
   }

   @Override
   public void draw() {
      System.out.println("Circle: Draw() [Color : " + color + ", x : " + x + ", y :" + y + ", radius :" + radius);
   }
}
```
# 第三步

创建一个工厂根据给予的信息创建具体类的对象。

**ShapeFactory.java**
```java
import java.util.HashMap;

public class ShapeFactory {
   private static final HashMap<String, Shape> circleMap = new HashMap();

   public static Shape getCircle(String color) {
      Circle circle = (Circle)circleMap.get(color);

      if(circle == null) {
         circle = new Circle(color);
         circleMap.put(color, circle);
         System.out.println("Creating circle of color : " + color);
      }
      return circle;
   }
}
```
# 第四步

通过向工厂传送color属性来获取具体类的对象

**FlyweightPatternDemo.java**
```java
public class FlyweightPatternDemo {
   private static final String colors[] = { "Red", "Green", "Blue", "White", "Black" };
   public static void main(String[] args) {

      for(int i=0; i < 20; ++i) {
         Circle circle = (Circle)ShapeFactory.getCircle(getRandomColor());
         circle.setX(getRandomX());
         circle.setY(getRandomY());
         circle.setRadius(100);
         circle.draw();
      }
   }
   private static String getRandomColor() {
      return colors[(int)(Math.random()*colors.length)];
   }
   private static int getRandomX() {
      return (int)(Math.random()*100 );
   }
   private static int getRandomY() {
      return (int)(Math.random()*100);
   }
}
```
# 第五步

校验输出
```java
Creating circle of color : Black
Circle: Draw() [Color : Black, x : 36, y :71, radius :100
Creating circle of color : Green
Circle: Draw() [Color : Green, x : 27, y :27, radius :100
Creating circle of color : White
Circle: Draw() [Color : White, x : 64, y :10, radius :100
Creating circle of color : Red
Circle: Draw() [Color : Red, x : 15, y :44, radius :100
Circle: Draw() [Color : Green, x : 19, y :10, radius :100
Circle: Draw() [Color : Green, x : 94, y :32, radius :100
Circle: Draw() [Color : White, x : 69, y :98, radius :100
Creating circle of color : Blue
Circle: Draw() [Color : Blue, x : 13, y :4, radius :100
Circle: Draw() [Color : Green, x : 21, y :21, radius :100
Circle: Draw() [Color : Blue, x : 55, y :86, radius :100
Circle: Draw() [Color : White, x : 90, y :70, radius :100
Circle: Draw() [Color : Green, x : 78, y :3, radius :100
Circle: Draw() [Color : Green, x : 64, y :89, radius :100
Circle: Draw() [Color : Blue, x : 3, y :91, radius :100
Circle: Draw() [Color : Blue, x : 62, y :82, radius :100
Circle: Draw() [Color : Green, x : 97, y :61, radius :100
Circle: Draw() [Color : Green, x : 86, y :12, radius :100
Circle: Draw() [Color : Green, x : 38, y :93, radius :100
Circle: Draw() [Color : Red, x : 76, y :82, radius :100
Circle: Draw() [Color : Blue, x : 95, y :82, radius :100
```
