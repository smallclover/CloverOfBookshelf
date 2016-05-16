# 设计模式-代理模式

在代理模式中，我们使用一个类来代表另一个类的功能。这种类型的设计模式属于结构型设计模式的一种。
在代理模式中，我们将创建一个对象，该对象在在接口中持有原始对象，以对外部提供它的功能。

## 实现

我们将创建一个Image接口并且创建具体类实现Image接口。ProxyImage是一个代理类，使用它可以减少RealImage对象加载带来的内存占用。
ProxyPatternDemo，我们的demo类将使用ProxyImage类去加载一个Image对象并且如果需要可以展示它。

![image](/Design Pattern/translate/image/Proxy Pattern.png)

### 第一步

创建一个接口

**Image.java**

    <span class="hljs-keyword">public</span> <span class="hljs-keyword">interface</span> <span class="hljs-title">Image</span> {
       <span class="hljs-function"><span class="hljs-keyword">void</span> <span class="hljs-title">display</span><span class="hljs-params">()</span></span>;
    }
    `</pre>

    ### 第二步

    创建具体类实现Image接口

    **RealImage.java**

    <pre>`<span class="hljs-keyword">public</span> <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">RealImage</span> <span class="hljs-keyword">implements</span> <span class="hljs-title">Image</span> </span>{

       <span class="hljs-keyword">private</span> String fileName;

       <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-title">RealImage</span><span class="hljs-params">(String fileName)</span></span>{
          <span class="hljs-keyword">this</span>.fileName = fileName;
          loadFromDisk(fileName);
       }

       <span class="hljs-annotation">@Override</span>
       <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">display</span><span class="hljs-params">()</span> </span>{
          System.out.println(<span class="hljs-string">"Displaying "</span> + fileName);
       }

       <span class="hljs-function"><span class="hljs-keyword">private</span> <span class="hljs-keyword">void</span> <span class="hljs-title">loadFromDisk</span><span class="hljs-params">(String fileName)</span></span>{
          System.out.println(<span class="hljs-string">"Loading "</span> + fileName);
       }
    }
    `</pre>

    **ProxyImage.java**

    <pre>`<span class="hljs-keyword">public</span> <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">ProxyImage</span> <span class="hljs-keyword">implements</span> <span class="hljs-title">Image</span></span>{

       <span class="hljs-keyword">private</span> RealImage realImage;
       <span class="hljs-keyword">private</span> String fileName;

       <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-title">ProxyImage</span><span class="hljs-params">(String fileName)</span></span>{
          <span class="hljs-keyword">this</span>.fileName = fileName;
       }

       <span class="hljs-annotation">@Override</span>
       <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">display</span><span class="hljs-params">()</span> </span>{
          <span class="hljs-keyword">if</span>(realImage == <span class="hljs-keyword">null</span>){
             realImage = <span class="hljs-keyword">new</span> RealImage(fileName);
          }
          realImage.display();
       }
    }
    `</pre>

    ### 第三步

    使用ProxyImage在需要的时候获得RealImage类的对象

    **ProxyPatternDemo.java**

    <pre>`    <span class="hljs-keyword">public</span> <span class="hljs-keyword">class</span> <span class="hljs-title">ProxyPatternDemo</span> {

           <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">static</span> <span class="hljs-keyword">void</span> <span class="hljs-title">main</span><span class="hljs-params">(String[] args)</span> </span>{
              Image image = <span class="hljs-keyword">new</span> ProxyImage(<span class="hljs-string">"test_10mb.jpg"</span>);

              <span class="hljs-comment">//image will be loaded from disk</span>
              image.display(); 
              System.<span class="hljs-keyword">out</span>.println(<span class="hljs-string">""</span>);

              <span class="hljs-comment">//image will not be loaded from disk</span>
              image.display();     
           }
        }
    `</pre>

    ### 第四步

    <pre>`校验输出
    