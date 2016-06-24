> [原文地址][1]
> 译者 [smallclover][2]
> 希望对你们有所帮助
# 设计模式-迭代器模式

迭代器是Java和.Net程序环境下经常使用的一种设计模式。这种设计模式通常用来获取能顺序访问集合对元素象的方式，并且不需要了解底层是如何实现的。
迭代器模式属于行为型模式下的一种。

## 实现

我们将创建一个Iterator接口，该接口描述迭代所需要的方法；紧接着声明了一个Container接口，该接口返回一个iterator对象。我们会创建具体的类实现Container接口和Iterator接口，并去使用它们。
IteratorPatternDemo，我们的demo类将使用NamesRepository类，该类有一个集合存储要被打印的名字。


### 第一步

创建接口

**Iterator.java**
```java
public interface Iterator {
   public boolean hasNext();
   public Object next();
}
```
**Container.java**
```java
public interface Container {
   public Iterator getIterator();
}
```

### 第二步

创建具体类实现Container接口，该类还有一个内部类NameIterator实现了Iterator接口。
**NameRepository.java**
```java
public class NameRepository implements Container {
   public String names[] = {"Robert" , "John" ,"Julie" , "Lora"};

   @Override
   public Iterator getIterator() {
      return new NameIterator();
   }

   private class NameIterator implements Iterator {

      int index;

      @Override
      public boolean hasNext() {

         if(index < names.length){
            return true;
         }
         return false;
      }

      @Override
      public Object next() {

         if(this.hasNext()){
            return names[index++];
         }
         return null;
      }		
   }
}
```
### 第三步

使用NameRepository获得迭代器并且打印name。
**IteratorPatternDemo.java**
```java
public class IteratorPatternDemo {

   public static void main(String[] args) {
      NameRepository namesRepository = new NameRepository();

      for(Iterator iter = namesRepository.getIterator(); iter.hasNext();){
         String name = (String)iter.next();
         System.out.println("Name : " + name);
      } 	
   }
}

```
### 第四步

校验输出

```java
Name : Robert
Name : John
Name : Julie
Name : Lora
```


  [1]: http://www.tutorialspoint.com/design_pattern/iterator_pattern.htm
  [2]: https://www.smallclover.com
