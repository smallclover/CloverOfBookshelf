> [原文链接][1]

> 译者：[smallclover][2]

> Thanks for your watching

# 设计模式-Null Object Pattern


在Null Object①设计模式中，一个Null Object替换对一个值为null的object的检查，而不是通过if语句来判断该值是不是为null。Null Object反映了一种do-nothing②的关系。这样的Null Object也可以用于提供默认行为，当数据不可用时。
在 Null Object 模式中，我们创建一个 抽象类声明了各种各样需要之执行的操作，创建具体的类继承这个抽象类，并且创建一个Null Object类来提供do-nothing的实现，同时也能在我们需要的时候帮我们检测null值。

** * 译注 * **

**
①	Null Object 直译的话就是空对象，感觉不够优雅，而且不太符合它的实际意义，所以暂时使用英文单词来代替。这里的Null Object不是指对象的值为null（Object object = null）而是指，该对象表达的是Null的含义。我们人为的为null赋予具体的含义，让null代表一种特殊的数据状态。来使程序语义更加的明确，避免空值和null等数据值使得程序语义混乱，以及null值导致程序的崩溃等等。这种为null赋予具体含义的思想 在Google的java类库guava中有很好的实现。
**


**
②	在本文中do-nothing 指，若对象的值为null时，将不做任何动作。
**


## 实现

我们将创建一个抽象类AbstractCustomer，该类声明了两个方法以及记录客户端名字的属性值。创建具体的类集成该抽象类。工厂类CustomerFactory通过 客户端传递给它的名字来创建并返回RealCustomer或者NullCustomer的对象。
NullPatternDemo，我们的demo类，将使用CustomerFactory来展示如何使用NullObjectPattern。


### 第一步


创建抽象类

** AbstractCustomer.java **

```java
public abstract class AbstractCustomer {
   protected String name;
   public abstract boolean isNil();
   public abstract String getName();
}
```

### 第二步


创建具体的类继承抽象类 AbstractCustomer.java

** RealCustomer.java **

```java
public class RealCustomer extends AbstractCustomer {

   public RealCustomer(String name) {
      this.name = name;		
   }

   @Override
   public String getName() {
      return name;
   }

   @Override
   public boolean isNil() {
      return false;
   }
}
```
** NullCustomer.java **

```java
public class NullCustomer extends AbstractCustomer {

   @Override
   public String getName() {
      return "Not Available in Customer Database";
   }

   @Override
   public boolean isNil() {
      return true;
   }
}
```
### 第三步

创建CustomerFactory类

** CustomerFactory.java **

```java
public class CustomerFactory {

   public static final String[] names = {"Rob", "Joe", "Julie"};

   public static AbstractCustomer getCustomer(String name){

      for (int i = 0; i < names.length; i++) {
         if (names[i].equalsIgnoreCase(name)){
            return new RealCustomer(name);
         }
      }
      return new NullCustomer();
   }
}
```

### 第四步


使用CustomerFactory类通过customer传递的name值来获取RealCustomer或者NullCustomer类的对象.

** NullPatternDemo.java **

```java
public class NullPatternDemo {
   public static void main(String[] args) {

      AbstractCustomer customer1 = CustomerFactory.getCustomer("Rob");
      AbstractCustomer customer2 = CustomerFactory.getCustomer("Bob");
      AbstractCustomer customer3 = CustomerFactory.getCustomer("Julie");
      AbstractCustomer customer4 = CustomerFactory.getCustomer("Laura");

      System.out.println("Customers");
      System.out.println(customer1.getName());
      System.out.println(customer2.getName());
      System.out.println(customer3.getName());
      System.out.println(customer4.getName());
   }
}
```

### 第五步


校验输出

```java
Customers
Rob
Not Available in Customer Database
Julie
Not Available in Customer Database
```

[推荐阅读：被遗忘的设计模式][3]


[1]:  https://www.tutorialspoint.com/design_pattern/null_object_pattern.htm
[2]: http://www.smallclover.com

[3]:http://www.2cto.com/kf/201504/388387.html
