# JToggleButton（开关按钮）

教程总目录: [Java-Swing 图形界面开发（目录）](../README.md)

## 1. 概述

官方JavaDocsApi: [javax.swing.JToggleButton](https://docs.oracle.com/javase/8/docs/api/javax/swing/JToggleButton.html)

`JToggleButton`，开关按钮。JToggleButton 是 JRadioButton, JCheckBox 的父类，主要实现一个按钮的两种状态（选中 和 未选中）来实现开关切换的效果。

**JToggleButton 常用构造方法**:

```java
// 无文本，默认未选中
JToggleButton()

// 有文本，默认未选中
JToggleButton(String text)

// 有文本，并指定是否选中
JToggleButton(String text, boolean selected)
```

**JToggleButton 常用方法**:

```java
// 设置开关按钮的 文本、字体 和 字体颜色
void setText(String text)
void setFont(Font font)
void setForeground(Color fg)

/* 以下方法定义在 javax.swing.AbstractButton 基类中 */

// 设置开关按钮是否选中状态
void setSelected(boolean b)

// 判断开关按钮是否选中
boolean isSelected()

// 设置开关按钮是否可用
void setEnabled(boolean enable)

// 设置开关按钮在 默认(关)、被选中(开)、不可用 时显示的图片
void setIcon(Icon defaultIcon)
void setPressedIcon(Icon pressedIcon)
void setDisabledIcon(Icon disabledIcon)

// 设置图片和文本之间的间距
void setIconTextGap(int iconTextGap)
```

**JToggleButton 常用监听器**:

```java
// 添加状态改变监听器
void addChangeListener(ChangeListener l)
```

## 2. 代码示例

```java
package com.xiets.swing;

import javax.swing.*;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

public class Main {

    public static void main(String[] args) {
        JFrame jf = new JFrame("测试窗口");
        jf.setSize(250, 250);
        jf.setLocationRelativeTo(null);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        JPanel panel = new JPanel();

        // 创建开关按钮
        JToggleButton toggleBtn = new JToggleButton("开关按钮");

        // 添加 toggleBtn 的状态被改变的监听
        toggleBtn.addChangeListener(new ChangeListener() {
            @Override
            public void stateChanged(ChangeEvent e) {
                // 获取事件源（即开关按钮本身）
                JToggleButton toggleBtn = (JToggleButton) e.getSource();
                System.out.println(toggleBtn.getText() + " 是否选中: " + toggleBtn.isSelected());
            }
        });

        panel.add(toggleBtn);

        jf.setContentPane(panel);
        jf.setVisible(true);
    }

}
```

结果展示：

![java-swing3_8](../images/java-swing3_8.gif)