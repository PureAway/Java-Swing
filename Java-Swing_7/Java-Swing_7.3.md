# 使用 Java 代码截取电脑屏幕并保存

教程总目录: [Java-Swing 图形界面开发（目录）](../README.md)

Java代码截屏使用`java.awt.Robot`中的`createScreenCapture`方法实现。

代码实例:

```java
package com.xiets.capturedemo;

import javax.imageio.ImageIO;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.File;

public class Main {

    public static void main(String[] args) throws Exception {
        // 获取屏幕尺寸
        Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();

        // 创建需要截取的矩形区域
        Rectangle rect = new Rectangle(0, 0, screenSize.width, screenSize.height);

        // 截屏操作
        BufferedImage bufImage = new Robot().createScreenCapture(rect);

        // 保存截取的图片
        ImageIO.write(bufImage, "PNG", new File("capture.png"));
    }

}
```

