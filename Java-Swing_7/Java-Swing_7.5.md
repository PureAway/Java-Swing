# Java操作桌面应用 --- Desktop 类

教程总目录: [Java-Swing 图形界面开发（目录）](../README.md)

官方JavaDocsApi: [java.awt.Desktop](https://docs.oracle.com/javase/8/docs/api/java/awt/Desktop.html)

Desktop 类允许 Java 应用程序启动已在本机桌面上注册的关联应用程序，以处理 URI 或文件。

支持的操作包括:

- **打开浏览器**: 启动用户默认浏览器来显示指定的 URI；
- **打开邮件客户端**: 启动带有可选 mailto URI 的用户默认邮件客户端；
- **打开文件/文件夹**: 启动已注册的应用程序，以打开、编辑 或 打印 指定的文件。

**Desktop 类相关方法**:

```java
// 判断当前平台是否支持此类
static boolean isDesktopSupported()

// 获取与当前平台关联的 Desktop 实例
static Desktop getDesktop()

// 启动默认浏览器来显示 URI
void browse(URI uri)

// 启动关联应用程序来打开文件
void open(File file)

// 启动关联编辑器应用程序并打开用于编辑的文件
void edit(File file)

// 使用关联应用程序的打印命令, 用本机桌面打印设备来打印文件
void print(File file)

// 启动用户默认邮件客户端的邮件组合窗口
void mail()

// 启动用户默认邮件客户端的邮件组合窗口, 填充由 mailto:URI 指定的消息字段
void mail(URI mailtoURI)

/*
 * 判断当前平台是否支持某一操作, 参数为以下值之一:
 *     Desktop.Action.OPEN: 打开动作
 *     Desktop.Action.EDIT: 编辑动作
 *     Desktop.Action.PRINT: 打印动作
 *     Desktop.Action.MAIL: 邮件动作
 *     Desktop.Action.BROWSE: 浏览器动作
 */
boolean isSupported(Desktop.Action action)
```

**代码实例**:

```java
package com.xiets.desktop;

import java.awt.*;
import java.io.File;
import java.io.IOException;
import java.net.URI;

public class Main {

    public static void main(String[] args) throws IOException {
        // 先判断当前平台是否支持桌面
        if (Desktop.isDesktopSupported()) {
            // 获取当前平台桌面实例
            Desktop desktop = Desktop.getDesktop();

            // 使用默认浏览器打开链接
            desktop.browse(URI.create("https://blog.csdn.net/xietansheng"));

            // 打开指定文件/文件夹
            desktop.open(new File("C:\\"));

        } else {
            System.out.println("当前平台不支持 Desktop");
        }
    }

}
—————
```

