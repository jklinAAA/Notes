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



#### 使用Android的日志工具Log

- 在Android开发中，Log工具是一种常用的调试工具，用于输出程序运行时的日志信息。
- 通过Log，可以在开发阶段方便地追踪代码执行流程、变量值等信息，帮助定位和解决问题。
- 在四大组件中的Activity、Service、BroadcastReceiver、ContentProvider等，都可以使用Log工具记录相关日志。
- Log的使用方法包括：
  - `Log.d(TAG, message)`: 输出调试信息。
  - `Log.i(TAG, message)`: 输出一般信息。
  - `Log.w(TAG, message)`: 输出警告信息。
  - `Log.e(TAG, message)`: 输出错误信息。
- `TAG`一般是一个标签，用于标识日志的来源，方便过滤和查看。
- 在Android开发中，通过Log工具可以更有效地进行调试和监测应用程序的运行状态。



#### 继承与构造函数

##### 继承

- **继承**是面向对象编程的核心概念，允许一个类（子类）继承另一个类（父类）的属性和方法。

- 在Kotlin中使用 `: `关键字实现继承。

- 子类可以访问父类的属性和方法，同时可以重写父类的方法以适应特定需求。

- 示例：

  ```
  // 父类
  open class Animal(val name: String) {
      open fun makeSound() {
          println("Animal makes a sound.")
      }
  }
  
  // 子类继承父类
  class Dog(name: String) : Animal(name) {
      override fun makeSound() {
          println("Dog barks.")
      }
  }
  
  // 创建子类对象
  val myDog = Dog("Buddy")
  myDog.makeSound()  // 输出: Dog barks.
  ```

- `open` 关键字用于标识可被继承的类和方法，子类通过 `override` 关键字重写父类的方法。

##### 构造函数

- **构造函数**是用于创建类实例的特殊方法，负责对象的初始化工作。

- 在Kotlin中，类可以有一个主构造函数和一个或多个次构造函数。

- 主构造函数可以在类头部声明，次构造函数使用 `constructor` 关键字声明。

- 示例：

  ```
  // 类声明主构造函数
  class Person(val name: String, val age: Int) {
      // 次构造函数
      constructor(name: String) : this(name, 0)
  
      fun introduce() {
          println("Hello, my name is $name and I am $age years old.")
      }
  }
  
  // 创建类的实例
  val person1 = Person("Alice", 30)
  val person2 = Person("Bob")
  
  person1.introduce()  // 输出: Hello, my name is Alice and I am 30 years old.
  person2.introduce()  // 输出: Hello, my name is Bob and I am 0 years old.
  ```

- 主构造函数直接在类头部声明属性，次构造函数使用 `this` 关键字调用主构造函数。

- 使用次构造函数可以提供更多的初始化选项，但最终仍然需要调用主构造函数完成对象的初始化。

#### 

#### 2.5.4 数据类与单例类

##### 数据类（Data Class）

- 数据类是Kotlin语言中用于封装数据的特殊类。

- 使用 `data class` 关键字声明，不需要显式实现 toString、equals、hashCode等方法，Kotlin会自动生成。

- 数据类主要用于存储数据，典型应用包括表示实体对象，如用户、商品等。

- 示例：

  ```
  data class Person(val name: String, val age: Int)
  
  // 创建数据类对象
  val person = Person("Alice", 25)
  
  // 自动生成toString方法
  println(person)  // 输出: Person(name=Alice, age=25)
  
  // 自动生成equals方法
  val anotherPerson = Person("Alice", 25)
  println(person == anotherPerson)  // 输出: true
  ```

##### 单例类（Singleton Class）

- 单例类确保一个类只有一个实例，Kotlin中使用 `object` 关键字声明单例类。

- 单例类适用于全局唯一的实例，例如配置管理、资源管理等。

- 示例：

  ```
  object MySingleton {
      fun doSomething() {
          println("Doing something in singleton.")
      }
  }
  
  // 调用单例类的方法
  MySingleton.doSomething()
  ```

- 使用 `object` 声明的类即为该类的单一实例，不需要额外的实例化步骤。

### 2.6 Lambda编程

- Lambda表达式是Kotlin中引入的一项重要特性，用于简化匿名函数的语法。

- Lambda表达式的语法形式为：![image-20240126180025311](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126180025311.png)

- 主要用于函数式编程，可以在集合操作、回调等场景中简化代码。

- 示例：

  ```
  // Lambda表达式作为参数传递给函数
  val list = listOf(1, 2, 3, 4, 5)
  val squaredList = list.map { it * it }
  
  // Lambda表达式作为函数的参数
  fun operateOnNumber(num: Int, operation: (Int) -> Int): Int {
      return operation(num)
  }
  
  val result = operateOnNumber(5) { it * 2 }
  ```

- Lambda表达式可以带有参数，也可以作为参数传递给其他函数。

#### 集合的创建与遍历

