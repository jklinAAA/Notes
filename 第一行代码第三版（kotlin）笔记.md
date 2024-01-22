#### 四大组件

Android系统四大组件分别是*Activity、Service、BroadcastReceiver*和*ContentProvider*。

- 其中Activity是所有Android应用程序的门面，凡是在应用中你看得到的东西，都是放在

Activity中的。

- 而Service就比较低调了，你无法看到它，但它会在后台默默地运行，即使用户退出了应用，Service仍然是可以继续运行的。

- BroadcastReceiver允许你的应用接收来自各处的广播消息，比如电话、短信等，当然，你的应用也可以向外发出广播消息。

- ContentProvider则为应用程序之间共享数据提供了可能，比如你想要读取系统通讯录中的联系人，就需要通过ContentProvider来实现

  

##### **Project**模式的项目结构

**AndroidManifest.xml**：程序中定义的所有四大组件都

需要在这个文件里注册，另外还可以在这个文件中给应用程序添加权限声明。（这个文件以后会经常用到）

![image-20240117163722244](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240117163722244.png)

这段代码表示对MainActivity进行注册，没有在AndroidManifest.xml里

注册的Activity是不能使用的。其中intent-filter里的两行代码非常重要，<action android:name="android.intent.action.MAIN"/>和<category android:name="android.intent.category.LAUNCHER" />表示MainActivity是这个项目的主Activity，在手机上点击应用图标，首先启动的就是这个Activity.

![image-20240117170858517](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240117170858517.png)

应用图标就是通过android:icon属性指定的，

应用的名称则是通过android:label属性指定的。



###### **res**目录下的结构:

所有以“mipmap”开头的目录都是用来放应用图标的，

所有以“values”开头的目录都是用来放字符串、样式、颜色等配置的，

所有以“layout”开头的目录都是用来放布局文件的。

打开res/values/strings.xml文件

##### ![image-20240117170437347](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240117170437347.png)

这里定义了一个应用程序名的字符串，我们有以下两种方式来引用它。

- 在代码中通过R.string.app_name可以获得该字符串的引用。
- 在XML中通过@string/app_name可以获得该字符串的引用。

基本的语法就是上面这两种方式，其中string部分是可以替换的，如果是引用的图片资源就可以替换成drawable，如果是引用的应用图标就可以替换成mipmap，如果是引用的布局文件就可以替换成layout，以此类推。

