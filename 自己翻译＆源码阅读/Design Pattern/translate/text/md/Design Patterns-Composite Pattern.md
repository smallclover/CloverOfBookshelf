> [原文链接][1]

> 译者：[smallclover][2]

>个人翻译，水平有限，如有错误欢迎指出，谢谢！


# 设计模式-组合模式#

当我们需要以相似的方式对待一组对象和一个对象的时候使用组合模式。组合模式按照树形结构来组织对象，并且表示部分与整体之间的层次结构。这种类型的模式属于结构型模式的一种，它创建一组树形结构的对象。
该模式将创建一个包含一组特定对象（该类的对象）的类。该类提供方法修改这组相同的对象。
我们将通过下面的例子来展示一个组织的员工层次结构。

## 实现##

我们有一个`Employee`类，该类扮演组合的角色。`CompositePatternDemo`,我们的demo类将使用`Employee`类来 打印一个公司的层次结构。

![image](/Design Pattern/translate/image/Composite.png)


### 第一步###

创建一个Employee类，该类持有一个Employee对象集合。

**Employee.java**

```java
import java.util.ArrayList;
import java.util.List;

public class Employee {
   private String name;
   private String dept;
   private int salary;
   private List<Employee> subordinates;

   // constructor
   public Employee(String name,String dept, int sal) {
      this.name = name;
      this.dept = dept;
      this.salary = sal;
      subordinates = new ArrayList<Employee>();
   }

   public void add(Employee e) {
      subordinates.add(e);
   }

   public void remove(Employee e) {
      subordinates.remove(e);
   }

   public List<Employee> getSubordinates(){
     return subordinates;
   }

   public String toString(){
      return ("Employee :[ Name : " + name + ", dept : " + dept + ", salary :" + salary+" ]");
   }   
}
```

### 第二步###

使用这个`Employee`类，创建并且打印employee的层次结构。

**CompositePatternDemo.java**

```java
public class CompositePatternDemo {
   public static void main(String[] args) {

      Employee CEO = new Employee("John","CEO", 30000);

      Employee headSales = new Employee("Robert","Head Sales", 20000);

      Employee headMarketing = new Employee("Michel","Head Marketing", 20000);

      Employee clerk1 = new Employee("Laura","Marketing", 10000);
      Employee clerk2 = new Employee("Bob","Marketing", 10000);

      Employee salesExecutive1 = new Employee("Richard","Sales", 10000);
      Employee salesExecutive2 = new Employee("Rob","Sales", 10000);

      CEO.add(headSales);
      CEO.add(headMarketing);

      headSales.add(salesExecutive1);
      headSales.add(salesExecutive2);

      headMarketing.add(clerk1);
      headMarketing.add(clerk2);

      //print all employees of the organization
      System.out.println(CEO);

      for (Employee headEmployee : CEO.getSubordinates()) {
         System.out.println(headEmployee);

         for (Employee employee : headEmployee.getSubordinates()) {
            System.out.println(employee);
         }
      }		
   }
}
```

### 第三步###

校验输出。

```java
Employee :[ Name : John, dept : CEO, salary :30000 ]
Employee :[ Name : Robert, dept : Head Sales, salary :20000 ]
Employee :[ Name : Richard, dept : Sales, salary :10000 ]
Employee :[ Name : Rob, dept : Sales, salary :10000 ]
Employee :[ Name : Michel, dept : Head Marketing, salary :20000 ]
Employee :[ Name : Laura, dept : Marketing, salary :10000 ]
Employee :[ Name : Bob, dept : Marketing, salary :10000 ]
```    
*鸡汤:-D*
*我必须努力*   
 *i have to work hand*
   *私は努力しなければならない*
  [1]: http://www.tutorialspoint.com/design_pattern/composite_pattern.htm
  [2]: http://www.smallclover.com