- Kotlin专门提供了一个内置的listOf()函数来简化初始化集合的写法，如下所示：

`val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape")`



![image-20240126175332682](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175332682.png)

- 这里先使用mutableListOf()函数创建一个可变的集合，然后向集合中

添加了一个新的水果，最后再使用for-in循环对集合进行遍历。

- Set集合的用法几乎与此一模一样，只是将创建集合的方式换成了setOf()和mutableSetOf()函数而已。大致代码如下![image-20240126175446348](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175446348.png)

（需要注意，Set集合中是不可以存放重复元素的，如果存放了多个相同的元素，只会保留其中一份，这是和List集合最大的不同之处。）

- Map集合的用法

  传统的Map用法是先创建一个HashMap的实例，然后将一个个键值对数据添加到Map中。比如这里我们给每种水果设置一个对应的编号，就可以这样写：![image-20240126175626882](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175626882.png)

但更加推荐使用一种类似于数组下标的语法结构，比如向Map中添加一条数据就可以这么写：

![image-20240126175706824](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175706824.png)

Kotlin毫无疑问地提供了一对mapOf()和mutableMapOf()函数来继续简化Map的用法。在mapOf()函数中，我们可以直接传入初始化的键值对组合来完成对Map集合的创建：（to并不是关键字，而是一个infix函数）

![image-20240126175755429](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175755429.png)

#### 集合的函数式API

- Kotlin的集合库提供了强大的函数式编程 API，可以用于处理集合数据。
- 函数式编程的优势在于简化代码、提高可读性，并允许更方便地进行链式操作。
- Kotlin中集合的函数式API包括 `map`、`filter`、`reduce` 等常见的函数。

##### map

- `map` 函数用于将集合中的每个元素映射为另一个元素，返回一个新的集合。

```
 codeval numbers = listOf(1, 2, 3, 4, 5)

// 将集合中的每个元素平方
val squaredNumbers = numbers.map { it * it }

// 输出: [1, 4, 9, 16, 25]
println(squaredNumbers)
```

##### filter

- `filter` 函数用于根据指定的条件过滤集合中的元素，返回一个新的集合。

```
 codeval numbers = listOf(1, 2, 3, 4, 5)

// 过滤出偶数
val evenNumbers = numbers.filter { it % 2 == 0 }

// 输出: [2, 4]
println(evenNumbers)
```

##### reduce

- `reduce` 函数用于将集合中的元素进行累加、合并或其他操作，返回一个单一的值。

```
codeval numbers = listOf(1, 2, 3, 4, 5)

// 将集合中的元素累加
val sum = numbers.reduce { acc, num -> acc + num }

// 输出: 15
println(sum)
```

##### forEach

- `forEach` 函数用于遍历集合中的每个元素，并对其执行指定的操作。

```
 codeval numbers = listOf(1, 2, 3, 4, 5)

// 输出每个元素的平方
numbers.forEach { println(it * it) }
```

#### 字符串内嵌表达式

- Kotlin中字符串内嵌表达式的语法规则：![image-20240129230931202](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129230931202.png)

（当表达式中仅有一个变量的时候，还可以将两边的大括号省略）![image-20240129231001120](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129231001120.png)

###### **Activity**状态

- 运行状态
- 暂停状态
- 停止状态
- 销毁状态

#### **Activity**的生存期

- onCreate()。这个方法你已经看到过很多次了，我们在每个Activity

中都重写了这个方法，它会在Activity第一次被创建的时候调用。你应

该在这个方法中完成Activity的初始化操作，比如加载布局、绑定事件

等。

- onStart()。这个方法在Activity由不可见变为可见的时候调用。

- onResume()。这个方法在Activity准备好和用户进行交互的时候调

用。此时的Activity一定位于返回栈的栈顶，并且处于运行状态。

onPause()。这个方法在系统准备去启动或者恢复另一个Activity的

时候调用。我们通常会在这个方法中将一些消耗CPU的资源释放掉，

以及保存一些关键数据，但这个方法的执行速度一定要快，不然会影

响到新的栈顶Activity的使用。

- onStop()。这个方法在Activity完全不可见的时候调用。它和

- onPause()方法的主要区别在于，如果启动的新Activity是一个对话

框式的Activity，那么onPause()方法会得到执行，而onStop()方

法并不会执行。

- onDestroy()。这个方法在Activity被销毁之前调用，之后Activity

的状态将变为销毁状态。

- onRestart()。这个方法在Activity由停止状态变为运行状态之前调

用，也就是Activity被重新启动了。

##### 标准函数**with**、**run**和**apply**

with函数会在Lambda表达式中提供第一个参数对象的上下文，并使用Lambda表达式中的最后一行代码作为返回值返回。示例代码如下![image-20240129232631537](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129232631537.png)

run：

![image-20240129232808241](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129232808241.png)

apply：

![image-20240129232834682](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129232834682.png)
