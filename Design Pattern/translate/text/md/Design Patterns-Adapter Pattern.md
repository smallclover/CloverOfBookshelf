> [原文链接][1]

> 译者：[smallclover][2]

>个人翻译，水平有限，如有错误欢迎指出，谢谢！

# 设计模式-适配器模式#


适配器模式作为桥梁，连接两个不兼容的接口。这种类型的设计模式来源于结构型模式，它具有结合两个相互独立的接口的能力。

这个模式涉及到单个类，该类负责接入独立的、不兼容的接口。一个现实生活的例子，比如说读卡器，它可能会在记忆卡和笔记本电脑之间扮演一个适配者的角色。首先把记忆卡插到读卡器上，在把读卡器插入笔记本上，然后我们就可以从笔记本读取记忆卡上的数据。
我们通过以下的例子来展示适配器模式。一个音频播放器设备只能播放mp3文件；而另一个比较先进的音乐播放器可以播放vlc和mp4文件。

![image](/Design Pattern/translate/image/Adapter Pattern.png)


## 实现

我们有一个`MediaPlayer`接口和一个实现该接口的实体类`AudioPlayer`，这个`AudioPlayer`默认播放mp3格式的音频。

我们还有另外一个接口 `AdvancedMediaPalyer` 和实现该接口的实体类
这些实体类可以播放**vlc**和**mp4**格式的音频。

我们希望`AudioPlayer`也可以播放其他格式的文件。为了实现这个目标，我们创建了一个适配器类`MediaAdapter`，该类实现了接口`MediaPlayer`，并且使用`AdvancedMediaPlayer`的对象来播放需要的格式。


`AudioPlayer` 使用适配器类 `MediaAdapter`，通过它来播放所期望的音频类型，不需要知道实际是哪个类播放这个期望的音频类型。`AdapterPatternDemo`，我们的demo类将使用`AudioPlayer`类来播放各种格式的音频。


### 第一步###

创建`MediaPlayer`和`AdvancedMediaPlayer`接口。

**MediaPlayer.java**
```java
public interface MediaPlayer {
   public void play(String audioType, String fileName);
}
```

**AdvancedMediaPlayer.java**
```java
public interface AdvancedMediaPlayer {
   public void playVlc(String fileName);
   public void playMp4(String fileName);
}
```

### 第二步###

创建实体类实现`AdvancedMediaPlayer`接口。

**VlcPlayer.java**
```java
public class VlcPlayer implements AdvancedMediaPlayer{
   @Override
   public void playVlc(String fileName) {
      System.out.println("Playing vlc file. Name: "+ fileName);		
   }

   @Override
   public void playMp4(String fileName) {
      //什么也不做
   }
}
```
**Mp4Player.java**
```java
public class Mp4Player implements AdvancedMediaPlayer{

   @Override
   public void playVlc(String fileName) {
      //什么也不做
   }

   @Override
   public void playMp4(String fileName) {
      System.out.println("Playing mp4 file. Name: "+ fileName);		
   }
}
```

### 第三步###

创建一个适配器类实现`MediaPlayer`接口

**MediaAdapter.java**
```java
public class MediaAdapter implements MediaPlayer {

   AdvancedMediaPlayer advancedMusicPlayer;

   public MediaAdapter(String audioType){

      if(audioType.equalsIgnoreCase("vlc") ){
         advancedMusicPlayer = new VlcPlayer();			

      }else if (audioType.equalsIgnoreCase("mp4")){
         advancedMusicPlayer = new Mp4Player();
      }
   }

   @Override
   public void play(String audioType, String fileName) {

      if(audioType.equalsIgnoreCase("vlc")){
         advancedMusicPlayer.playVlc(fileName);
      }
      else if(audioType.equalsIgnoreCase("mp4")){
         advancedMusicPlayer.playMp4(fileName);
      }
   }
}
```

### 第四步###

创建实体类实现`MediaPlayer`

**AudioPlayer.java**
```java
public class AudioPlayer implements MediaPlayer {
   MediaAdapter mediaAdapter;

   @Override
   public void play(String audioType, String fileName) {		

      //内置支持播放MP3类型的音乐
      if(audioType.equalsIgnoreCase("mp3")){
         System.out.println("Playing mp3 file. Name: " + fileName);			
      }

      //mediaAdapter 提供播放其他格式音频文件的支持
      else if(audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")){
         mediaAdapter = new MediaAdapter(audioType);
         mediaAdapter.play(audioType, fileName);
      }

      else{
         System.out.println("Invalid media. " + audioType + " format not supported");
      }
   }   
}
```

### 第五步###

使用`AudioPlayer`播放不同种类的音频格式。

**AdapterPatternDemo.java**
```java
public class AdapterPatternDemo {
   public static void main(String[] args) {
      AudioPlayer audioPlayer = new AudioPlayer();

      audioPlayer.play("mp3", "beyond the horizon.mp3");
      audioPlayer.play("mp4", "alone.mp4");
      audioPlayer.play("vlc", "far far away.vlc");
      audioPlayer.play("avi", "mind me.avi");
   }
}
```

### 第六步###

校验输出。
```java
Playing mp3 file. Name: beyond the horizon.mp3
Playing mp4 file. Name: alone.mp4
Playing vlc file. Name: far far away.vlc
Invalid media. avi format not supported
```

  [1]: http://www.tutorialspoint.com/design_pattern/adapter_pattern.htm
  [2]: http://www.smallclover.com
