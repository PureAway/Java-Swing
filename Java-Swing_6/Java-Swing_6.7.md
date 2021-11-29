# 闪屏（Splash Screen）

教程总目录: [Java-Swing 图形界面开发（目录）](../README.md)

Splash Screen，即闪屏，也可以理解为一个软件的第一个界面，欢迎界面等。启动一个 Java 虚拟机是比较耗时的，有时可能要等待几秒钟的时间，为了 GUI 应用程序的友好用户体验，在这段时间内可以使用一张图片显示在屏幕中间等待虚拟机的启动，虚拟机启动完成后，该图片自动消失，这个闪现的屏幕称为闪屏。闪屏的图片支持各种格式，例如 GIF(支持动画)、JPG、PNG等。

添加闪屏主要有两种方式:

(1) **使用 java 命令启动主类时添加闪屏参数:**

```java
// 这里的闪屏图片路径相对于当前工作路径
java -splash:filename.gif MainClass
或
java -splash:filename.gif -jar RannalbeJAR.jar
```

(2) **把闪屏图片信息添加到可执行 JAR 包内的 MANIFEST.MF 文件中:**

这里的闪屏图片需要放到 jar 包内，闪屏图片路径相对于 classpath，即 jar 包内根目录。

```java
Manifest-Version: 1.0
Main-Class: MainClass
SplashScreen-Image: filename.gif
```

