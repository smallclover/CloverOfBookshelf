> [原文链接][1]

> 译者：[smallclover][2]

>个人翻译，水平有限，如有错误欢迎指出，谢谢！

# 设计模式-生成器模式#

生成器模式使用简单的对象来逐步的构建一个复杂的对象。这种类型的设计模式是创建型模式中创建对象最好的方式之一。
一个生成器类会逐步的构建这个最终的对象。这个生成器与其他对象是相互独立的。


## 实现##

我们举一个快餐店的案例：这个快餐店的典型饮食风格是一个汉堡加一杯可乐。这里的汉堡可以是蔬菜汉堡也可以是鸡肉汉堡，它们将使用包装纸来包装；冷饮可以是可口可乐或者是百事可乐，它们将使用瓶子来包装。
我们将创建一个`Item`接口代表食品元素如汉堡和冷饮，创建具体的类实现这个`Item`接口；`Packing`接口代表包装食品元素，创建具体的类实现这个`Packing`接口，像汉堡可以通过包装纸来包装，冷饮可以通过瓶子来包装。
我们随后将创建一个`Meal`类，它有一个存储`Item`类型的`ArrayList`，然后我们使用一个`MealBuilder`来结合`Item`来构建不同类型的`Meal`对象。`BuilderPatternDemo`，我们的demo类将使用`MealBuilder`将会构建一个`Meal`。


![image](/Design Pattern/translate/image/Builder Pattern.png)

### 第一步###

创建一个接口`Item`代表食品元素和一个`Packing`接口代表包装的情况。

**Item.java**

```java
public interface Item {
   public String name();
   public Packing packing();
   public float price();
}
```
**Packing.java**
```java
public interface Packing {
   public String pack();
}
```

### 第二步###

创建具体的类来实现`Packing` 接口。

**Wrapper.java**
```java
public class Wrapper implements Packing {

   @Override
   public String pack() {
      return "Wrapper";
   }
}
```
**Bottle.java**
```java
public class Bottle implements Packing {

   @Override
   public String pack() {
      return "Bottle";
   }
}
```

### 第三步###

创建多个抽象类实现`Item`接口提供默认的功能。

**Burger.java**
```java
public abstract class Burger implements Item {

   @Override
   public Packing packing() {
      return new Wrapper();
   }

   @Override
   public abstract float price();
}
```
**ColdDrink.java**
```java
public abstract class ColdDrink implements Item {

	@Override
	public Packing packing() {
       return new Bottle();
	}

	@Override
	public abstract float price();
}
```
### 第三步###

创建具体的类继承`Burger`和`ColdDrink`类。

**VegBurger.java**
```java
public class VegBurger extends Burger {

   @Override
   public float price() {
      return 25.0f;
   }

   @Override
   public String name() {
      return "Veg Burger";
   }
}
```
**ChickenBurger.java**
```java
public class ChickenBurger extends Burger {

   @Override
   public float price() {
      return 50.5f;
   }

   @Override
   public String name() {
      return "Chicken Burger";
   }
}
```
**Coke.java**
```java
public class Coke extends ColdDrink {

   @Override
   public float price() {
      return 30.0f;
   }

   @Override
   public String name() {
      return "Coke";
   }
}
```
**Pepsi.java**
```java
public class Pepsi extends ColdDrink {

   @Override
   public float price() {
      return 35.0f;
   }

   @Override
   public String name() {
      return "Pepsi";
   }
}


### 第五步###

创建一个`Meal`类,该类包含一个`Item`的集合。

**Meal.java**
```java
  import java.util.ArrayList;
  import java.util.List;

  public class Meal {
     private List<Item> items = new ArrayList<Item>();

     public void addItem(Item item){
        items.add(item);
     }

     public float getCost(){
        float cost = 0.0f;

        for (Item item : items) {
           cost += item.price();
        }		
        return cost;
     }

     public void showItems(){

        for (Item item : items) {
           System.out.print("Item : " + item.name());
           System.out.print(", Packing : " + item.packing().pack());
           System.out.println(", Price : " + item.price());
        }		
     }
  }
```

### 第六步###

创建一个`MealBuilde`r类，这个类负责实际创建`Meal`对象。

**MealBuilder.java**
```java
public class MealBuilder {

   public Meal prepareVegMeal (){
      Meal meal = new Meal();
      meal.addItem(new VegBurger());
      meal.addItem(new Coke());
      return meal;
   }   

   public Meal prepareNonVegMeal (){
      Meal meal = new Meal();
      meal.addItem(new ChickenBurger());
      meal.addItem(new Pepsi());
      return meal;
   }
}
```

### 第七步###

`BuilderPatternDemo`使用`MealBuilder`来演示生成器模式

**BuilderPatternDemo.java**
```java
public class BuilderPatternDemo {
   public static void main(String[] args) {

      MealBuilder mealBuilder = new MealBuilder();

      Meal vegMeal = mealBuilder.prepareVegMeal();
      System.out.println("Veg Meal");
      vegMeal.showItems();
      System.out.println("Total Cost: " + vegMeal.getCost());

      Meal nonVegMeal = mealBuilder.prepareNonVegMeal();
      System.out.println("\n\nNon-Veg Meal");
      nonVegMeal.showItems();
      System.out.println("Total Cost: " + nonVegMeal.getCost());
   }
}
```

### 第八步###

校验输出
```java
Veg Meal
Item : Veg Burger, Packing : Wrapper, Price : 25.0
Item : Coke, Packing : Bottle, Price : 30.0
Total Cost: 55.0


Non-Veg Meal
Item : Chicken Burger, Packing : Wrapper, Price : 50.5
Item : Pepsi, Packing : Bottle, Price : 35.0
Total Cost: 85.5
```
## 译者注###
注意区分抽象工厂模式和生成器模式的区别：生成器模式的是生产一个复杂的产品，抽象工厂模式是生产一个族的产品。具体请参考文章[生成器模式与抽象工厂模式的区别][3]。若无法理解请自行Google，这里只做简单的介绍。


  [1]: http://www.tutorialspoint.com/design_pattern/builder_pattern.htm
  [2]: http://www.smallclover.com
  [3]: http://blog.csdn.net/hawksoft/article/details/6626775
