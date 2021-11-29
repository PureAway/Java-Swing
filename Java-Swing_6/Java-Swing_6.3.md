# 事件处理

教程总目录: [Java-Swing 图形界面开发（目录）](../README.md)

前面介绍每个组件时，几乎都已经介绍了相应事件的使用，这里仅对常用的事件做一个小整理。

### 1. 动作监听器 — ActionListener

动作监听器的动作通常为“点击动作”，常用的组件基本都支持该事件。如果有多个组件都需要设置动作监听器，可以为它们设置同一个实例，再为组件绑定不同的动作命令（ActionCommand）来区分当前触发事件的组件。

```java
final String COMMAND_OK = "OK";
final String COMMAND_CANCEL = "Cancel";

JButton okBtn = new JButton("OK");
okBtn.setActionCommand(COMMAND_OK);             // 按钮绑定动作命令

JButton cancelBtn = new JButton("Cancel");
cancelBtn.setActionCommand(COMMAND_CANCEL);     // 按钮绑定动作命令

// 创建一个动作监听器实例
ActionListener listener = new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        // 获取事件源，即触发事件的组件（按钮）本身
        // e.getSource();
    
        // 获取动作命令
        String command = e.getActionCommand();
        
        // 根据动作命令区分被点击的按钮
        if (COMMAND_OK.equals(command)) {
            System.out.println("OK 按钮被点击");
            
        } else if (COMMAND_CANCEL.equals(command)) {
            System.out.println("Cancel 按钮被点击");
        }
    }
};

// 设置两个按钮的动作监听器（使用同一个监听器实例）
okBtn.addActionListener(listener);
cancelBtn.addActionListener(listener);
```

### 2. 焦点监听器 — FocusListener

一个窗口内的所有组件（包括窗口本身）同一时间只能有一个组件获得焦点。

```java
JButton btn = new JButton("OK");
btn.addFocusListener(new FocusListener() {
    @Override
    public void focusGained(FocusEvent e) {
        System.out.println("获得焦点: " + e.getSource());
    }
    @Override
    public void focusLost(FocusEvent e) {
        System.out.println("失去焦点: " + e.getSource());
    }
});

JTextField textField = new JTextField(10);
textField.addFocusListener(new FocusListener() {
    @Override
    public void focusGained(FocusEvent e) {
        System.out.println("获得焦点: " + e.getSource());
    }
    @Override
    public void focusLost(FocusEvent e) {
        System.out.println("失去焦点: " + e.getSource());
    }
});
```

### 3. 鼠标监听器 — MouseListener

```java
JPanel panel = new JPanel();

panel.addMouseListener(new MouseListener() {
    @Override
    public void mouseEntered(MouseEvent e) {
        System.out.println("鼠标进入组件区域");
    }

    @Override
    public void mouseExited(MouseEvent e) {
        System.out.println("鼠标离开组建区域");
    }

    @Override
    public void mousePressed(MouseEvent e) {
        // 获取按下的坐标（相对于组件）
        e.getPoint();
        e.getX();
        e.getY();

        // 获取按下的坐标（相对于屏幕）
        e.getLocationOnScreen();
        e.getXOnScreen();
        e.getYOnScreen();

        // 判断按下的是否是鼠标右键
        e.isMetaDown();

        System.out.println("鼠标按下");
    }

    @Override
    public void mouseReleased(MouseEvent e) {
        System.out.println("鼠标释放");
    }

    @Override
    public void mouseClicked(MouseEvent e) {
        // 鼠标在组件区域内按下并释放（中间没有移动光标）才识别为被点击
        System.out.println("鼠标点击");
    }
});
```

### 4. 鼠标移动/拖动监听器 — MouseMotionListener

```java
JPanel panel = new JPanel();

panel.addMouseMotionListener(new MouseMotionListener() {
    @Override
    public void mouseDragged(MouseEvent e) {
        // 鼠标保持按下状态移动即为拖动
        System.out.println("鼠标拖动");
    }
    @Override
    public void mouseMoved(MouseEvent e) {
        System.out.println("鼠标移动");
    }
});
```

### 5. 鼠标滚轮监听器 — MouseWheelListener

```java
JPanel panel = new JPanel();

panel.addMouseWheelListener(new MouseWheelListener() {
    @Override
    public void mouseWheelMoved(MouseWheelEvent e) {
        // e.getWheelRotation() 为滚轮滚动多少的度量
        System.out.println("mouseWheelMoved: " + e.getWheelRotation());
    }
});
```

### 6. 键盘监听器 — KeyListener

组件监听键盘的按键，该组件必须要获取到焦点。

如果一个窗口内没有可获取焦点的组件，一般打开窗口后焦点为窗口所有，可以把键盘监听器设置到窗口（JFrame）身上。

如果窗口内还有其他组件可获取焦点（例如按钮、文本框），窗口打开后焦点会被内部组件获得，如果想要在窗口打开期间都能监听键盘按键，可以为所有可获得焦点的组件都设置一个键盘监听器。

```java
JFrame jf = new JFrame();

jf.addKeyListener(new KeyListener() {
    @Override
    public void keyPressed(KeyEvent e) {
        // 获取键值，和 KeyEvent.VK_XXXX 常量比较确定所按下的按键
        int keyCode = e.getKeyCode();
        System.out.println("按下: " + e.getKeyCode());
    }
    
    @Override
    public void keyTyped(KeyEvent e) {
        // e.getKeyChar() 获取键入的字符
        System.out.println("键入: " + e.getKeyChar());
    }
    
    @Override
    public void keyReleased(KeyEvent e) {
        System.out.println("释放: " + e.getKeyCode());
    }
});
```

### 7. 窗口监听器 — WindowListener

窗口监听器只有窗口类组件支持，例如 JFrame、JDialog。

```java
JFrame jf = new JFrame();

jf.addWindowListener(new WindowListener() {
    @Override
    public void windowOpened(WindowEvent e) {
        System.out.println("windowOpened: 窗口首次变为可见时调用");
    }

    @Override
    public void windowClosing(WindowEvent e) {
        System.out.println("windowClosing: 用户试图从窗口的系统菜单中关闭窗口时调用");
    }

    @Override
    public void windowClosed(WindowEvent e) {
        System.out.println("windowClosed: 窗口调用 dispose 而将其关闭时调用");
    }

    @Override
    public void windowIconified(WindowEvent e) {
        System.out.println("windowIconified: 窗口从正常状态变为最小化状态时调用");
    }

    @Override
    public void windowDeiconified(WindowEvent e) {
        System.out.println("windowDeiconified: 窗口从最小化状态变为正常状态时调用");
    }

    @Override
    public void windowActivated(WindowEvent e) {
        System.out.println("windowActivated: 窗口变为活动状态时调用");
    }

    @Override
    public void windowDeactivated(WindowEvent e) {
        System.out.println("windowDeactivated: 窗口变为不再是活动状态时调用");
    }
});

// 窗口焦点监听器
jf.addWindowFocusListener(new WindowFocusListener() {
    @Override
    public void windowGainedFocus(WindowEvent e) {
        System.out.println("windowGainedFocus: 窗口得到焦点");
    }

    @Override
    public void windowLostFocus(WindowEvent e) {
        System.out.println("windowLostFocus: 窗口失去焦点");
    }
});

// 窗口状态监听器
jf.addWindowStateListener(new WindowStateListener() {
    @Override
    public void windowStateChanged(WindowEvent e) {
        System.out.println("windowStateChanged: " + e.getNewState());
    }
});
```

