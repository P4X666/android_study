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
