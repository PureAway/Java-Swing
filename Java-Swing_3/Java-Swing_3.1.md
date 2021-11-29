# JLabel（标签）

教程总目录: [Java-Swing 图形界面开发（目录）](../README.md)

## 1. 概述

官方JavaDocsApi: [javax.swing.JLabel](https://docs.oracle.com/javase/8/docs/api/javax/swing/JLabel.html)

`JLabel`，标签。标签主要用于展示 **文本** 或 **图片**，也可以 **同时显示文本和图片**。

**JLabel 的构造方法**:

```java
/*
 * 构造方法中的参数含义:
 *     text: 标签显示的 文本
 *     image: 标签显示的 图片
 *     horizontalAlignment: 标签内容（在标签内）的水平对其方式（竖直方向默认居中, 可通过方法设置）
 */
JLabel()

JLabel(String text)

JLabel(String text, int horizontalAlignment)

JLabel(Icon image) 

JLabel(Icon image, int horizontalAlignment) 

JLabel(String text, Icon image, int horizontalAlignment) 
```

**JLabel 的常用方法**:

```java
// 设置 文本 和 图片
void setText(String text)
void setIcon(Icon icon)

// 设置文本相对于图片的位置（文本默认在图片右边垂直居中）
void setHorizontalTextPosition(int textPosition)
void setVerticalTextPosition(int textPosition)

// 设置标签内容（在标签内）的对其方式（默认左对齐并垂直居中）
void setHorizontalAlignment(int alignment)
void setVerticalAlignment(int alignment)

// 设置图片和文本之间的间隙
void setIconTextGap(int iconTextGap)

/* 
 * 下面的方法定义在 JComponent 基类中
 */

// 设置文本的字体类型、样式 和 大小
void setFont(Font font)

// 设置字体颜色
void setForeground(Color fg)

// 当鼠标移动到组件上时显示的提示文本
void setToolTipText(String text)

// 设置组件的背景
void setBackground(Color bg)

// 设置组件是否可见
void setVisible(boolean visible)

// 设置组件是否为 不透明，JLabel默认为透明，设置为不透明后才能显示背景
void setOpaque(boolean isOpaque)

// 设置组件的 首选 大小
void setPreferredSize(Dimension preferredSize)

// 设置组件的 最小 大小
void setMinimumSize(Dimension minimumSize)

// 设置组件的 最大 大小
void setMaximumSize(Dimension maximumSize)

/*
 * 上面的对齐参数具体的取值常量参考 DocsApi；
 * setXXX(...) 方法往往都对应着 getXXX() 方法。
 */
```

显示图片时，`Icon`实例的创建（一般创建`ImageIcon`，ImageIcon 实现了 Icon）:

**ImageIcon 的构造方法**:

```java
// 使用 本地路径 图片创建 ImageIcon
ImageIcon(String filename)

// 使用 网络路径 图片创建 ImageIcon
ImageIcon(URL location)

// 使用图片文件的字节数组创建 ImageIcon
ImageIcon(byte[] imageData)

// 使用 java.awt.Image 实例创建 ImageIcon
ImageIcon(java.awt.Image image)
```

**java.awt.Image 实例的创建**:

```java
// 方法一: 通过 java.awt.Toolkit 工具类来读取本地、网络 或 内存中 的 图片（支持 GIF、JPEG 或 PNG）
Image image = Toolkit.getDefaultToolkit().getImage(String filename);
Image image = Toolkit.getDefaultToolkit().getImage(URL url);
Image image = Toolkit.getDefaultToolkit().createImage(byte[] imageData);

// 方法二: 通过 javax.imageio.ImageIO 工具类读取本地、网络 或 内存中 的 图片（BufferedImage 继承自 Image）
BufferedImage bufImage = ImageIO.read(File input);
BufferedImage bufImage = ImageIO.read(URL input);
BufferedImage bufImage = ImageIO.read(InputStream input);

/*
 * PS_01: 图片宽高: BufferedImage 可以通过 bufImage.getWidth() 和 bufImage.getHeight() 方法直接获取图片的宽高;
 *                 Image 获取宽高需要另外传入一个 ImageObserver 参数。
 *
 * PS_02: 图片裁剪: BufferedImage 通过 bufImage.getSubimage(int x, int y, int w, int h) 方法可以截取图片的
 *                 任意一部分，返回一个新的 BufferedImage 实例。
 *
 * PS_03: 图片缩放: Image 通过 image.getScaledInstance(int width, int height, int hints) 方法可以对图片进行
 *                 缩放，返回新的一个 Image 实例。
 */
```

## 2. 代码示例

```java
package com.xiets.swing;

import javax.swing.*;
import java.awt.*;

public class Main {

    public static void main(String[] args) {
        JFrame jf = new JFrame("测试窗口");
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        // 创建内容面板，默认使用流式布局
        JPanel panel = new JPanel();

        /*
         * 只显示文本
         */
        JLabel label01 = new JLabel();
        label01.setText("Only Text");
        label01.setFont(new Font(null, Font.PLAIN, 25));  // 设置字体，null 表示使用默认字体
        panel.add(label01);

        /*
         * 只显示图片
         */
        JLabel label02 = new JLabel();
        label02.setIcon(new ImageIcon("demo01.jpg"));
        panel.add(label02);

        /*
         * 同时显示文本和图片
         */
        JLabel label03 = new JLabel();
        label03.setText("文本和图片");
        label03.setIcon(new ImageIcon("demo02.jpg"));
        label03.setHorizontalTextPosition(SwingConstants.CENTER);   // 水平方向文本在图片中心
        label03.setVerticalTextPosition(SwingConstants.BOTTOM);     // 垂直方向文本在图片下方
        panel.add(label03);

        jf.setContentPane(panel);
        jf.pack();
        jf.setLocationRelativeTo(null);
        jf.setVisible(true);
    }

}
```

结果展示：

![java-swing3_1](../images/java-swing3_1.png)