> [原文连接][1]

> 译者 [smallclover][2]

> 希望对大家有所帮助。谢谢！

# 设计模式-命令模式


命令模式是一种数据驱动的设计模式，属于行为型模式这一类。命令模式会将一个请求包装成一个对象并以命令的方式传递给调用者对象。调用者对象会寻找合适的并且能够处理该命令的对象，然后把该命令传递给相应的对象处理。

## 实现

我们创建了一个Order接口，该接口代表一组命令。紧接着创建一个Stock类代表请求。创建具体的命令类 BuyStock和SellStock 实现Order接口，它们将会作为具体的命令被处理。 Broker 代表调用者，它能获得并且发出命令。
Broker对象将通过命令模式来识别哪种对象该执行哪种命令。CommandPatternDemo，我们的demo类，将使用Broker类来演示命令模式。


![clipboard.png](/Design Pattern/translate/image/Commad Pattern.png)


### 第一步

创建命令接口。

**Order.java**

```java
public interface Order {
   void execute();
}
```

### 第二步

创建一个请求类

**Stock.java**

```java
public class Stock {

   private String name = "ABC";
   private int quantity = 10;

   public void buy(){
      System.out.println("Stock [ Name: "+name+",
         Quantity: " + quantity +" ] bought");
   }
   public void sell(){
      System.out.println("Stock [ Name: "+name+",
         Quantity: " + quantity +" ] sold");
   }
}
```

### 第三步

创建具体类实现Order接口


**BuyStock.java**

```java
public class BuyStock implements Order {
   private Stock abcStock;

   public BuyStock(Stock abcStock){
      this.abcStock = abcStock;
   }

   public void execute() {
      abcStock.buy();
   }
}
```

**SellStock.java**
```java
public class SellStock implements Order {
   private Stock abcStock;

   public SellStock(Stock abcStock){
      this.abcStock = abcStock;
   }

   public void execute() {
      abcStock.sell();
   }
}
```

### 第四步

创建命令调用者类

**Broker.java**
```java
import java.util.ArrayList;
import java.util.List;

   public class Broker {
   private List<Order> orderList = new ArrayList<Order>();

   public void takeOrder(Order order){
      orderList.add(order);		
   }

   public void placeOrders(){

      for (Order order : orderList) {
         order.execute();
      }
      orderList.clear();
   }
}
```

### 第五步

使用Broker类获得并且执行命令

**CommandPatternDemo.java**
```java
public class CommandPatternDemo {
   public static void main(String[] args) {
      Stock abcStock = new Stock();

      BuyStock buyStockOrder = new BuyStock(abcStock);
      SellStock sellStockOrder = new SellStock(abcStock);

      Broker broker = new Broker();
      broker.takeOrder(buyStockOrder);
      broker.takeOrder(sellStockOrder);

      broker.placeOrders();
   }
}
```

### 第六步

校验输出。
```java
Stock [ Name: ABC, Quantity: 10 ] bought
Stock [ Name: ABC, Quantity: 10 ] sold
```


  [1]: http://www.tutorialspoint.com/design_pattern/command_pattern.htm
  [2]: https://www.smallclover.com
