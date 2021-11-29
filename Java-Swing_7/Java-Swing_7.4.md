# ava模拟鼠标键盘输入事件 --- Robot 类

教程总目录: [Java-Swing 图形界面开发（目录）](../README.md)

官方JavaDocsApi: [java.awt.Robot](https://docs.oracle.com/javase/8/docs/api/java/awt/Robot.html)

Robot，机器人。此类用于为测试自动化、自运行演示程序和其他需要控制鼠标和键盘的应用程序生成本机系统输入事件。Robot 的主要目的是便于 Java 平台实现自动测试。

Robot 可以模拟鼠标和键盘的输入，相当于 **Java 版的按键精灵**。

**Robot 构造方法**:

```java
// 在基本屏幕坐标系中构造一个 Robot 对象, 如果平台不支持 Robot, 将抛出异常
Robot()

// 为给定屏幕设备创建一个 Robot（用于同时使用多个显示设备的情况）
Robot(GraphicsDevice screen)
```

**模拟鼠标的方法**:

```java
// 将鼠标指针移动到指定屏幕坐标
void mouseMove(int x, int y)

/**
 * 按下/释放一个或多个鼠标按钮, 参数说明:
 *     buttons: 鼠标按钮掩码, 一个或多个以下标志的组合:
 *              InputEvent.BUTTON1_MASK 鼠标左键
 *              InputEvent.BUTTON2_MASK 鼠标中键
 *              InputEvent.BUTTON3_MASK 鼠标右键
 */
void mousePress(int buttons)
void mouseRelease(int buttons)

// 在配有滚轮的鼠标上旋转滚轮
void mouseWheel(int wheelAmt)
```

**模拟键盘的方法**:

```java
/**
 * 按下/释放键盘按键, 参数说明:
 *     keycode: 键盘键值常量, 定义在 KeyEvent.VK_XXX 中
 */
void keyPress(int keycode)
void keyRelease(int keycode)
```

**屏幕相关方法**:

```java
// 获取指定屏幕坐标处的像素颜色
Color getPixelColor(int x, int y)

// 截屏, 截取指定的矩形区域
BufferedImage createScreenCapture(Rectangle screenRect)
```

**控制类方法**:

```java
// 睡眠指定的时间, 相当于 Thread.sleep(long ms)
void delay(int ms)

// 在处理完当前事件队列中的所有事件之前, 一直等待
void waitForIdle()

// 设置此 Robot 在生成一个事件后是否自动调用 waitForIdle()
// 设置为 true, 表示添加的事件逐个按顺序执行（执行完一个再执行下一个）
void setAutoWaitForIdle(boolean isOn)
boolean isAutoWaitForIdle()

// 设置此 Robot 每在生成一个事件后自动睡眠的毫秒数
void setAutoDelay(int ms)
int getAutoDelay()
```

**一般开发步骤模（模拟鼠标事件）**:

```java
package com.xiets.robot;

import java.awt.*;
import java.awt.event.InputEvent;

public class Main {

    public static void main(String[] args) throws AWTException {
        // 创建 Robot 实例
        Robot robot = new Robot();

        // 执行完一个事件后再执行下一个
        robot.setAutoWaitForIdle(true);

        // 移动鼠标到指定屏幕坐标
        robot.mouseMove(100, 100);

        // 按下鼠标左键
        robot.mousePress(InputEvent.BUTTON1_MASK);

        // 延时100毫秒
        robot.delay(100);

        // 释放鼠标左键（按下后必须要释放, 一次点击操作包含了按下和释放）
        robot.mouseRelease(InputEvent.BUTTON1_MASK);
    }

}
```

