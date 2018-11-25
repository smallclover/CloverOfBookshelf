> [原文链接][1]

> 译者：[smallclover][2]

>个人翻译，水平有限，如有错误欢迎指出，谢谢！

# 设计模式-桥模式#

我们使用桥来**解耦(decouple)**
一个抽象以及该抽象的实现。使用桥之后抽象和实现可以相互独立的改变。这种类型的设计模式来源于结构型模式，它可以通过使用桥结构来解耦抽象类及其实现类。

这种模式涉及一个接口，它扮演一个桥的角色，使得具体类的功能独立与接口。这两种类型的类可以在不影响对方的情况下改变自身结构。

我们通过下面的例子来演示桥模式的使用。画一个圆使用不同的颜色，相同的抽象类方法，不同的桥的具体实现者。

![image](/Design Pattern/translate/image/Bridge Pattern.png)



## 实现##

我们有一个DrawAPI接口，它扮演一个桥的实现化者的角色，然后会有具体的类RedCircle和GreenCircle实现接口DrawAPI。抽象类Shape将持有DrawAPI对象。BridgePatternDemo，我们的demo类将使用Shape类画两个不同颜色的圆。


***译者注***：**bridge implementer** 这里翻译为**桥的实现化**者，它不同于具体的实现，如：继承，实现。这里的实现是指对桥这种概念的具体化，实现化。


### 第一步###

创建一个桥的实现化者接口DrawAPI

**DrawAPI.java**
```java
public interface DrawAPI {
   public void drawCircle(int radius, int x, int y);
}
```

### 第二步###

创建具体的类实现DrawApI接口

**RedCircle.java**
```java
public class RedCircle implements DrawAPI {
   @Override
   public void drawCircle(int radius, int x, int y) {
      System.out.println("Drawing Circle[ color: red, radius: " + radius + ", x: " + x + ", " + y + "]");
   }
}
```
**GreenCircle.java**
```java
public class GreenCircle implements DrawAPI {
   @Override
   public void drawCircle(int radius, int x, int y) {
      System.out.println("Drawing Circle[ color: green, radius: " + radius + ", x: " + x + ", " + y + "]");
   }
}
```

### 第三步###

创建一个抽象类 Shape，该类持有一个DrawAPI接口的引用。


**Shape.java**
```java
public abstract class Shape {
   protected DrawAPI drawAPI;

   protected Shape(DrawAPI drawAPI){
      this.drawAPI = drawAPI;
   }
   public abstract void draw();
}
```

### 第四步###

创建一个具体类实现抽象类Shape。

**Circle.java**
```java
public class Circle extends Shape {
   private int x, y, radius;

   public Circle(int x, int y, int radius, DrawAPI drawAPI) {
      super(drawAPI);
      this.x = x;  
      this.y = y;  
      this.radius = radius;
   }

   public void draw() {
      drawAPI.drawCircle(radius,x,y);
   }
}
```

### 第五步###

使用Shape和DrawAPI类画两个不同颜色的圆。

**BridgePatternDemo.java**
```java
public class BridgePatternDemo {
   public static void main(String[] args) {
      Shape redCircle = new Circle(100,100, 10, new RedCircle());
      Shape greenCircle = new Circle(100,100, 10, new GreenCircle());

      redCircle.draw();
      greenCircle.draw();
   }
}
```

### 第六步###

校验输出。

```java

Drawing Circle[ color: red, radius: 10, x: 100, 100]
Drawing Circle[  color: green, radius: 10, x: 100, 100]
```

  [1]: http://www.tutorialspoint.com/design_pattern/bridge_pattern.htm
  [2]: http://www.smallclover.com
