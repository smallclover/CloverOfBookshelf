
# 设计模式-代理模式


在代理模式中，我们使用一个类来代表另一个类的功能。这种类型的设计模式属于结构型设计模式的一种。
在代理模式中，我们将创建一个对象，该对象在在接口中持有原始对象，以对外部提供它的功能。

## 实现

我们将创建一个Image接口并且创建具体类实现Image接口。ProxyImage是一个代理类，使用它可以减少RealImage对象加载带来的内存占用。
ProxyPatternDemo，我们的demo类将使用ProxyImage类去加载一个Image对象并且如果需要可以展示它。
 
![image](/Design Pattern/translate/image/Proxy Pattern.png)

### 第一步

创建一个接口
** Image.java**

    public interface Image {
       void display();
    }

### 第二步

创建具体类实现Image接口
**RealImage.java**

    public class RealImage implements Image {
    
       private String fileName;
    
       public RealImage(String fileName){
          this.fileName = fileName;
          loadFromDisk(fileName);
       }
    
       @Override
       public void display() {
          System.out.println("Displaying " + fileName);
       }
    
       private void loadFromDisk(String fileName){
          System.out.println("Loading " + fileName);
       }
    }

**ProxyImage.java**

    public class ProxyImage implements Image{
    
       private RealImage realImage;
       private String fileName;
    
       public ProxyImage(String fileName){
          this.fileName = fileName;
       }
    
       @Override
       public void display() {
          if(realImage == null){
             realImage = new RealImage(fileName);
          }
          realImage.display();
       }
    }

### 第三步

使用ProxyImage在需要的时候获得RealImage类的对象
**ProxyPatternDemo.java**
```
    public class ProxyPatternDemo {
    	
       public static void main(String[] args) {
          Image image = new ProxyImage("test_10mb.jpg");
    
          //image will be loaded from disk
          image.display(); 
          System.out.println("");
          
          //image will not be loaded from disk
          image.display(); 	
       }
    }
```
### 第四步


```
校验输出
```

