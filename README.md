# android_study
android 学习相关  

学习参考文档：  
+ [google官方文档](https://developer.android.google.cn/develop/ui/views/layout/declaring-layout)

## 第一天
### 环境配置
1. 配置`GRADLE_USER_HOME`，防止因`.gradle`过大而导致c盘爆满
### 配置代理
1. Settings --> System Settings --> HTTP Proxy 
2. 代理地址
    + 中国科学院开源协会镜像站地址:
        + http://mirrors.opencas.cn 端口：80
        + http://mirrors.opencas.org 端口：80
        + http://mirrors.opencas.ac.cn 端口：80
    + 上海GDG镜像服务器地址:
        + http://sdk.gdgshanghai.com 端口：8000
    + 北京化工大学镜像服务器地址:
        + http://ubuntu.buct.edu.cn/ 端口：80
        + http://ubuntu.buct.cn/ 端口：80 
        + http://ubuntu.buct6.edu.cn/ 端口：80
    + 大连东软信息学院镜像服务器地址: http://mirrors.neusoft.edu.cn 端口：80
    + 腾讯Bugly 镜像: http://android-mirror.bugly.qq.com 端口：8080
3. 觉得as默认的模拟器比较慢的话，可以配置`Genymotion`，[参考链接](https://blog.csdn.net/weixin_44871749/article/details/126044145)
### 单位和尺寸

dp(dip): device independent pixels(设备独立像素)，不依赖像素
sp: scaled(放大像素) 主要用于字体显示
ppi：每英寸像素数（pixel per inch），该值越高，则屏幕越细腻。
dpi：每英寸多少点（dot per inch），该值越高，则图片越细腻

### Activity
Android中，Activity是所有程序的根本，所有程序的流程都运行在Activity之中，如果把手机比作一个浏览器，那么Activity就相当于一个网页

### res的目录识别
+ drawable 存放能转换为绘制资源的位图文件或定义了绘制资源的xml文件。
+ layout 存放定义了用户界面布局的xml文件。
+ mipmap-hdpi 高分辨率图标目录。
+ mipmap-mdpi 中等分辨率图标目录，一般较少使用，除了兼容老旧手机。
+ mipmap-xhdpi 超高分辨率目录。
+ mipmap-xxhdpi 超超高分辨率目录，当前主流手机的分辨率。
+ mipmap-xxxhdpi 超超超高分辨率目录，如平板电视。
+ values
  存放定义了多种类型资源的xml文件，主要包括以下这些：
    + demens.xml：定义尺寸资源
    + string.xml：定义字符串资源
    + styles.xml：定义样式资源
    + colors.xml：定义颜色资源
    + arrays.xml：定义数组资源
    + attrs.xml：自定义控件时用的较多，自定义控件的属性。
  除了上述这些，可能还会涉及到以下目录：
+ menu 存放定义了菜单资源的xml文件。
+ raw 存放各种原生资源(音频、视频、一些XML文件等)。
+ anim 存放补间动画的XML文件
## 第二天
### 常见界面布局
1. **View**  
在Android中View类是最基本的一个UI类，基本上所有的高级UI组件都是继承View类实现的。Android应用的绝大部分UI组件都放在android.widget包及其子包、android.view包及其子包中，可以看到Android应用的所有UI组件都继承了 View类。View类是Android系统平台上用户界面表示的基本单元，View的一些子类被统称为Widgets （工具），提供了诸如文本输入框和按钮之类的UI对象的完整实现
所有的UI元素都是通过`View`与`ViewGroup`构建的，对于一个`Android`应用的用户界面来说，`ViewGroup`作为容器盛装界面中的控件，它可以包含普通的`View`控件，也可以包含`ViewGroup`
2. **界面布局编写方式**  
    1. 在xml中编写布局（推荐）
        + 数据视图分离，使程序结构更加清晰
    2. 在Java中编写
        + 在`Android`中所有的布局和控件都可以通过`new`关键字创建出来，将创建出来的`View`控件添加到`ViewGroup`布局中，从而实现`View`控件在布局中显示
3. **代码示例**  
    1. 使用`xml`编写
        1. 在`res/layout`目录下添加`xml`
            ```xml
            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
                          android:layout_width="match_parent"
                          android:layout_height="match_parent"
                          android:orientation="vertical" >
                <TextView android:id="@+id/text"
                          android:layout_width="wrap_content"
                          android:layout_height="wrap_content"
                          android:text="Hello, I am a TextView" />
            </LinearLayout>
            ```
        2. 在`MainActivity`中添加与上述`xml`的绑定
            ```java
            public void onCreate(Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
                // 通过 R.layout 来绑定xml
                setContentView(R.layout.main_layout);
            }
            ```
    2. 使用`java`编写
    ```java
    public class MainActivity extends AppCompatActivity {  
        @Override
        protected void onCreate(Bundle savedInstanceState){
            super.onCreate(savedInstanceState);
            //setContentView(R.layout.activity_main);
            // 创建一个线性布局
            LinearLayout layout = new LinearLayout (this);
            layout.setOrientation(LinearLayout.VERTICAL);   
            // 创建一个显示Hello World!的TextView
            TextView show = new TextView(this);
            show.setText("Hello World!");
            // 向layout容器添加一个TextView
            layout.addView(show);
            // 设置该Activity显示layout
            setContentView(layout);
        }
    }
    ```
4. 常见布局
    1. 线性布局，特点：以水平或垂直方向排列
        1. LinearLayout线性布局
        线性布局（LinearLayout）主要以水平或垂直方式来显示界面中的控件。当控件水平排列时，显示顺序依次为从左到右，当控件垂直排列时，显示顺序依次为从上到下
        2. orientation属性
        orientation属性控制控件排列方向，包含两个属性值：vertical(垂直)、horizontal(水平)；weight属性表示权重，类似与`flex`中的`flex-grow`,`flex-shrink`的概念
    2. 相对布局，特点：通过相对定位排列
        1. 相对布局（RelativeLayout）是通过相对定位的方式指定子控件位置，即以其它控件或父容器为参照物，摆放控件位置
        2. 相对布局—控件位置属性
        | 布局属性                         | 功能描述                             |
        | ------------------------------  | ------------------------------------ |
        | android:layout_centerInparent   | 设置当前控件位于父布局的中央位置        |
        | android:layout_centerVertical   | 设置当前控件位于父布局的垂直居中位置    |
        | android:layout_centerHorizontal | 设置当前控件位于父布局的水平居中位置    |
        | android:alignParentTop          | 设置当前控件是否与父控件顶端对齐        |
        | android:alignParentLeft         | 设置当前控件是否与父控件左对齐         |
        | android:alignParentRight        | 设置当前控件是否与父控件右对齐         |
        | android:alignParentBottom       | 设置当前控件是否与父控件底部对齐        |
        | android:above                   | 设置当前控件位于某控件的上方            |
        | android:below                   | 设置当前控件位于某控件的下方            |
        | android:toLeftOf                | 设置当前控件位于某控件的左侧            |
        | android:toRightOf               | 设置当前控件位于某控件的右侧            |
    3. 网格布局，`GridLayout`类似于前端中的`Grid`
    4. 帧布局，特点：开辟空白区域，帧里面的控件会叠加
    5. 表格布局，特点：表格形式排列
    6. 约束布局，特点：可视化编写布局

### 常见界面控件

#### TextView
1. 功能： 用于显示文本信息
2. 控件属性及功能描述  

| 控件属性               | 功能描述            |
| ---------------------  | ------------------ |
| android:id             | id                 |
| android:layout_width   | 控件宽度            |
| android:layout_height  | 控件高度            |
| android:layout_margin  | margin              |
| android:layout_padding | padding             |
| android:text           | 文本                |
| android:textColor      | 文本颜色             |
| android:textSize       | 文本大小，推荐单位sp  |
| android:gravity        | 设置文本内容的位置    |
| android:maxLength      | 文本最大长度，超出隐藏 |
| android:lines          | 文本行数，超出隐藏     |
| android:maxLines       | 文本最大行数，超出隐藏 |
| android:ellipsize      | 文本超出范围的显示方式 `start`,`middle`,`end`,`marquee`,通常与`android:singleline = "true"`搭配 |

#### Button
1. 功能：表示按钮，它继承自`TextView`控件，既可以显示文本，又可以显示图片，同时也允许用户通过点击来执行操作，当`Button`控件被点击时，被按下与弹起的背景会有一个动态的切换效果，这个效果就是点击效果
2. 实现点击事件
    + **在布局文件中**  
        1. 在`layout`中指定`onClick`属性
        ```xml
        android:onClick="click"
        ```
        2. 在`Activity`中实现方法
        ```java
        public void click(View v){
          Log.e("xml中的click方法", "onClick")
        }
        ```
    + **在`Activity`中**
        ```java
        Button btn = (Button) findViewById(R.id.btn);
        btn.setOnClickListener((View view)->{
          Log.e("内部类方式，前提是要在xml中提前写好id","onClick")
        })
        ```
#### EditView
1. 功能：它继承自`TextView`控件，用户可在此控件中输入信息，类似`input`
2. 控件属性及功能描述
| 控件属性                     | 功能描述                |
| --------------------------- | ----------------------- |
| android:editable            | 是否可编辑  disabled     |
| android:phoneNumber         | 类型为数字时的显示        |
| android:password            | 类型为密码时的显示        |
| android:scrollHorizontally  | 超出宽度时是否会出现横拉条 |
| android:hint                | placeholder             |
| android:textColorHint       | placeholder color       |

#### ImageView
1. 功能：可以加载各种图片资源
2. 控件属性及功能描述
| 控件属性                     | 功能描述                |
| --------------------------- | ----------------------- |
| android:background          | 背景，可以设置为图片     |
| android:src                 | src                    |
| android:scaleType           | 图片资源的缩放或移动     |
3. 代码示例
```xml
<ImageView
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:background="@drawable/bg"
/>
<ImageView
  android:layout_width="100dp"
  android:layout_height="100dp"
  android:src="@drawable/bg"
/>
```
#### RadioButton
1. 功能：`RadioButton`为单选按钮，`android:checked`属性指定是否选中的状态。`RadioGroup`是单选组合框，可容纳多个`RadioButton`，并把它们组合在一起，实现单选状态
2. 代码示例
```xml
<RadioGroup
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:orientation="vertical">
  <RadioButton
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textSize="25sp"
    android:text="男" />
  <RadioButton
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textSize="25sp"
    android:text="女" />
</RadioGroup>
```
#### CheckBox
1. 功能: `CheckBox`表示复选框，它是`Button`的子类，用于实现多选功能，通过`android:checked`属性指定`CheckBox`控件是否选中的状态
2. 代码示例
```xml
<CheckBox
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:text="羽毛球"
  android:textSize="18sp"/>
<CheckBox
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:text="乒乓球"
  android:textSize="18sp"/>
```
#### Toast
1. 功能: `Toast`是`Android`系统提供的轻量级信息提醒机制，用于向用户提示即时消息，它显示在应用程序界面的最上层，显示一段时间后自动消失不会打断当前操作，也不获得焦点
2. 代码示例
```java
Toast.makeText(MainActivity.this,"WIFI已断开",Toast.LENGTH_SHORT).show();
```
